
```
        }

        return (int)Session("SessionNumber");

    }

}
```

接下来，让我们来了解如何在 Web 服务中使用 ASP.NET AJAX。

## ASP.NET AJAX 与 Web 服务

你可以使用 AJAX 创建 AJAX 服务。Web 服务可以通过客户端脚本语言（如 JavaScript）访问。Web 服务通信层允许 Web 页面在服务器之间传输数据。该层使用 AJAX 调用 Web 服务。客户端与服务器之间的数据交换以 JavaScript 对象表示法 (`JSON`) 格式以异步模式进行。

ASP.NET AJAX 服务架构分类如下：

- 用于 Web 服务的 ASP.NET AJAX 客户端架构
- 用于 Web 服务的 ASP.NET AJAX 服务端架构

## Web 服务的 ASP.NET AJAX 客户端架构

浏览器使用代理类（`proxy classes`）来调用 Web 服务方法。代理类在 Web 页面加载时生成。客户端代理类代表 Web 暴露的消息。当用户调用 Web 服务时，客户端脚本会调用代理类的 Web 方法。这些调用通过 `XMLHttpRequest` 对象异步进行。在 ASP.NET AJAX Web 服务客户端架构中，你必须实现代理类，通过 Web 服务通信层中包含的库脚本来调用 Web 服务。使用以下方法调用 Web 服务：

- 使用 HTTP-Post 协议：包含一个正体，其中包含客户端浏览器发送到服务器的数据。请求包含要传输的数据。因此，每当数据传输超过 GET 请求的限制时，可以使用 POST 请求。传输从客户端开始，客户端将请求序列化为 `JSON` 格式并作为 POST 数据发送到服务器。当服务器接收请求时，它将数据格式反序列化为 `.NET Framework` 兼容的类型，然后对 Web 服务执行实际操作。作为响应，服务器序列化返回值并将其发送回客户端，客户端在处理时将值反序列化为 JavaScript 对象。

- 使用 HTTP-Get 协议：包含一个查询字符串，向服务器请求参数。GET 请求使用 `ScriptMethod` 特性调用 Web 服务的方法。传输的数据大小受浏览器允许的 URL 限制。

图 15.2 显示了用于 Web 服务的架构：

![](img/17af790174c8079)

图 15.2：Web 服务的架构

## Web 服务的 ASP.NET AJAX 服务端架构

ASP.NET AJAX 服务端包含管理用户界面的 ASP.NET 控件。它还管理序列化、验证和控件扩展。此外还有启用客户端的 Web 服务。图 15.3 显示了用于 Web 服务的架构：

![](img/17af790174c8079)

图 15.3：Web 服务的架构

## Web 服务安全性

如果你想创建一个 Web 服务并在互联网上托管它，你需要能够控制和监管对 Web 服务的访问。你可以通过以下两种方式防止 Web 服务被未经授权的访问：

- 使用加密和基于消息的安全
- 为 Web 服务使用身份验证和访问控制

# 第 15 章：ASP.NET Web 服务

现在，让我们详细学习这些方法。

## 加密与基于消息的安全

加密是对你的 Web 服务包含的文本进行扰乱的过程，使得只有预期的用户才能在密钥的帮助下对其解密（将加密数据转换回原始形式）。

基于消息的安全允许你向任何人发送加密消息，而无需担心恶意用户对消息进行解密。你可以立即检测到有人对消息进行了任何修改，因为附带在消息上的签名（私钥）会失效，然后你就可以安全地丢弃该消息。这种安全机制通过在请求和响应层级对消息进行加密来工作。

## Web 服务的身份验证与访问控制

身份验证验证用户提供的用户凭据的过程。保护 Web 服务的一种方法是强制要求使用 Web 服务的用户以用户 ID 和密码的形式提供其凭据。如果他们未能这样做，将被拒绝访问 Web 服务。

## 创建 Web 服务

在查看创建 Web 服务需要执行的任务之前，让我们先看看在创建 Web 服务时需要考虑的要点。以下列表列举了一些值得注意的点：

- 确保请求 Web 服务的 Web 应用程序与提供 Web 服务的 Web 服务器之间的通信是异步的。在异步通信中，Web 应用程序不需要等到 Web 服务器响应其请求之前停止其进程。

