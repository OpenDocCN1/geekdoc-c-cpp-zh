
```
        <wsdl:input name="nmtoken"? message="qname">?

            <wsdl:documentation .... /> ?

        </wsdl:input>

        <wsdl:output name="nmtoken"? message="qname">?

            <wsdl:documentation .... /> ?

        </wsdl:output>

        <wsdl:fault name="nmtoken" message="qname"> *

            <wsdl:documentation .... /> ?

        </wsdl:fault>

    </wsdl:operation>

</wsdl:portType>

<wsdl:binding name="nmtoken" type="qname">*

    <wsdl:documentation .... />?

    <!-- extensibility element --> *

    <wsdl:operation name="nmtoken">*

        <wsdl:documentation .... /> ?

        <!-- extensibility element --> *

        <wsdl:input> ?

            <wsdl:documentation .... /> ?

            <!-- extensibility element -->

        </wsdl:input>

        <wsdl:output> ?

            <wsdl:documentation .... /> ?

            <!-- extensibility element --> *

        </wsdl:output>

        <wsdl:fault name="nmtoken"> *

            <wsdl:documentation .... /> ?

            <!-- extensibility element --> *

        </wsdl:fault>

    </wsdl:operation>

</wsdl:binding>

<wsdl:service name="nmtoken"> *

    <wsdl:documentation .... />?>

    <wsdl:port name="nmtoken" binding="qname"> *

        <wsdl:documentation .... /> ?

        <!-- extensibility element -->

    </wsdl:port>

    <!-- extensibility element -->

</wsdl:service>

<!-- extensibility element --> *

</wsdl:definitions>
```

# Web 服务线路格式

Web 服务线路格式提供了一个接口，用于通过协议（如 `HTTP-GET` 和 `HTTP-POST`）在 Web 服务与其用户之间传输数据。Web 服务可以使用任何远程过程调用（RPC）协议（如 `DCOM` 或公共对象请求代理体系结构（`CORBA`））来传输数据。然而，不建议使用这类协议来创建普遍可用的 Web 服务。因此，您需要使用常用协议（如超文本传输协议（`HTTP`）和 `SOAP`）在 Web 服务与其用户之间传输数据。

表 18.2 列出了 Web 服务用于传输数据的常见协议：

| 表 18.2：用于数据传输的 Web 服务协议 |
| 协议名称 | 描述 |
| `HTTP-GET` | 创建名称/值对的查询字符串，例如 `name=joe`、`city=Chicago`，并将其附加到服务器上请求脚本的统一资源定位符（URL）后 |
| `HTTP-POST` | 在 HTTP 请求消息的正文中传递名称/值对 |
| `SOAP` | 在分散、分布式的环境中交换信息 |
| 多用途互联网邮件扩展（`MIME`） | 定义复杂消息体（例如包含嵌入图形或音频片段的消息）的标准表示 |

表 18.2 中列出的协议用于调用 Web 服务的 Web 方法。Web 服务协议的选择决定了方法的参数类型及其返回类型。

现在让我们详细探讨一些重要协议。

## HTTP-GET 和 HTTP-POST

尽管您可能了解 Web 服务用于通过网络传输数据的 `HTTP-GET` 和 `HTTP-POST` 协议，但您必须认识到，这两种数据传输方式不够丰富，无法表示复杂的结构或类。在使用 Web 方法时，您只能将 `HTTP-GET` 和 `HTTP-POST` 方法用于表 18.3 中列出的数据类型：

| 表 18.3：HTTP-GET 和 HTTP-POST 协议支持的数据类型 |
| 数据类型 | 描述 |
| 枚举 | 支持传输 `.NET System.Enum` 类型，前提是它们被表示为静态常量字符串。 |
| 数组 | 将数组创建为基元类型。 |
| 字符串 | 指公共语言运行时（`CLR`）基元（如 `Int16`、`Int32`、`Int64`、`Boolean`、`Single`、`Double` 和 `Decimal`）的字符串表示形式。`HTTP-GET` 和 `HTTP-POST` 将所有数值数据作为字符串标记进行传输。 |

默认情况下，`HTTP-GET` 和 `HTTP-POST` 绑定不用于远程 Web 服务调用。但是，启用 `HTTP-POST` 以允许计算机调用本地 Web 服务。这些设置是在 `machine.config` 文件中使用 `<protocol>` 元素建立的。清单 18.3 显示了 `machine.config` 文件的部分代码：

### 清单 18.3：machine.config 文件的部分代码

