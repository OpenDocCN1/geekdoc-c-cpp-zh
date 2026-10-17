
以下代码片段是 C# 中的一个简单 LINQ 示例：

```
var query = from s in Students where s.Gender = "M";
select s.Name;
```

执行给定查询时，它会返回所有男性学生的姓名。您可以使用以下代码片段中的代码打印此列表：

```
foreach(var name in query)
{
    Response.Write(name);
}
```

前面代码片段中给出的查询语法类似于 SQL 查询。需要注意的是，即使它看起来类似于 SQL，显示的 LINQ 查询也不是 SQL 语句。相反，它是纯粹的 C# 语言。虽然 LINQ 查询类似于 SQL，但它们并不局限于仅访问关系数据库。

LINQ 启用数据访问组件如下：

- `LINQ to ADO.NET` – 包括两个选项，`LINQ to SQL` 和 `LINQ to DataSet`。`LINQ to SQL` 选项用于将查询转换为 SQL 查询，然后针对 SQL Server 数据库中的表发出。`LINQ to DataSet` 选项用于在 `DataSet` 的内容上执行查询。
- `LINQ to Object` – 允许查询集合中的对象。
- `LINQ to XML` – 允许查询 XML 数据，包括创建和操作 XML 数据。

> NOTE
>
> LINQ 还为查询提供了其他运算符，例如 `OrderBy`、`GroupBy` 和 `Sum`。

现在，让我们探索 .NET Framework 4.0 的新功能。

# New Features of .NET Framework 4.0

`.NET Framework 4.0` 有助于提供一致的面向对象编程环境。此版本更安全，因为它包含改进的安全模型。`.NET Framework 4.0` 的一些新功能如下：

- 改进的应用程序兼容性和部署支持
- 动态语言运行时（DLR）
- 受管可扩展性框架（MEF）
- 并行计算
- 进程内并行执行
- 改进的安全模型
- 网络改进
- 改进的核心 ASP.NET 服务
- WPF 的改进
- 改进的实体框架
- WCF 和 WF 的集成

让我们详细了解它们。

## Improved Application Compatibility and Deployment Support

在早期版本 `.NET Framework` 中开发的应用程序在此版本中得到支持。这意味着 `.NET Framework` 的新版本甚至与在 `.NET Framework` 早期版本中开发的应用程序兼容。您可以通过在编译时指定 `.NET Framework` 的目标版本来运行在旧版本 `.NET Framework` 中开发的应用程序。您还可以通过在应用程序配置文件中使用 `<supportedRuntime>` 元素指定受支持的运行时来运行在旧版本 `.NET Framework` 中创建的应用程序。

`.NET Framework 4.0` 中引入的以下功能提供了改进的部署支持：

- `.NET Framework Client Profile` — 通过提供 Windows 窗体、控制台或 WPF 应用程序的快速部署来改进部署过程。
- 进程内并行执行 — 有助于加载和启动多个版本的 `.NET Framework`。组件对象模型（COM）组件随 `.NET Framework` 一起运行，它们是在其中开发的。

## Dynamic Language Runtime

`DLR` 功能在 `.NET Framework 4.0` 中引入，用于实现动态语言，例如 Python 和 Ruby。这意味着 `DLR` 是一个运行时环境，它向 `CLR` 添加服务以实现动态语言。

`DLR` 的目的不仅是使动态语言能够在 `.NET Framework` 上运行，还为其提供 `.NET` 互操作性的优势。已在 `.NET Framework` 中添加了新的 `System.Dynamic` 命名空间以支持 `DLR` 功能。`DLR` 的优势如下：

- 在静态类型语言（如 C# 和 Visual Basic（VB））中实现动态功能，以便这些语言也可以创建动态对象
- 启用静态类型语言和动态语言之间的互操作，以便在一个语言中实现的对象可以轻松地被其他语言使用
- 帮助开发人员专注于特定语言功能，因为开发人员不必创建代码生成器

图 1.9 显示了 `DLR` 架构：

![](img/e073a4882197be4ab61103cbe0bcb394_57_0.png)

图 1.9：显示 `DLR` 架构

As shown in Figure 1.9, `DLR` adds the following sets of services to `CLR` for supporting the dynamic languages:

- Expression trees – Allows you to define variable assignments and function loops
- Call site caching – Allows `DLR` to cache information about method calls so that in case of any subsequent calls to the method, the `DLR` can use the cache history information
- Dynamic object interoperability – Refers to the set of classes that can be used to create dynamic objects

