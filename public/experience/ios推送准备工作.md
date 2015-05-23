####iOS推送准备工作

**此篇日志只是用来记录iOS推送需要使用的pem文件生成过程，以及会附上一段php推送代码。**

######推送准备
1.	在[https://developer.apple.com/account/ios/certificate/certificateList.action][1]里更新该项目的App ID（前提是该项目具有自己的App ID），设置其支持推送。
    ![apns1](http://7xitbl.com1.z0.glb.clouddn.com/apns1.png)

2.	生成两种环境的SSL证书（测试、发布）；需要先创建CSR文件 ，之后把.certSigningRequest保存在本地
    ![apns2](http://7xitbl.com1.z0.glb.clouddn.com/apns2.png)
	
    然后之前的页面上点击 “Creat …”
	![apns3](http://7xitbl.com1.z0.glb.clouddn.com/apns3.png)

    之后上传CSR文件
	![apns4](http://7xitbl.com1.z0.glb.clouddn.com/apns4.png)

    然后依次把生成的Development SSL和Production SSL文件下载并保存在本地。

3.	新建开发证书（一般我们的开发证书都带有通配符*，目的是能够适配所有的App ID），因为APNS不支持带有通配符的证书，所以需要新建专门的开发证书；这里不配图，之前有文档说明


4.	更新发布证书，重新下载，安装到Xcode；

5.	根据服务器的需要，将SSL证书转换成.p12或者.pem 文件。

    转换成.p12 ：
    打开“钥匙串访问”，选中左边栏“登录”，然后进行
	![apns5](http://7xitbl.com1.z0.glb.clouddn.com/apns5.png)

    导入之后，右键选中该证书，选择“导出”
	![apns6](http://7xitbl.com1.z0.glb.clouddn.com/apns6.png)
	

    之后输入文件名，点击确认，之后会弹出“输入密码保护框”，建议之间回车，不使用密码。

	有两种方式：1个pem文件；key.pem与cert.pem。
	
	转换成1个pem文件：先把文件转换成.p12文件，之后在Mac系统下的终端输入命令
	
        openssl pkcs12 –in xxx.p12 –out  xxx.pem -nodes –clcerts
    ![apns7](http://7xitbl.com1.z0.glb.clouddn.com/apns7.png)

    上面的输入密码就是之前导出时输入的密码，因为在这里没有设置密码，所以直接回车就行。

    转换成2pem文件：分别将cert和key导出成p12，然后使用命令
	
		openssl pkcs12 -clcerts -nokeys -out apns-dev-cert.pem -in apns-dev-cert.p12
		openssl pkcs12 -nocerts -out apns-dev-key.pem -in apns-dev-key.p12转成pem。

	注意：将apns-dev-key.p12转成apns-dev-key.pem的时候必须输入passphrase，可以随意输入一个，等转换完成之后，再执行openssl rsa -in apns-dev-key.pem -out apns-dev-key-noenc.pem，将之前输入的passphrase去除，在移除的时候需要输入passphrase。

    如果要将2个pem合成1个，则可以使用以下命令：

        cat apns-dev-cert.pem apns-dev-key-noenc.pem > apns-dev.pem




    备注：
	
	APNS详解[http://blog.csdn.net/sxfcct/article/details/7939082][2]
	
	如何实现APNS？[http://blog.163.com/ray_jun/blog/static/167053642201231144540434/][3]

#####PHP推送代码
附：PHP推送代码 ，欢迎拷贝！

        <?php

		//1. 把上报的Token填入（注意不要有空格）
		$deviceToken = '2353584a53ceaeda45d9768852219d5da82a7cfe75edc2317a4981093fde8653';

		//2. message:推送的信息，如果要使用中文推送，则注释英文$message，打开中文$message
		$message = 'push content' ;
		//$message = 中文推送内容，不要括号 ;

		//3. title:推送的标题，如果要使用中文推送，则注释英文$title，打开中文$title
		$title =  'title';
		//$title = 中文推送标题，不要括号 ;

    
    
		// 这个是推送pem的密码，不用管.
		$passphrase = '';
    
		$ctx = stream_context_create();
    
    
		//4. 替换pem的文件名，确保正确！如下面写的是yunboiPhone_Development.pem
		stream_context_set_option($ctx, 'ssl', 'local_cert', 'yunboiPhone_Development.pem');
		stream_context_set_option($ctx, 'ssl', 'passphrase', $passphrase);

    
		// Open a connection to the APNS server
		$fp = stream_socket_client(
			'ssl://gateway.sandbox.push.apple.com:2195', $err,
			$errstr, 60, STREAM_CLIENT_CONNECT|STREAM_CLIENT_PERSISTENT, $ctx);

		if (!$fp)
			exit("Failed to connect: $err $errstr" . PHP_EOL);

		echo 'Connected to APNS' . PHP_EOL;

		// Create the payload body
		$body['aps'] = array(
			'alert' => $message,
		    'title' => $title,
			'sound' => 'default'
			);

		// Encode the payload as JSON
		$payload = json_encode($body);

		// Build the binary notification
		$msg = chr(0) . pack('n', 32) . pack('H*', $deviceToken) . pack('n', strlen($payload)) . $payload;

		// Send it to the server
		$result = fwrite($fp, $msg, strlen($msg));

		if (!$result)
			echo 'Message not delivered' . PHP_EOL;
		else
			echo 'Message successfully delivered' . PHP_EOL;

		// Close the connection to the server
		fclose($fp);	

这个脚本是最初写给测试组测试用的，为此还专门写了篇短文说明：

**前提条件**：

1. 向开发组获取具体项目的推送证书——pem文件 ；
2. 推送的脚本 ——VipMobilePush.php；
3. Mac OS系统

说明：在windows当然也没问题，不过需要安装PHP解析器，而Mac OS自带这个功能，如有需要后续研究给出文档。

**准备步骤**：

1. 确保pem文件正确，和开发小组核对文件；
2. 根据上报或者询问开发，获取需要测试推送的设备Token，需要填入php脚本；
3. 根据推送内容，使用自带应用‘文本编辑’修改VipMobilePush.php（脚本里有注释，按注释1234来改）；
4. 将修改好的VipMobilePush.php和.pem文件放入同一目录下；

**操作步骤**：

1.  打开自带应用‘终端’，使用’cd’命令进入该目录；
2.  输入 php VipMobilePush.php，运行该php文件

示例：

     $  cd /Users/muzihuowei/Desktop/VipMobilePush 
     $  php VipMobilePush.php


[1]:https://developer.apple.com/account/ios/certificate/certificateList.action
[2]:http://blog.csdn.net/sxfcct/article/details/7939082
[3]:http://blog.163.com/ray_jun/blog/static/167053642201231144540434/

[10]: ../uploads/2014-04-29/apns1.png
[11]: ../uploads/2014-04-29/apns2.png
[12]: ../uploads/2014-04-29/apns3.png
[13]: ../uploads/2014-04-29/apns4.png
[14]: ../uploads/2014-04-29/apns5.png
[15]: ../uploads/2014-04-29/apns6.png
[16]: ../uploads/2014-04-29/apns7.png

