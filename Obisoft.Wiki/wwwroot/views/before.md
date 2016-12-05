# 欢迎来到Obisoft文档中心
欢迎。

这将是你阅读的文档中最简练的一份。

左侧是目录。用于检索API。

BeautyTeam是Obisoft旗下敏捷办公平台。本文档包含BeautyTeam的全部开发文档。

Obisoft为了识别用户，每个用户针对服务器都会产生唯一ID。

**注意：Obisoft没有接入OAuth。如果要实现第三方登录，则使用这个ID区分用户** 

开发者另外需要注意

    * 如果发现服务器Code=-5返回值，请尽快联络我们。
    * 必须实现HTTPS
    * 开发者需要一款接口调试工具来调试接口。例如：Postman
    * 在开发过程中遇到困难，则可以前往社区讨论

最后，祝开发者开发顺利。

### 开始开发前

开发者必须拥有Obisoft账号。[登录](/Manage)

必须创建你的应用程序。创建按钮在本页面右上角。

**请记录你的App的AppId和AppSecret。**

我们会使用你的AppId来记录你的API调用记录并追究非法调用的相关责任。使用AppId来区分应用

### AppId和AppSecret

AppId和AppSecret用于换取临时性Token，保证安全性

Token是你调用所有API的凭据

每个Token可以生存**两小时**  

每天至多可以换**2000**次Token。不要在每次需要Token的时候都换一次Token

**不要每次调用API就索取一次Token! 否则会很快把今天50次机会用完。**

### 安全性

**AppSecret安全性要求极高。不要把AppSecret传给客户端!**  

如果你拥有你的服务器集群，也不要把AppSecret保存在服务器上! 

使用一台高安全性的中转服务器换Token，把Token传给需要调API的客户端或服务器

用于换Token的中转服务器的Token下发服务不允许外网访问，不允许访问数据库，即可保证AppSecret安全

### Token的递交和存储

Token采用Cookie存储。   

	Cookie名称：Token
	Cookie值：Token的值
	Cookie生存期：两小时

所以请保证每次调用API的时候，检查Cookie里面Token是否已经过期。如果过期了，那么应该立即更新Token

也可以使用API来检查Token是否还合法。不推荐这样做，这样会导致每次调用API都增加一次握手

