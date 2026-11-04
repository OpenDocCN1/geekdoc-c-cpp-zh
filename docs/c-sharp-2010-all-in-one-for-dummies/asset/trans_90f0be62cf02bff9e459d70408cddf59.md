
![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_782_0.png)

图3-8：
发布Web对话框。

你可以一次性设置配置文件，之后每次需要重新发布应用程序时都可以重复使用。非常方便。

## 使用服务

剩下的就是使用它了。

正如所料，为WCF服务设置服务引用与为ASMX服务设置引用非常相似。仍然是右键单击并选择“添加服务引用”，仍然会得到图3-9所示的对话框，并且仍然可以在代码中轻松引用该服务。

有两件事需要记住：

- 你要查找的文件扩展名是`.svc`。
- 你设置的绑定对你来说是抽象的。

文件名那部分还行，但绑定很重要。请记住，绑定的选择对开发人员是不可见的，但它对功能尤其是性能有显著影响。选择使用哪种绑定不可草率决定；只有在经过大量研究和需求分析之后才能做出决定。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_783_0.png)

图3-9：
添加WCF服务引用。

## 第4章：使用ReST构建Web服务

### 本章内容包括

- ✔ 理解ReST的原则
- ✔ 使用WCF实现ReST服务
- ✔ 使用ReST服务

第3章中有一个侧边栏“使用不同的端点”，其中列出了可以与WCF一起使用的大量绑定格式。我指出，对于大多数应用程序，你使用SOAP或二进制。这并不一定准确。

另一种绑定非常流行——它是Web浏览器从Web服务器获取页面时使用的绑定。它被称为ReST，代表Representational State Transfer（表述性状态转移）。

在本章中，我将向你介绍ReST，并带你了解它的优点和缺点。

### 初识ReST

ReST基本上就是传统GET和POST模式的使用，老一代人还记得CGI。对于你们这些新手来说，它是Web请求的基本格式。例如，当你点击一个如下所示的链接时：

```
http://mydomain.com/start.aspx?id=3
```

...你就是在使用ReST。请记住，我们在这里不是讨论实现。我们讨论的是一种远程过程调用机制。它只是将查询参数发送到远程机器并获取返回数据的一种方式。

我们也不是在讨论像SOAP那样的协议。ReST是一种架构。它有指导原则，而不是规则。

ReST接口有四个目标。它们是：

- 组件交互的可扩展性
- 接口的通用性
- 组件的独立部署
- 中间组件以减少延迟、加强安全并封装遗留系统

在WCF中使用ReST满足其中大部分目标，但并非全部。让我们快速了解一下ReST在WCF中的实现细节，然后你可以自己做决定。

### 理解ReST的指导原则

ReST有四个指导原则。根据标准，所有ReSTful接口都必须提供遵循这些原则的接口。在现实世界中，是否符合标准还有待讨论。以下是这些原则：

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_785_0.png)

- **资源标识：** 单个资源（例如数据项）在请求中被标识（例如，在基于Web的ReST系统中使用URI）。资源本身在概念上与返回给客户端的表示形式是分开的。例如，服务器不会发送其数据库，而是可能发送一些HTML、XML或JSON，它们表示某些数据库记录，例如以法语表达并以UTF-8编码，具体取决于请求的细节和服务器实现。
- **通过表示操纵资源：** 当客户端持有资源的表示（包括附带的任何元数据）时，它就有足够的信息来修改或删除服务器上的资源，前提是它有权限这样做。
- **自描述消息：** 每条消息都包含足够的信息来描述如何处理该消息（例如，调用哪个解析器）。这方面的例子是使用Internet媒体类型（以前称为MIME类型）。仅凭媒体类型，客户端就必须知道如何处理其内容。如果需要查看消息内容才能理解它，那么该消息就不是自描述的。例如，仅仅使用“application/xml”媒体类型并不足以知道如何处理其内容，除非使用代码下载。
- **超媒体作为应用状态的引擎：** 如果客户端很可能想要访问相关资源，那么这些资源应该在返回的表示中被标识出来（例如，通过在其上下文中提供URI，如超文本链接）。这就创造了一个环境，使使用该服务的软件系统对数据存储方式的了解超过正常水平。

