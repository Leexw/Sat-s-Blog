###以下步骤简要说明创建新应用的过程：

-	创建App ID
-	创建发布证书
-	登录 iTunes connect，创建App
####一、创建App ID (目的:在app store上⽤用来唯⼀一标识app)
![](http://7xitbl.com1.z0.glb.clouddn.com/Screen Shot 2015-05-22 at 11.08.02 PM.png)
有两处填项:App ID Description、Bundle Identify(App ID suffix)
**description**：这个是描述，在创建发布证书的时候需要⽤到，⻅名知意就好，只是⽤来告诉⾃己这是什么应用程序的ID
**Bundle Identify**：这个要认真写，要确保和你账号中现有的Bundle Identify不⼀样，这⾥的信息会显示在itunes connect⾥里的app information中,它代表的是Bundle ID;
示例:description : lixianHD
Bundle Identify : com.xunlei.lixianxiazaiHD
填好之后,会在这⾥显⽰出来
![](http://7xitbl.com1.z0.glb.clouddn.com/7022F039-7B28-4215-923C-9BBF00E5D956.png)
通过在其后面加Bundle Identify就能够唯一标识你的应⽤程序。
****
####二、创建发布证书(目的: 需要⽤发布证书来编译发布程序包,并通过发布证书来唯⼀标识程序包)
![](http://7xitbl.com1.z0.glb.clouddn.com/7C474AB2-91CF-4E10-91F1-D23BC6430C72.png)
有三处所填项:Destribution Method 、Profile Name 、App ID
**Destribution Method**: 选择App store
**Profile Name**:是此发布证书的名字，要和现在已有的发布证书区分开来，且要⻅名知意，一般会加Distribution的后缀
**App ID**:选择之前创建的App ID，这⾥里显示的是App ID的description;
⽰例:
profile Name :lixianHD_ Distribution
App ID: lixianHD(这个是迅雷离线下载App ID的 description)完成之后，会在这⾥显示:
![](http://7xitbl.com1.z0.glb.clouddn.com/08F95124-2B44-482E-92FA-5C36D8325357.png)
创建完成之后,点击download，下载保存起来，在打发布程序包的时候要⽤到;

****

####三、登录 iTunes connect，点击Add New App(目的:编写应用程序的类型、版本号、发布市场等信息)

之前的是创建应⽤程序唯⼀标识的身份，现在才是创建应用程序所该具备的信息。经过上诉两个步骤之后,还要准备的有:
a. 确定应⽤程序的名称，这个要在App store上展示;b. 确定SKU Number，这个是⽤来区别于同一开发者账号下的程序标识 (详⻅下⽂说明);c. 确定应⽤的⾯向市场，一般为China ;d. 1024*1024的应⽤程序图标和至少⼀张应⽤截图;
点击 Manage Your Applications，然后点击 Add New App ;
![](http://7xitbl.com1.z0.glb.clouddn.com/BAC8BFBA-30E8-404C-A42D-C15E5B87A8A2.png)
这⾥有三处填框: App Name\SKU Number\Bundle ID，这三者创建了之后,以后就不能修改;
**App Name**: 这个名称会在App store上显⽰示,提交后就不能再改;
**SKU Number**: SKU是物流管理的术语，⽤来标识产品，这⾥里的SKU Number是⽤来标识你的应⽤程序，只要和同⼀帐号下的程序不⼀样就行;
**Bundle ID**:也可以说App ID，它就是应⽤程序的身份证，用来在App store中唯一标识⾃己，这个选择之前创建的App ID就行;
⽰例:
选择 iOS App ;
Default Language :默认就是中文，选中⽂就好
App Name:迅雷离线下载HD ;
SKU Number:lixianHD
Bundle ID:选择 com.xunlei.lixianHD;
之后进⼊应⽤用程序详细信息的填写界⾯面:![](http://7xitbl.com1.z0.glb.clouddn.com/Screen Shot 2015-05-22 at 11.21.55 PM.png)
**Availability Date** : 就是默认时间;
**Price Tier**: 如果免费就选free ,如果收费就选择相应的价钱; 
**Discount for educational institutions** :按照默认;
**Custom B2B App**:默认不勾选;
**Specific Stores**:⼀般我们的市场都是⾯向中国大陆 , 选择China !
接着输⼊程序基本信息:
![](http://7xitbl.com1.z0.glb.clouddn.com/Screen Shot 2015-05-22 at 11.23.05 PM.png)
这些按规矩来填，填写提交之后可以修改;
接着上传应用程序图标和截图:
![](http://7xitbl.com1.z0.glb.clouddn.com/Screen Shot 2015-05-22 at 11.23.51 PM.png)
我上传的时间是2012年10⽉月30⽇日，当时系统已经要求图标尺⼨为1024x1024，之前是512x512 ;
接下来还需要填写联系人信息、程序的描述、关键词、支持URL等等。这些都可以在后续修改。
