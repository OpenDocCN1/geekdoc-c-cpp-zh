

## ASP.NET Web Services

7) 构建一个基于 Windows 或 Web 的项目来消费该 Web 服务，并在 GUI 上获取并显示所需信息。
8) 将我们的 ASP.NET Web 项目文件存储在安全的位置。

在本章中，我们将尝试开发以下项目，以说明 Web 服务的构建和实现过程：

- 构建一个专业的 ASP.NET Web 服务项目，访问 SQL Server 数据库以获取 Faculty（教师）表所需的信息。
- 构建客户端应用程序，提供 GUI 来消费 Web 服务。
- 构建一个专业的 ASP.NET Web 服务项目，向 SQL Server 数据库中的 Faculty 表中插入新信息。
- 构建一个专业的 ASP.NET Web 服务项目，对 SQL Server 数据库中的 Faculty 表进行信息更新和删除操作。
- 构建一个专业的 ASP.NET Web 服务项目，访问 SQL Server 数据库以获取 Course（课程）表所需信息。
- 构建一个专业的 ASP.NET Web 服务项目，向 SQL Server 数据库中的 Course 表中插入新信息。
- 构建一个专业的 ASP.NET Web 服务项目，对 SQL Server 数据库中的 Course 表进行信息更新和删除操作。
- 构建客户端应用程序，提供 GUI 来消费 Web 服务。

基于上述讨论的项目，我们可以开始构建我们的第一个 Web 服务项目 WebServiceSelect Project。

## 9.3 访问 SQL SERVER 数据库的 ASP.NET 服务项目

创建一个新的 ASP.NET Web 服务项目，请执行以下操作：

1) 打开 Windows 资源管理器或文件管理器，在 C 根驱动下创建一个名为 `Chapter 9` 的新文件夹。
2) 打开 Visual Studio.NET，并到 File | New | New | Project 项目。
3) 在打开的 New Project 向向中，在 Search for templates 框中找到 `WCF Service`，或者滚动到顶部找到并定位我们所需的 WCF 模板。搜索结果如图 9.4 所示。
4) 确保从 Templates 列表中带有 C# 图标的 **WCF Service Application**（如图 9.4 所示），我们需要创建以便托管在 IIS 中的我们的 Web 服务项目。然后点击 Next。
5) 在 ProjectName 框中输入 `WebSelectProject`，在 name 框中输入 `WebServiceSelection`。在 Location 框中输入或选择 `C:\Chapter 9`，如图 9.5 所示。
6) 点击 Create 按钮创建此新的 Web 服务项目。

### 9.3.1 新 Web 服务项目中创建的文件和项目

创建此新的 WCF Web 服务项目后，Solution Explorer 窗口会出现四个项目，如图 9.6 所示。这些组件包括：

1) 附加连接服务文件 (Connected Services)
2) 服务合约文件 (IServiceervice1.cs)。
3) 服务实现文件 (Service1.svc)。
4) Web 配置文件 (Web.config)。

## 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_548_0.png)

图 9.4 WCF 组件的搜索结果。

![](img/d59a47501d0a20fc0460a49c469c6fb7_548_1.png)

图 9.5 创建新的 WCF Web 服务项目。

## ASP.NET Web Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_549_0.png)

**图 9.6** WCF Web 服务项目的新项。

如前述节所示，文件 2 和 3 用于提供一些默认功能以获取某些系统数据和进行操作。
我们可以向默认服务 IService1.cs 添加操作操作或方法来构建我们的项目。
但在这里，我们希望以自定义的方式通过自己的后代码页面构建 Web 服务，因此需要执行以下操作以向我们的项目添加新的 Web 主服务：

1) 在 Solution Explorer 窗口中右键点击我们的新 **WebServiceSelect Project** 并选择 **Add | Item**。
2) 在 **New Item** 向导中，从 Template 列表中选择 **Web Service (ASMX)**。
3) 在 **Name** 框中输入 `WebServiceSelect.asmx`。
4) 点击 **Add** 完成此项添加操作。

修改后的 Web 服务项目如图 9.7 所示。
Web 服务文件 **WebServiceSelect.asmx** 是一个后代码页面，我们在此处为 Web 服务创建并开发代码。该页面包含一个派自基类 **WebService** 的默认类。该类定义了一个默认 Web 方法 **HelloWorld**，它是一个占位符，我们可以根据 Web 服务项目的需求将其替换为我们的操作或方法。此文件还用于显示有关 Web 服务方法的信息以及访问 Web 的 WSDL 信息。
配置文件 **Web.config** 用于为我们的新 Web 服务项目设置配置，例如各种 Web 主体的命名空间、数据组件和 Web 服务的连接字符串以及 Windows 身份验证。所有这些组件都会自动创建并添加到我们的新项目中。重要的是，文件 **WebServiceSelect.asmx** 设计用于自动创建可扩展的 WSDL 方法、序列化和反序列化参数，并为应用程序中的消息拦截提供钩。但当从文件系统创建并打开新的 Web 服务项目时，它仅包含一个编译指令。
双击后代码页面 **WebServiceSelect.asmx** 打开如图 9.8 所示的文件，让我们仔细查看此页面中的代码。

使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_550_0.png)

**图 9.7** 修改后的 Web 项目。

| WebServerSelect Project | HelloWorld() |
|--- |--- |
| A using System; using System.Collections.Generic; using System.Linq; using System.Web; using System.Web.Services; namespace WebServerSelectProject B // <summary> // Summary description for WebServerSelect // </summary> [WebServiceBinding(Namespace="http://tempuri.org/")] [ServiceContract(ServiceInterface=typeof(IBasicProfile1))] CD [ComponentModel(Toolbox=false)] // To allow this Service to be called from script, using ASP.NET AJAX, uncomment the following line: // // [System.Web.Services.ScriptService] E public class WebServerSelect : System.Web.Services.WebServiceSelect F [WebMethod] public string HelloWorld() { return "Hello World"; } } | |

**图 9.8** WebServerSelect.asmx 的默认代码。

A. 首先导入包含 Web 服务相关的命名空间，以便访问和使用这些组件来构建我们的 Web 服务。关于这些命名空间及其功能的详细描述如图 9.9 所示。
B. 在此部分定义了一些 WebAttribute 属性。通常，WebAttribute 属性用于识别部署的 Web 服务的附加信息。namespace 属性就是一个示例。正如我们在上一节讨论的，我们需要使用

## ASP.NET Web Services

| 空间 | 功能 |
| --- | --- |
| using System | 允许在项目中使用 System 库。它提供了一些常用的类和函数，如 Console 或 |
| using System.Collections.Generic | 定义泛型集合的接口和类，比非泛型提供了更好的类型安全性能。 |
| using System.Web | 包含浏览器通信的接口和类。 |
| using System.Web.Services | 允许使用 ASP.NET 和 XML 创建 XML 服务。 |

## 9.9 服务命名空间

当此项目被修改时的实际命名空间。

C. 此 Web 服务绑定表示当前 Web 服务符合一个接口，在该接口中定义了一组具体操作。

D. 这表示工具箱项的基类。

E. 我们的 Web 服务命名空间 WebSelect 是派自父类 WebService 的子类。

F. HelloWorld 方法被定义为全局函数，当返回给客户端时，该函数返回字符串 "Hello World"。


