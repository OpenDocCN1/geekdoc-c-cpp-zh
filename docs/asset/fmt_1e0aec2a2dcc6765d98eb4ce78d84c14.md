
- Application Service Proxies Authentication, Profile, Roles — Enables you to log on or log off the Web browser using the JavaScript language without making a round trip to the server. The server authentication application service generates the `AuthenticationService` proxy class. The Role proxy class enables you to make a group of the users of Web services and treat each group as a single user through the JavaScript language, without making round trips to the server. The server roles application service generates the `RoleService` proxy class. This approach can be useful to grant or deny the access rights of resources on the server. The Profile proxy class enables clients to get information about the current user’s profile through the JavaScript language without making round trips to the server. The server profile application service generates the `ProfileService` class.

- Page Methods Proxy – Provides scripting infrastructure for the client script, which enables you to call static methods as if they are the methods of a Web service.

- Web Service Communication Layer – Enables clients to communicate with Web services on the server. This element is a library of client script types. The Web service communication layer consists of the following elements:

  - `WebRequest` – Provides the functionality to the client script to make a Web request

  - `WebRequestManager` – Manages the flow of requests when the `WebRequest` object issues two or more requests for Web services

  - `XmlHttpExecutor` – Uses the browser's XMLHTTP support to make asynchronous network requests

  - JSON Serialization – Provides the serialization of JavaScript objects into the JSON format

  - `XMLHttp` – Used to send HTTP request to the server and load the response

# ASP.NET AJAX Server Architecture for Web Services

The ASP.NET AJAX server consists of ASP.NET Web server controls and components that manage the user interface and execution flow of an application. It also manages serialization, validation, and control extensibility. There are also ASP.NET Web services that enable you to access ASP.NET application services for forms authentication, roles, and user profiles.

Figure 18.3 shows the ASP.NET AJAX server architecture of a Web service in which the elements that enable communication with client applications are included:

![](img/e073a4882197be4ab61103cbe0bcb394_960_0.png)

Figure 18.3: ASP.NET AJAX Server Architecture for Web Services

As shown in Figure 18.3, the elements of the ASP.NET AJAX server architecture are as follows:

- Custom Services WCF and ASMX – Provides the functionality to a Web service and returns suitable response to the client.

- Application Service Authentication, Profile, Roles – Enables you to log on or log off through the client JavaScript. The authentication service generates the Authentication proxy class. There is no need to instantiate the authentication service as it is always available to the user of the Web service. The Role service generates the roles information of the currently authenticated user accessed by the client's JavaScript of the role proxy class. The Profile service generates a profile proxy class to get and set the profile properties of the user associated with the current request.

- Page Methods – Enables a method in an ASP.NET page to be called as if it is a Web service method. This element must be defined in the page that performs the page method call.

- Web Service Communication Layer – Enables a server to communicate with the Web services. This element is a library of server script types. The Web service communication layer consists of the following elements:

  - XML Serialization – Performs SOAP requests and returns XML types from a JSON request in Web services.

  - **JSON 序列化** – 执行从通用 .NET Framework 类型到 JSON 格式及反向的自定义序列化和反序列化。

  - HTTP 处理程序 – 用于执行 `.aspx`、`.asmx` 和 `.soap` 文件。ASP.NET 也使用它来处理请求。HTTP 处理程序可以通过 `IHTTPHandler` 接口创建。

现在，让我们学习如何保护 Web 服务。

# 保护 Web 服务

如果要创建 Web 服务并将其托管在 Internet 上，则需要能够控制和调节对 Web 服务的访问。Web 服务请求和响应以 XML 文档形式发送，而这些文档采用文本格式。因此，您需要在此类传输过程中保护 Web 服务免受未经授权的访问。

您可以通过以下两种方式防止 Web 服务被未经授权访问：

- 使用加密和基于消息的安全性

- 使用针对 Web 服务的身份验证和访问控制

现在，让我们详细了解这些方法。

## 加密和基于消息的安全性

