## Eclipse 安装配置Open Liberty Server & WebSphere Liberty Server
### 1. Open Liberty Server & WebSphere Liberty Server介绍
Open Liberty 和 WebSphere Liberty 是两种现代化的 Java 应用服务器，由 IBM 开发和维护。它们为 Java 应用程序提供了一个运行时环境，特别是为 Java EE (现在称为 Jakarta EE) 和 MicroProfile 应用程序设计。以下是这两个产品的简要介绍：

1. **Open Liberty**:
   - **开源**：Open Liberty 是完全开源的 Java 应用服务器，可以在 [GitHub](https://github.com/OpenLiberty/open-liberty) 上找到它的源代码。
   - **轻量级**：设计时考虑了微服务和云原生架构，因此它是轻量级的，并且启动速度快。
   - **灵活性**：用户可以选择需要的特性和功能，这意味着只有真正需要的组件会被加载和启动，这有助于减少内存占用和启动时间。
   - **支持标准**：支持最新的 Jakarta EE 和 MicroProfile 标准。
   - **开发友好**：提供了开发模式，使得开发人员可以在修改代码后立即查看更改，无需重启服务器。

2. **WebSphere Liberty**:
   - **商业产品**：虽然它与 Open Liberty 共享相同的核心代码库，但 WebSphere Liberty 是 IBM 的商业产品，为企业级客户提供额外的功能和支持。
   - **子集与超集**：你可以认为 WebSphere Liberty 是 Open Liberty 的超集，因为它包含了 Open Liberty 的所有功能，并添加了更多的企业级特性。
   - **持续更新**：与 Open Liberty 一样，WebSphere Liberty 也经常得到更新，以支持最新的技术标准和提供改进。
   - **集成**：为企业级客户提供更深入的监视、管理和操作功能，以及与其他 IBM 产品的更好集成。
### 2. Eclipse WebSphere Liberty Server安装设置
接下来我会在Windows环境中安装Eclipse并为其设置WebSphere Liberty Server，Open Liberty Server的设置与其类似，只需要下载不同的Server即可。WebSphere Application Server如果用在本地开发环境是不收费的，如果用做商业软件则需要购买License。
#### 2.1 安装Openjdk8
推荐到RedHat官网下载Installer版的最新Openjdk8，Installer版的安装只需运行安装程序即可，无需手动配置环境变量。[RedHat官网链接](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?downloadType=distributions&product=core.service.openjdk&version=1.8.0.382) 
![在这里插入图片描述](https://img-blog.csdnimg.cn/29b1ee2bb02e426293e863ce409aa743.png)
#### 2.2 安装Eclipse IDE for Enterprise Java and Web Developers
这个版本的Eclipse功能最强大，专门为企业级Java和Web开发人员设计。[Eclipse官网链接](​​https://www.eclipse.org/downloads/packages/) 

> 建议先不要下载最新版的Eclipse，我在23-03版本上测试没有问题

#### 2.3 安装Eclipse中安装IBM Liberty Developer Tools插件
IBM Liberty Developer Tools（简称 LDT）是为 IBM Liberty 应用服务器（包括 WebSphere Liberty 和 Open Liberty）设计的一套开发工具。这些工具旨在帮助开发者更有效地创建、运行、测试和部署适用于 Liberty 的应用程序。LDT 主要是作为 Eclipse IDE 的插件提供，以完善 Eclipse 的 Java EE 和 MicroProfile 开发体验。

打开Eclipse后在Help菜单来，选择Eclipse Marketplace，而后输入"Liberty"关键字搜索。
![在这里插入图片描述](https://img-blog.csdnimg.cn/5b3b502a4c0b454e9f6cc473f4c844db.png)
按照默认推荐的组件下载即可。
![在这里插入图片描述](https://img-blog.csdnimg.cn/ef1bae56c98e4249a2364af0a22260bf.png)
因为“你懂的”原因可能会出现下载比较慢的情况，这种情况可以去Eclipse Marketplace官网下载。[EclipseMarketplace官网链接](https://marketplace.eclipse.org/) 
#### 2.4 下载WebSphere Liberty Server
请到Maven repo的官网去搜索相关的WebSphere Liberty Server & Open Liberty Server包，
[Maven repo官网](https://mvnrepository.com/) 
WebSphere Liberty Server搜索“wlp”关键字
Open Liberty Server搜索“OpenLiberty javaEE”关键字

我这里以Wlp JavaEE8作为演示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/7d478878f7694db1b9688b06cd95c6cf.png)
下载zip格式的：
![在这里插入图片描述](https://img-blog.csdnimg.cn/f8960adb4d2b4074801225ce6a1cfbb1.png)
#### 2.5 Eclipse设置WebSphere Liberty Server
解压上一步下载的zip包，得到一个wlp的目录(WebSphere Liberty Server所在目录)。创建一个新Server，选择IBM->Liberty Server
![在这里插入图片描述](https://img-blog.csdnimg.cn/4289ea6d457d462396ed69282b0ade1e.png)
选择之前解压出来的“wlp”路径作为“Liberty Runtime Environment”，其余的按照默认值选择即可。
![在这里插入图片描述](https://img-blog.csdnimg.cn/73640331272045b1837a23a4cf704a62.png)
#### 2.6 使用WebSphere Liberty Server运行一个简单的JavaWeb程序
新建一个“Dynamic Web Project”
![在这里插入图片描述](https://img-blog.csdnimg.cn/b5397ad7b95b4e76959797f970a8b689.png)
webapp路径下新建一个“index.html”文件，其中随便写的内容即可。
![在这里插入图片描述](https://img-blog.csdnimg.cn/baad44c84d0644d2a95b5d8de5dfa90b.png)
右键点击“Liberty Server”选择“Add and Remove”
![在这里插入图片描述](https://img-blog.csdnimg.cn/f4b7040e9e8f4c45b94dcaf052f488dd.png)
将testWeb工程添加进去
![在这里插入图片描述](https://img-blog.csdnimg.cn/2b690aefbe9f4009994675f6795655cf.png)
由于安装了“IBM Liberty Developer Tools”插件，server.xml文件会自动配置。

在 WebSphere Liberty 中，server.xml 文件是服务器配置的核心文件。它为 Liberty 服务器实例定义了各种配置和特性。server.xml 文件是声明性的，允许您指定服务器的运行时行为、启用的特性、应用程序部署信息以及其他相关设置。如果想了解详细信息请参考 [WebSphere Liberty官网](https://www.ibm.com/docs/en/was-liberty/core?topic=overview-server-configuration) 或 [Open Liberty官网](https://openliberty.io/docs/latest/reference/config/server-configuration-overview.html) 
![在这里插入图片描述](https://img-blog.csdnimg.cn/d6384c8fbd0742fc974c00df3b41b146.png)
第一次启动，需要填一个设置一个KeyStore，需要提供一个用户名密码，建议填写一个复杂的，不然启动Server会有Error（该Error不影响Server正常运行），看到如下提示则代表程序启动成功：
![在这里插入图片描述](https://img-blog.csdnimg.cn/be05958d8755451ca4936c2c772cadb0.png)
页面尝试访问，Liberty Server运行的默认端口是9080
![在这里插入图片描述](https://img-blog.csdnimg.cn/b7082d5fe30d4b48bfdf61f6b74bebee.png)