- 尽可能减少 Web 应用程序为获取 Web 服务向 Web 服务器发送的请求数量。你可以通过将 Web 服务的任务合并到单个方法中来实现。例如，假设你想创建一个提供运动项目信息的 Web 服务。与其为提供每个项目的名称、价格和制造商信息创建单独的方法，不如创建一个在单个请求中提供所有信息的方法。随着获取 Web 服务所需请求数量的减少，传输信息的网络开销随之增加。这是因为大量小数据块被一次性传输。

- 确保使用面向对象的编程概念创建 Web 服务。你可以通过从 Web 应用程序中抽象 Web 服务的实现细节，并使用继承和多态来创建 Web 服务来确保这一点。面向对象的编程概念允许你复用代码来创建 Web 服务并简化 Web 服务业务的设计。

- 尽可能缩短 Web 服务器响应 Web 应用程序请求的时间。可以通过对 Web 应用程序发送到 Web 服务器的请求输出进行一段时间的缓存来缩短 Web 服务器的响应时间。现在，当 Web 应用程序请求 Web 服务时，其请求将从缓存中获取。这减少了从 Web 服务器获取请求结果所需的时间和处理量。

现在，让我们转向在 ASP.NET 中创建 Web 服务时需要执行的任务。这些包括：

1. 创建 Web 服务项目
2. 声明 Web 服务
3. 设置 WebService 属性
4. 为 Web 服务声明方法

### 创建 Web 服务项目

你可以通过“添加项”（Add Item）对话框中间面板中的 Web 服务模板来创建 Web 服务项目。图 15.4 显示了“添加项”对话框中的 Web 服务模板：

第 15 章：ASP.NET Web 服务![](img/af790174c480761404624ae9b30b.png)

图 15.4：显示模板

从“添加项”框选择 Web 服务模板以创建 Web 服务。接下来，选择 Web 服务所需的语言，在文本框中输入 Web 服务的名称并点击“添加”。

当你创建一个服务项目时，注意它始终包含一个 Web 服务，其功能定义在后台代码（`code-behind`）中。你可以通过右键点击 `.asmx` 文件并从上下文菜单中选择“代码视图”（Code View）来查看 Web 服务。另一种查看 Web 服务的方法是扩展解决方案资源管理器中的 `App_Code` 节点。你可以根据需求修改 `.asmx` 文件。

### 声明 Web 服务

创建 Web 项目后的下一步是在 `.asmx` 文件中声明 Web 服务。Web 服务使用 `@WebService` 指令进行声明，该指令为 ASP.NET 编译器和解析器提供了编译和运行 Web 服务所需的信息。这包括关于 `WebService` 的以下属性的信息：

- Class（类）：指定实现 Web 服务的类。
- CodeBehind（后台代码）：指定包含 Web 服务实现的文件名。当包含 `@WebService` 指令的文件或 Bin 文件夹中的文件都不包含实现 Web 服务的类时，使用此属性。
- Debug（调试）：指定编译期间的 Web 服务。如果 `Debug` 属性的值设置为 True，则对 Web 服务进行调试。
- Language（语言）：指定编译 Web 服务的语言。你可以将 `Language` 属性设置为 .NET 支持的任何语言，如 VB 或 C#。

`@WebService` 指令的语法为：在使用这些属性声明服务之前，你需要确定包含 Web 服务实现的类是否存在于包含 `@WebService` 指令的同一个程序集中，还是在 Bin 文件夹中的单独程序集中。你需要确定这一点，因为两种情况下的 Web 服务声明有所不同。

### 立即解决方案

如果类与 `@WebService` 指令位于同一个程序集中，你只需要在 `Class` 属性中指定类名。然而，如果类位于单独的程序集中，你需要在 `Class` 属性中除了类名外还需要指定类所在的程序集名称。现在，让我们考虑一个例子来更好地理解这个概念。

假设实现 Web 服务的类名为 `Webserv`，它位于包含 `@WebService` 指令的同一个程序集中。你可以通过在 .asmx 页面中编写以下单行代码在 Visual Studio 2012 中声明此 Web 服务：

```xml
<WebService Language="C#" CodeBase="Webserv" />
```