加密是对 Web 服务所包含的文本进行混淆的过程，以便只有预期用户才能借助密钥解密（将加密数据转换回其原始形式）。

基于消息的安全性允许您向任何人发送加密消息，而不必担心恶意用户对消息进行解密。您可以立即检测到消息中有人所做的任何修改，因为附加到消息的签名（私钥）会失效，然后您可以安全地丢弃该消息。这种类型的安全性通过在请求和响应两个级别对消息进行加密来工作。

## 针对 Web 服务的身份验证和访问控制

身份验证是根据用户提供的用户凭据来验证用户的过程。保护 Web 服务的一种方法是强制想要使用 Web 服务的用户以用户 ID 和密码的形式提供其凭据。如果用户未能提供，则拒绝其对 Web 服务的访问。

# 直接解决方案

## 创建 Web 服务

在查看创建 Web 服务需要执行的任务之前，让我们先了解创建 Web 服务时要考虑的事项。以下列表列举了几个值得注意的要点：

- 确保请求 Web 服务的 Web 应用程序与提供 Web 服务的 Web 服务器之间的通信是异步的。在异步通信中，Web 应用程序无需在 Web 服务器响应其请求之前停止其进程。

- 尽量减少 Web 应用程序为获取 Web 服务而需要向 Web 服务器发送的请求数量。您可以通过将 Web 服务的相似任务合并到单个方法中来实现这一点。例如，假设您想创建一个提供体育用品信息的 Web 服务。与其为每个用品的名称、价格和制造商创建单独的方法，不如创建一个在单个请求中提供用品完整信息的方法。随着获取 Web 服务所需请求数量的减少，传输信息的网络效率会提高。这是因为大量信息会一次性传输，而不是分成小块传输。

- 确保使用面向对象编程的概念创建 Web 服务。您可以通过向访问 Web 服务的 Web 应用程序抽象 Web 服务的实现细节，并使用继承和多态来创建 Web 服务，从而确保这一点。面向对象编程概念允许您重用代码来创建 Web 服务，并简化 Web 服务的设计。

- 尽量减少 Web 服务器响应 Web 应用程序请求所需的时间。您可以通过创建缓存，将 Web 应用程序发送到 Web 服务器的请求输出存储一段特定时间，从而减少 Web 服务器的响应时间。现在，当 Web 应用程序请求 Web 服务时，其请求可以从缓存中得到满足。这减少了从 Web 服务器获取请求结果所需的时间和处理的量。

现在，让我们继续介绍在 ASP.NET 中创建 Web 服务时需要执行的任务。这些任务包括：

1. 创建 Web 服务项目
2. 声明 Web 服务
3. 设置 `WebService` 特性
4. 为 Web 服务声明方法

### 创建 Web 服务项目

您可以使用“新建网站”对话框中间模板中找到的 Web 服务模板来创建 Web 服务项目。

图 18.4 显示了“添加新项”对话框中的 Web 服务模板：

图 18.4：显示 Web 服务模板

从“添加新项”对话框中选择 Web 服务模板来创建 Web 服务。接下来，选择 Web 服务所需的语言，在“名称”文本框中输入 Web 服务的名称，然后点击“添加”按钮。

创建 Web 服务项目时，请注意它已经包含一个 Web 服务，其功能在代码隐藏文件的`HelloWorld`函数中定义。您可以通过右键单击`WebService.asmx`文件并从上下文菜单中选择“查看代码”选项来查看`WebService.asmx`文件。查看`WebService.asmx`文件的另一种方法是展开解决方案资源管理器中的`App_Code`节点。您可以根据需要修改`WebService.asmx`和`WebService`文件来创建新的 Web 服务。

### 声明 Web 服务

创建 Web 服务项目后的下一步是在`WebService.asmx`文件中声明 Web 服务。

Web 服务使用`@WebService`指令声明，该指令为 ASP.NET 的编译器和解析器提供编译和运行 Web 服务所需的信息。这包括有关 Web 服务以下特性的信息：