The binder helps `DLR` to communicate with not only the `.NET Framework` but also with other infrastructure and services, such as Silverlight and Office. The binder informs the `DLR` about the language and how to perform operations in a call site by using expression trees.

## Managed Extensibility Framework

The Managed Extensibility Framework (`MEF`) is a new library included in the `.NET Framework 4.0` version to create lightweight and extensible applications. `MEF` also helps in reusing the extensions not only within but across the applications also. The `System.ComponentModel.Composition` namespace is included in `.NET Framework 4.0`, which provides classes that constitute the core of `MEF`.

Earlier, while creating an application that needed a plug-in model, you need to create the infrastructure of the application. In this method, the plug-ins created were application-specific and cannot be reused across multiple applications. The `MEF` library, however, provides extensions that can be reused in multiple applications. With the help of `MEF`, the application can not only locate the extension but also load it in the application.

## Parallel Computing

Parallel computing is a process in which a large problem is divided into small units and then these units are solved parallelly. Sometimes personal computers and workstations have two or three Central Processing Units (`CPUs`) that enable multiple threads to be executed simultaneously. In such a situation, a new programming model is provided by `.NET Framework 4.0` that allows the developers to develop multithreaded and asynchronous code. This new programming model is known as parallel computing, which is supported by new runtime, class library types, and diagnostic tools. In parallel computing, you need to distribute the code for execution across multiple processors. Note that to implement parallel computing, you need to import the `System.Threading.Tasks` namespace, which is introduced with the `.NET Framework 4.0` version.

## In-Process Side-by-Side Execution

The In-Process Side-by-Side Execution feature supports the loading and starting of multiple versions of `.NET Framework` by an application within the same process. For example, you can execute an application, which loads the components developed in `.NET Framework 3.0` and `.NET Framework 4.0` in the same process.

## Improved Security Model

A new and improved security model is introduced with `.NET Framework 4.0`. Many useful classes and services introduced in `CLR` and `.NET Framework` help the developers to write secure code and implement cryptography and role-based security. The following are the two major changes introduced in `.NET Framework 4.0` security system:

- There is no machine-wide security policy, although the user permissions system remains the same.
- The default enforcement mechanism is changed to security transparency.

## Networking Improvements

The following are the various networking improvements implemented in `.NET Framework 4.0`:

- Improvements in classes for Windows authentication, such as `System.Net.HttpWebRequest`, `System.Net.HttpListener`, `System.Net.Mail.SmtpClient`, and `System.Net.Security.NegotiateStream`
- Improvements in support for Network Address Translation (`NAT`) traversal using IPv6 and Teredo
- Introduction of new networking performance counters that provide information about `HttpWebRequest` objects
- Introduction of `AddRange` method in the `System.Net.HttpWebRequest` class
- Implementation of Secure Socket Layer (`SSL`) support for `System.Net.Mail.SmtpClient` class
- Improvement in support for mail headers in the `System.Net.Mail.MailMessage` class

## Improved Core ASP.NET Services

Along with the `.NET Framework`, the following features are introduced in ASP.NET to improve the core ASP.NET services:

- Introduction of the properties to set meta tags by using the `Page.MetaKeywords` and `Page.MetaDescription` page properties
- Improvements in working with browser capabilities by making it easier
- Introduction of ASP.NET routing with Web forms
- Introduction of the new ASP.NET Chart control
- Introduction of the new QueryExtender control, which provides filtering support for data source controls
- Implementation of more control over HTML code in the `FormView` and `ListView` controls

## Improvements in WPF

In `.NET Framework 4.0`, the following changes have been introduced in many areas of WPF, which includes controls, graphics, and XAML:

- Introduction of new controls, such as `DataGrid`, `Calendar`, and `DatePicker`
- Introduction of `VisualStateManager` class and supporting classes to define the appearance of a control according to its visual state
- Introduction of `UIElement`, `UIElement3D`, and `ContentElement` classes to expose the events that occur on a touch-enabled screen, when a user touches an element
- Introduction of changes related to text, such as new text rendering stack, the `SelectBrush` property to highlight a selected text, and the `CaretBrush` property to change the brush that paints the cursor
- Introduction of changes and improvements related to binding

## Improved Entity Framework

In `.NET Framework 4.0`, you need to do less amount of coding in Entity Framework. The new features introduced in Entity Framework are as follows:

- Creation of conceptual models in which the columns with foreign keys in the database correspond to entity types
- Introduction of new methods in the `System.Data.Objects` namespace so that the N-tier applications are developed easily
- Introduction of the `EntityDataSource` control support for the QueryExtender control