```
<!-- In the machine.config file! -->
<webServices>
<protocols>
<add name="HttpSoap1.2"/>
<add name="HttpSoap"/>
<add name="Documentation"/>
<!-- Http GET and POST are disabled! -->
<!--<add name="HttpPost"/>-->
<!--<add name="HttpGet"/>-->
<!--Used by the web service test page-->
<add name="HttpPostLocalhost"/>
</protocols>
</webServices>
```

您可以通过在本地 `web.config` 文件中添加 `HttpPost` 和 `HttpGet` 名称来为 Web 服务启用 `HTTP-GET` 和 `HTTP-POST` 协议，如清单 18.4 所示：

### 清单 18.4：在本地 web.config 文件中添加 HttpPost 和 HttpGet 名称

```
<configuration>
  <system.web>
    <webServices>
      <protocols>
        <add name="HttpPost" />
        <add name="HttpGet" />
      </protocols>
    </webServices>
  </system.web>
</configuration>
```

使用 `HTTP-GET` 和 `HTTP-POST` 协议时，您无法构建将复杂类型（如 `ADO.NET DataSet` 或结构类型）作为参数或返回值的 Web 方法。对于简单的 Web 服务，这种限制或许可以接受。但是，如果您想构建更复杂精细的 Web 服务，可以使用 `SOAP` 绑定。

## 简单对象访问协议

`SOAP` 是 Web 服务中的关键元素之一，是一种用于消息传递的协议。它完全基于 `XML`。

`SOAP` 规范由 `W3C` 标准化，并且被大多数开发 Web 服务的公司所使用。

`SOAP` 为消息提供了一套完整的规则，称为 `SOAP` 信封，以及针对数据编码、消息处理、消息绑定到其他协议（如 `HTTP`）等问题的规则。使用 `SOAP` 消息的一大优点是它不受任何特定协议的限制。然而，`HTTP` 协议最常用，因为它不限于任何一种操作系统。

`SOAP` 消息是一个简单的 `XML` 文档，它始终包含必需的 `envelope` 和 `body` 元素，并且可以包含一些可选元素，例如 `<Header>` 和 `<Fault>`。清单 18.5 显示了 `SOAP` 消息的语法：

### 清单 18.5：SOAP 消息的语法

```
<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2001/12/soap-envelope"
soap:encodingStyle="http://www.w3.org/2001/12/soap-encoding">
  <soap:Header>
    ...
  </soap:Header>
  <soap:Body>
    ...
    <soap:Fault>
      ...
    </soap:Fault>
  </soap:Body>
</soap:Envelope>
```

如前所述，`envelope` 和 `body` 元素在任何 `SOAP` 消息中始终是必需的。以下是这两个元素的语法：

```
<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2001/12/soap-envelope"
soap:encodingStyle="http://www.w3.org/2001/12/soap-encoding">
...
```

消息信息位于 `<body>` 元素中，如清单 18.6 所示：

### 清单 18.6：<body> 元素内的消息信息

```
...
</soap:Envelope>
<?xml version="1.0"?>
<soap:Envelope
xmlns:soap="http://www.w3.org/2001/12/soap-envelope"
soap:encodingStyle="http://www.w3.org/2001/12/soap-encoding">
<soap:Body>
<m:GetName xmlns:m="http://www.mydomain.com/NamesData">
<m:record>1</m:record>
</m:GetName>
</soap:Body>
</soap:Envelope>
```

了解 `ASP.NET` Web 服务的基础结构之后，接下来让我们看看 `ASP.NET` Web 服务的代码模型。

## ASP.NET Web 服务的代码模型

Web 服务包含两个部分：Web 服务的入口点以及用于实现 Web 服务功能的代码。在 `ASP.NET` 中，任何 Web 服务的入口点都是扩展名为 `.asmx` 的文本文件。该文件引用预编译程序集中的代码、代码隐藏文件中的代码或 `.asmx` 文件本身的代码。

`WebService` 指令确定了 Web 服务实现的入口点，它位于 `.asmx` 文件的顶部。当您通过 `ASP.NET` Web Service 模板创建 Web 服务时，会找到一个代码隐藏文件（如 `Service.cs`）来编写 Web 服务的代码。

`ASP.NET` Web 服务的代码模型由以下两部分组成：

- `WebService` 指令
- 代码隐藏文件

现在，让我们详细讨论这两个部分。

### WebService 指令

`WebService` 指令定义了由 `ASP.NET` 编译器和解析器使用的 Web 服务特定属性，例如 `Namespace` 和 `Description` 属性。`WebService` 指令的属性如下：

- **语言** – 通知 `ASP.NET` 编译器编写类所用的编程语言，例如 `C#`、`VB` 或 `JS`。
- **类** – 通知 `ASP.NET` 编译器要作为 Web 服务公开的类名。Web 服务应用程序可以包含多个类，但并非所有类都属于该 Web 服务；因此，您必须告知 `ASP.NET` 编译器要公开哪些类。

