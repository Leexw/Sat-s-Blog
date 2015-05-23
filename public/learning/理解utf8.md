---
####理解UTF8

#####字符乱码问题
前些天被字符乱码问题折腾得够呛，纠结了好几天。
问题如下：

将[http://ziyuansoso.com/search?wd=%E5%A5%BD&p=0&s=1000&ie=utf8][1]返回的JSON数据解析出来，然后分类展示。
使用的是ASI的接口，回调之后将request的responseData使用系统解析库解析

	       	NSError *error = nil;
 	       	id jsonObj = [NSJSONSerialization JSONObjectWithData:request.responseData
                                                 options:NSJSONReadingMutableContainers
                                                   error:&error];

结果发现解析失败，返回错误码3840.

接下来使用requset.responseString打印出返回的titlle字段含有乱码，并且在ASI的request调用responseString时，发现其使用的encoding是NSISOLatin1StringEncoding ，既是ASI默认的编码方式。

	       	“"title":"TVBNOW ä¸–å￥½ç^”

追踪下去，继续发现服务器没有在responseHeader中设置charset为UTF8，遂手动将网络请求返回的数据使用UTF8编码转换一次

 	       	NSString *string = [[NSString alloc] initWithData:request.responseData encoding:NSUTF8StringEncoding];

结果发现string 为 nil ！！


然后将[http://ziyuansoso.com/search?wd=%E5%A5%BD&p=0&s=1000&ie=utf8][2]使用Mac版的Chrome打开，发现一样是乱码，不过当手动选择编码为UTF8之后，就一切正常了。
	       
		   	“"title":"TVBNOW ä¸–å￥½ç^”  —>"title":"TVBNOW 世好爸"

继续用其他进行对比，使用Safari，正常！安卓弟兄们的代码运行解析正常！

检查了各个逻辑，并尝试了很多种方案，最后有几个内容是明确的：

1.  服务器没有设置charset为UTF8是不对，但是也不应该影响解析；
2.  使用Mac版浏览器，第一次打开会存在乱码，但是选UTF8转码后就正常；
3.  使用iOS平台主流的浏览器打开，都是乱码，使用安卓平台自带的浏览器也是乱码；
4.  安卓弟兄们的代码运行正常，使用的解析代码是安卓内置的Apache HttpClient库，并没有做其他处理，就只是转成UTF8；
5.  将返回的数据到[http://i-tools.org/charset][3]中检测，显示其确实是UTF8编码


我们使用的是iOS自带的字符转码API，但是为什么不成功，不解不解？？？？！！！
经过了3天。。。

最后在服务器、团队成员、主管的共同参与讨论之下，才得出结论：

原因是虽然请求的是UTF8编码的数据，但返回的数据中，有些字段不是UTF8编码，则导致转码失败！
应该对title字段，单独进行一次UTF8编码。


之前就应该使用二进制查看器，确定是否是UTF8。

#####UTF8的理解
下面是自己对Unicode和UTF8的理解。

Unicode就是一张巨大的字符 - 编码的对应表，它将世界上几乎所有的字符都囊括其中。将字符都用唯一的编码来表示，如U+674E表示李，如U+0639表示阿拉伯字母Ain。

注意，Unicode只定义了对应表，并没有说明这种编码是如何在计算机世界存储的。

UTF8就是一种存储方式，是不定长的，以8bit为最小单位的存储方式。

在[阮一峰的博客][4]中能够看到下图：
![utf8unicode](http://7xitbl.com1.z0.glb.clouddn.com/utf8unicode.png)

可以看到，UTF8的编码方式是使用字节左端来标识：

1. 如果左边第一位为0，则当前字节就为一个完整的字符；
2. 如果左边第一位为1，并且第二位为0，则当前字节为字符的一部分；
3. 如果左边第一位为1，并且第二位也为1，则表示当前字节为字符的头字节，该字节有多少个1，就表示有多少个字节来表示当前字符；

说说UTF8的派生物：

1. 在Windows中，许多Windows程序（如自带的记事本）会在UTF8文件的开头加入一段字节串EF BB BF ，如果没有预期要处理UTF8的文本编辑器或者浏览器，就会显示为ISO-8859-1字符串”ï»¿”（就像本文开头说到的，服务器没有在responseHeader中设置charset）；
2. Java同时支持标准UTF8和变种UTF8，变种UTF8的特殊点为空字符(U+0000)使用两个字节存储，以及最多使用3个字节来表示Unicode；


参考：

[http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html][6]

[http://zh.wikipedia.org/wiki/UTF-8][7]

[http://docs.oracle.com/javase/7/docs/api/java/io/DataInput.html#modified-utf-8][8]


  [1]:http://ziyuansoso.com/search?wd=%E5%A5%BD&p=0&s=1000&ie=utf8
  [2]:http://ziyuansoso.com/search?wd=%E5%A5%BD&p=0&s=1000&ie=utf8
  [3]:http://i-tools.org/charset
  [4]:http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html
  [5]: ../uploads/2014-02-25/utf8unicode.png
  [6]:http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html
  [7]:http://zh.wikipedia.org/wiki/UTF-8
  [8]:http://docs.oracle.com/javase/7/docs/api/java/io/DataInput.html#modified-utf-8