### 深入探讨ReST的细节

ReST作为一个概念与Web一样古老，但作为一种Web服务实现，它相当新——大约和SOAP一样新。ReST作为标准的最大实现就是Web本身。CGI就是基于ReST接口的。

对ReST接口的调用显然比SOAP调用小。真的。看看这两个例子：

ReST:

```
POST /Start.asmx HTTP/1.1
Host: localhost
Content-Type: text; charset=utf-8
http://mydomain.com/start.aspx?id=3
```

SOAP:

```
POST /Service1.asmx HTTP/1.1
Host: localhost
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
  <soap12:Body>
    <HelloWorld xmlns="http://tempuri.org/" />
  </soap12:Body>
</soap12:Envelope>
```

SOAP的XML有点碍事。

另一方面，SOAP有一系列安全特性。有一系列事务特性。有一系列附件特性。SOAP有很多特性。

ReST就没有那么多了。ReST只有四个特性：

- GET – 请求资源
- PUT – 上传资源
- POST – 提交数据
- DELETE – 删除资源

第七卷
第4章
使用ReST的服务
构建Web

```
List<Conference> conferencesAtLocation(int locationId);
}
```

这对我们有什么作用？它告诉运行时编译器，URI可以直接调用它。你可以通过查看测试客户端来检查绑定本身，如图4-1所示。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_788_0.png)

图4-1：
一个ReST绑定。

不过，这还不是全部。我们需要创建一个WebServiceHost。

### 以不同方式返回数据

WebServiceHost是一个ServiceHost类，它恰好能很好地处理ReST，因此我们用它来实现这一目的。实现方式有几种，就像WCF中一样。这些包括：

- 任何在机器上运行的.NET应用程序都可以作为宿主。Windows服务、控制台应用程序，甚至正在运行的WPF应用程序都可以承载服务。只要它能访问网络设备，就应该能工作。
- IIS可以承载应用程序，并且可以在代码中对其进行配置。这涉及在服务代码隐藏中使用WebServiceHost对象，并用特性修饰类以进行配置。
- 可以设置Web.config文件来定义端点。这是最简单的方法，也是我们在第3章中所采用的方法。如果以这种方式配置，向代码中添加其他端点就是一个直接的更改。

然而，WCF配置工具中没有用于ReST绑定的绑定，因此我们必须用另一种方式。只需按照以下步骤操作：

- 1. **打开服务的Web.Config。**
- 其中应该有我们在第3章中构建的SOAP服务的绑定信息。将其保留。
- 2. **在ServiceModel部分下添加自定义POX绑定的粗体代码。**
- 它是清单4-1中的第一个粗体代码。
- 3. **将服务信息添加到Service部分。它是清单4-1中的第二个粗体代码。**

### 清单4-1：ReST服务实现

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <compilation debug="true" targetFramework="4.0">
      <assemblies>
        <add assembly="System.Data.Entity, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </assemblies>
    </compilation>
  </system.web>
  <system.serviceModel>
    <bindings>
      <customBinding>
        <binding name="poxBinding">
          <textMessageEncoding messageVersion="None" />
          <httpTransport />
        </binding>
      </customBinding>
    </bindings>
    <services>
      <service name="SHARPSERVICE.Registration">
        <clear />
        <endpoint address="http://localhost" binding="basicHttpBinding" name="SharpHttp" contract="SHARPSERVICE.Iregistration" listenUriMode="Explicit">
          <identity>
            <certificateReference storeName="My" storeLocation="LocalMachine" x509FindType="FindBySubjectDistinguishedName" />
          </identity>
        </endpoint>
        <endpoint address="http://localhost" binding="wsDualHttpBinding" bindingConfiguration="" name="SharpDual" contract="SHARPSERVICE.Iregistration" />
      </service>
      <service name="SHARPSERVICE.Registration">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost" />
          </baseAddresses>
        </host>
```