例如，

```
<%@ WebService Language="C#" Class="MyFirstWebservice" %>
```

在上述示例中，类是 `MyFirstWebservice`。

### 代码隐藏文件

在 Web 服务编程的代码隐藏方法中，`WebService` 指令与支持源代码分离。`WebService` 指令放在扩展名为 `.asmx` 的文件中，而支持源代码放在扩展名为 `.asmx.cs` 的文件中。使用 Web 服务之前，必须将源代码文件编译成程序集，并放在特定 Web 服务的 `\bin` 目录中，这会在您生成或编译项目时自动完成。

当首次向 Web 服务发送请求时，`ASP.NET` 会访问 `.asmx` 文件并读取 `WebService` 指令，以获取包含支持逻辑的类文件的名称。然后，`ASP.NET` 会在 Web 服务项目的 `\bin` 目录中的程序集内搜索已编译的类，例如 `MyFirstWebservice`。如果 Web 服务项目的 `\bin` 文件夹中有不止一个程序集，则 `ASP.NET` 会检查每个程序集，直到找到适当的类。

将编译后的源代码存储在代码隐藏文件中的主要优点是，恶意用户无法访问代码，因为代码未存储在 Web 服务器中。声明代码隐藏属性的语法是：

```
<%@ WebService Language="c#" CodeBehind="~/App_Code/MyFirstWebService.cs" Class="MyFirstWebservice" %>
```

让我们讨论代码隐藏文件的各种属性。

### The WebService Attribute

`WebService` 属性是 `System.Web.Services` 命名空间的成员，并传达有关 Web 服务的信息，例如 Web 服务的名称、描述和命名空间。`WebService` 属性由以下三个属性组成：

- `Name` – 在 `WSDL` 文档中定义 Web 服务的类名。当代理使用 `WSDL` 文档并构建代理类时，生成的类的名称对应于 Web 服务的名称值。此属性允许覆盖默认值。
- `Description` – 提供有关 Web 服务的类，例如 `MyFirstWebservice` 所执行功能的简要描述。
- `Namespace` – 为 Web 服务设置 `XML` 命名空间，通常为 `URL`。使用 `URL` 设置 Web 服务的 `XML` 命名空间的原因是 `URL` 总是唯一的。

例如，

```
[WebService(Name="CalculateInterest",Description="This class contains methods for calculating Simple Interest as well as Compound Interest and population of DataSet with the calculated Amount.", Namespace="http://www.InterestRate.com/")]
```

在前面的示例中，`Name` 属性的值定义如下：

```
Name="CalculateInterest"
```

`Description` 属性的值定义如下：

```
Description="This class contains methods for calculating Simple Interest as well as Compound Interest and population of DataSet with the calculated Amount."
```

`Namespace` 属性的值定义如下：

```
Namespace="http://www.InterestRate.com/"
```

### The System.Web.Services.WebService Class

Web 服务继承自 `System.Web.Services.WebService` 类。`WebService` 类定义了一些常见的 `ASP.NET` 对象，例如 `Application`、`User`、`Session` 和 `Context`，以便您可以在 Web 服务中直接使用它们，而无需重新定义它们。

`WebService` 类的继承层次结构如下：

```
System.Object
System.ComponentModel.MarshalByValueComponent
System.Web.Services.WebService
```

### The WebMethod Attribute

Web 服务类可以包含一个或多个 `WebMethod` 属性，这些属性可通过 `HTTP` 协议访问。`WebMethod` 属性由以下六个属性组成：

- `CacheDuration` – 指定客户端发送的请求响应的时间（以秒为单位）。它应保存在系统的缓存中。默认情况下，缓存被禁用。通过将服务的响应放入缓存，可以提高 Web 服务的性能。例如，

```
[WebMethod(CacheDuration=30)]
```

在前面的示例中，`[WebMethod]` 属性的 `CacheDuration` 属性的值设置为 `30`。

- `BufferResponse` – 允许服务器存储 Web 服务生成的响应。整个响应存储后，响应将一次性传输给客户端。默认情况下，`BufferResponse` 属性设置为 `True`。如果将 `BufferResponse` 属性设置为 `False`，则响应会在服务器上构建时传输给客户端。
- `Description` – 提供 `[WebMethod]` 属性的简要描述，此描述成为 `WSDL` 文档的一部分。
- `EnableSession` – 为 Web 方法启用会话状态。默认情况下，此属性设置为 `False`。
- `MessageName` – 在处理重载的 Web 方法时，标识类中的多态方法。