- `Class` — 指定实现 Web 服务的类的名称。
- `CodeBehind` — 指定包含 Web 服务实现的文件名。当包含`@WebService`指令的文件和`Bin`文件夹中的文件都不包含实现 Web 服务的类时，使用此特性。
- `Debug` — 指定是否在编译期间调试 Web 服务。如果`Debug`特性的值设置为`True`，则在编译期间对 Web 服务进行调试。
- `Language` — 指定编译 Web 服务所使用的语言。您可以将`Language`特性设置为 .NET 支持的任何语言，例如 VB、C# 或 jscript。

`@WebService`指令的语法是：

```
<%@ webservice attribute="value" ... %>
```

在使用这些特性声明 Web 服务之前，您需要确定包含 Web 服务实现的类是与包含`@WebService`指令的程序集位于同一程序集中，还是位于`Bin`文件夹中的单独程序集中。您需要确定这一点，因为在这两种情况下 Web 服务的声明是不同的。

如果类与`@WebService`指令位于同一程序集，您只需在`Class`特性中指定类的名称。但是，如果类位于单独的程序集中，则除了类名之外，还需要在`Class`特性中指定该程序集的名称。现在，让我们考虑一个例子来更好地理解这个概念。

假设实现 Web 服务的类的名称是`Webserv`，并且它与包含`@WebService`指令的程序集位于同一程序集中。

您可以通过在 Visual Studio 2010 中的`Service.aspx`页面中编写以下单行代码来声明此 Web 服务：

```
<%@ webservice Language="C#" Class="webserv" %>
```

但是，如果`Webserv` Web 服务位于单独的程序集`Webserv_assembly`中，则需要在`Service.aspx`页面中编写以下单行代码，才能在 Visual Studio 2010 中声明 Web 服务：

```
<%@ webservice Language="C#" Class=" WebServ,WebServ_assembly" %>
```

到目前为止，我们已经学习了如何使用`@WebService`指令声明 Web 服务。现在，我们来看另一个指令`@Assembly`。我们需要理解这个指令，因为在某些情况下，声明 Web 服务时也需要使用它。我们首先查看这些情况，然后探讨此指令的特性。

假设您希望 Web 服务使用一些包含预定义接口和类的程序集。这些接口和类既可以是用户定义的，也可以是系统定义的。如果这些程序集与`@WebService`指令位于同一程序集，或位于包含您网站的 Web 应用程序的`Bin`文件夹中，则它们会自动链接到您的 Web 服务。然而，情况并非总是如此。因此，在这种情况下，您需要使用`@Assembly`指令将这些程序集显式链接到 Web 服务。

`@Assembly`指令在 Web 服务编译时将程序集与 Web 服务关联起来。这允许 Web 服务使用该程序集中定义的类和接口。要使用`@Assembly`指令将程序集与 Web 服务关联，您需要在其`Name`特性中指定程序集的名称。设置`Name`特性时，您不需要指定程序集的扩展名。设置`Name`特性的语法是：

```
<%@ Assembly Name="assemblyname" %>
```

`@Assembly`指令还允许您在 Web 服务中包含程序集之外的代码文件。例如，您可以使用`@Assembly`指令在 Web 服务中包含 C# 代码文件。您可以通过在`@Assembly`指令的`Src`特性中指定文件路径来实现。使用`Src`特性的语法是：

```
<%@ Assembly Src="pathname" %>
```

### 设置 WebService 特性

`WebService`特性用于提供有关 Web 服务的附加信息，例如 Web 服务的功能。但是，在 Web 服务中使用`WebService`特性并非强制要求。

您也可以使用`WebService`特性为 Web 服务设置默认命名空间`http://tempuri.org`。但是，为了将您的 Web 服务与 Internet 上可用的其他 Web 服务区分开来，您应该在发布 Web 服务时更改默认命名空间。这允许用户唯一地识别他们的 Web 服务。要设置`WebService`特性，您需要将其应用于实现 Web 服务的类。使用`WebService`特性的语法是：
