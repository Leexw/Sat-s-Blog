####如何安装和使用CocoaPods

当你的项目要用到第三方库的时候，CocoaPods就派上大用场了！

不再需要手动下载代码，添加各种path ，各种flag！

只需要修改Podfile配置文件，再运行pod install命令就ok了

1. 通过ruby gem命令安装 
	   
	       	$ sudo gem install cocoapods
  
   如果出现以下文字则说明安装成功
  
			Successfully installed cocoapods-0.29.0
            Parsing documentation for activesupport-3.2.17
            Installing ri documentation for activesupport-3.2.17
            Parsing documentation for claide-0.4.0
            Installing ri documentation for claide-0.4.0
            Parsing documentation for cocoapods-0.29.0
            Installing ri documentation for cocoapods-0.29.0
            Parsing documentation for cocoapods-core-0.29.0
            Installing ri documentation for cocoapods-core-0.29.0
            Parsing documentation for cocoapods-downloader-0.3.0
            Installing ri documentation for cocoapods-downloader-0.3.0
            Parsing documentation for cocoapods-try-release-fix-0.1.1
            Installing ri documentation for cocoapods-try-release-fix-0.1.1
            Parsing documentation for colored-1.2
            Installing ri documentation for colored-1.2
            Parsing documentation for escape-0.0.4
            Installing ri documentation for escape-0.0.4
            Parsing documentation for fuzzy_match-2.0.4
            Installing ri documentation for fuzzy_match-2.0.4
            Parsing documentation for i18n-0.6.9
            Installing ri documentation for i18n-0.6.9
            Parsing documentation for json_pure-1.8.1
            Installing ri documentation for json_pure-1.8.1
            Parsing documentation for multi_json-1.8.4
            Installing ri documentation for multi_json-1.8.4
            Parsing documentation for nap-0.6.0
            Installing ri documentation for nap-0.6.0
            Parsing documentation for open4-1.3.2
            Installing ri documentation for open4-1.3.2
            Parsing documentation for xcodeproj-0.14.1
            Installing ri documentation for xcodeproj-0.14.1
            Done installing documentation for activesupport, claide, cocoapods, cocoapods-core, cocoapods-downloader, cocoapods-try-release-fix, colored, escape, fuzzy_match, i18n, json_pure, multi_json, nap, open4, xcodeproj after 19 seconds
            15 gems installed


   如果不成功，可能是被墙了，我们可以使用淘宝的Ruby镜像来访问cocoapods.	
   依次输入以下命令
   
            $ gem sources --remove https://rubygems.org/
            $ gem sources -a http://ruby.taobao.org/
 
   出现以下内容时说明已经成功了
   
            http://ruby.taobao.org/ added to sources			
 
   这时再次输入
   
            $ sudo gem install cocoapods
   


2. 创建Podfile配置文件
    
   进入你的工程路径
   
            $ cd <your product path>
 
   输入以下命令进行创建
   
			$ sudo touch Podfile

   进入编辑界面
   
			$ vi Podfile

   添加以下内容(注意要输入你的project支持的最低系统)
   以下是添加著名第三方库
   
			platform :ios, '6.0'
			pod 'AFNetworking'	
   
   保存以上修改
   
			按键盘esc ，再输入：，最后输入wq!，按回车结束	



3. 输入命令安装生成xcworkspace

			$ pod install 
  
   之后出现以下信息说明已经成功：
   
			Analyzing dependencies
			Downloading dependencies
			Generating Pods project
			Integrating client project



4. Finder打开所在目录就会有xcworkspace ，双击打开此文件就行

如图所示：

![xcworkspace](http://7xitbl.com1.z0.glb.clouddn.com/xcworkspace.png)


参考：

[http://www.xujingbao.com/blog/2013/04/26/cocoapods/][2]
[http://stackoverflow.com/questions/17265674/cocoapods-doesnt-install-pods-for-ios7-and-xcode-5][3]
[http://code4app.com/article/cocoapods-install-usage][4]


  [1]: ../uploads/2014-02-25/xcworkspace.png
  [2]:http://www.xujingbao.com/blog/2013/04/26/cocoapods/
  [3]:http://stackoverflow.com/questions/17265674/cocoapods-doesnt-install-pods-for-ios7-and-xcode-5
  [4]:http://code4app.com/article/cocoapods-install-usage