然而，如果 `Webserv` Web 服务位于单独的程序集 `Webserv_assembly` 中，你需要在 .asmx 页面中编写以下单行代码以在 Visual Studio 2012 中声明 Web 服务：

```xml
<Assembly Language="C#" CodeBase="/App_Code/Webserv.cs" Class="Webserv" />
```

现在，我们学会了使用 `@WebService` 指令声明 Web 服务。现在，我们遇到了另一个指令：`@Assembly`。我们需要理解这个指令，因为在某些声明 Web 服务的情况下我们也需要使用它。我们首先查看这些情况，然后探索该指令的属性。

假设你想跨越包含预定义接口和类的程序集使用你的 Web 服务。这些接口和类可以是预定义的。如果这些程序集位于包含网站的 Web 应用程序的 Bin 文件夹，则它们通过 `WebService` 属性链接到服务。然而，并非总是如此。因此，在这种情况下，你不需要使用 `@Assembly` 指令显式地将它们链接到 Web 服务。

`@Assembly` 指令在编译 Web 服务时将程序集与 Web 服务关联。这允许 Web 服务使用另一个程序集中定义的类和接口。你需要使用 `@Assembly` 指令的 `Src` 属性指定程序集名称，以关联程序集。在设置 `Name` 属性时，不需要指定程序的扩展名。设置 `Name` 属性的语法为：

```xml
<Assembly Name="assemblyname" />
```

`@Assembly` 指令还允许在 Web 服务包含程序集以外的代码文件。例如，你可以通过在 `@Assembly` 指令的 `Src` 属性中指定文件路径来实现。`Src` 属性的语法为：

```xml
<Assembly src="pathname" />
```

### 设置 WebService 属性

`WebService` 属性用于提供有关 Web 服务的附加信息，例如 Web 服务的功能。然而，Web 服务并不使用 `WebService` 属性。

你还可以使用 `WebService` 属性为 Web 服务设置默认命名空间 `http://tempuri.org/`。然而，为了将你的 Web 服务与互联网上的其他 Web 服务区分开来，发布 Web 服务时应更改命名空间。这允许用户唯一标识你的 Web 服务。你需要使用实现 Web 服务的类来设置 `WebService` 属性。

### 为 Web 服务声明方法

你需要声明定义 Web 服务功能的方法来实现 Web 服务。Web 服务的方法应该能够通过互联网与 Web 应用程序交换数据，以便 Web 应用程序访问。你可以启用 Web 服务方法

# 第 15 章：ASP.NET Web 服务

通过将方法声明为公共 并在方法上应用 `WebMethod` 属性来与 Web 应用程序通信。

`WebMethod` 属性使 Web 服务能够与位于本地或远程机器上的 Web 应用程序通信。在 Web 服务方法中使用 `WebMethod` 属性的语法如下：

```
[WebMethod]
public returntype functionname()
```

到为止，我们已经学习了创建 Web 服务涉及的步骤。现在，让我们通过一个示例来实现此过程，来创建一个 Web 服务。

> 注意：
> 我们使用 ASP.NET 空白 站点来创建应用程序。

假设你想创建一个可以被其他应用程序用于计算单利的 Web 服务。为了实现这一点，创建一个名为 CalculateSimpleInterest 的 ASP.NET Web 应用程序。现在，按照以下步骤操作：

- 1. 创建实现 Web 服务的方法 `WebService.asmx`。在 `WebService.asmx` 文件的后置文件中添加如列表 15.11 所示的方法代码：

列表 15.11：`WebService.asmx` 文件的后置文件代码

```
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Services;
// <summary>
// webservice 的摘要描述
// </summary>
[webservice(Namespace="http://tempuri.org/", Is.Profiles.BasicProfile_1)]
// 要允许从脚本调用此 webservice（使用 ASP.NET AJAX），请取消下行的注释
[System.web.Script.Services.ScriptService]
public class webservice : System.web.Services.WebService
public webservice ()
{
// 如果使用设计组件，请取消下行的注释
// InitializeComponent();
}
[WebMethod]
public string helloWorld()
{
return "Hello world";
}
[WebMethod]
public double calculatesimpleInterest(double principal, double rate, int duration)
{
double SI;
SI = principal * rate * duration / 100;
return SI;
}
```
