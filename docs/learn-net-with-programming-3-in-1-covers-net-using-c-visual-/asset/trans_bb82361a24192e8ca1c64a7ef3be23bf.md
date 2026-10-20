
该方法将指定的字符串值写入标准输出流。如果 value 为 null 引用，则不向标准输出流写入任何内容。请考虑以下代码以作说明。

```
Public class formatconverter
{
    Public static void Main(string[] args)
    {
        String lineinput;
        While((lineinput = Console.readline() )!= null)
        {
            Bool isfirstfield = true;
            Foreach(string item in fields)
            {
                If (isfirstfield)
                Isfirstfield = false;
                Else
                Console.Write(',');
```
```
Try
{
Console.Write(Convert.tobyte(Convert.toboolean(item)))
;
}
Catch(formatexception)
{
Console.Write(item);
}
}
Console.writeline();
}
}
}
```

## 3.6 .NET 程序集

程序集是 .Net Framework 应用程序的基本构建块。它本质上是可以由 CLR 执行的已编译代码。程序集是类型和资源的集合，这些类型和资源被构建为协同工作并形成一个逻辑功能单元。程序集可以是 DLL 或 exe，具体取决于我们选择的项目。

程序集基本上有以下两种类型：

- 1. 私有程序集
- 2. 共享程序集

### 1. 私有程序集

它是仅供单个应用程序使用的程序集。假设我们有一个引用了 DLL 的项目，那么当我们构建该项目时，该 DLL 会被复制到我们项目的 bin 文件夹中。该 DLL 就成为我们项目中的私有程序集。通常，为特定项目准备的 DLL 就是私有程序集。

### 2. 共享程序集

可以在多个项目中使用的程序集称为共享程序集。共享程序集通常安装在 GAC 中。安装在 GAC 中的程序集可供该机器上的所有 .Net 应用程序使用。

然而，.Net 中还有另外两种程序集：卫星程序集和共享程序集。

## 3.7 GAC（全局程序集缓存）

### 使用全局程序集缓存（GAC）部署

如果要安装的组件将被同一台机器上的多个应用程序使用，或者需要在单台计算机上运行同一程序集的多个版本，则将应用程序组件安装到全局程序集缓存（GAC）中会很有用。默认情况下，当您安装 Ultimate UI for ASP.NET 工具集时，控件程序集将安装到 GAC 中。如果您希望将应用程序中的 Infragistics 组件部署到客户端计算机的 GAC 中，有三种主要方法。

### 使用 Gacutil.exe 向 GAC 添加组件

Gacutil.exe 工具是一个命令行实用工具，作为基础 .NET 框架的一部分安装，可用于向 GAC 添加应用程序组件或从 GAC 移除应用程序组件。Gacutil.exe 工具位于 .NET Framework 安装目录中。其默认位置为：

```
C:\Windows\Microsoft.NET\Framework\v4.0.30319.
```

要使用 Gacutil.exe 工具：

打开 Visual Studio 命令提示符

（开始 > 程序 > Microsoft Visual Studio .NET 2005 > Visual Studio .NET 工具 > Visual Studio .NET 2005 命令提示符）

输入 Gacutil.exe 命令。下面一行演示如何从名为 myapplication 的应用程序文件夹将 Infragistics webchart 组件添加到 GAC。

```
Gacutil -i
```

C:\Projects\myapplication\Infragistics4.webui.ultrawebchart.v21.2.dll

Gacutil.exe 命令行包含多条命令，允许您指定希望该工具执行的操作。以下列表说明了可用的命令：

- - /i - 将程序集安装到 GAC
- - /il - 将一个或多个程序集安装到 GAC
- - /u - 从 GAC 卸载程序集
- - /ul - 从 GAC 卸载一个或多个程序集
- - /ungen - 卸载通过 NGEN 实用程序安装的本机映像
- - /l - 列出按 <assembly_name> 筛选的 GAC
- - /lr - 列出带有所有跟踪引用的 GAC
- - /cdl - 删除下载缓存的内容
- - /ldl - 列出下载缓存的内容

Gacutil.exe 还允许在命令行上指定多个选项：

- - /r - 指定要安装或卸载的跟踪引用
- - /f - 强制重新安装程序集
- - /nologo - 禁止显示徽标横幅

```
<%@ Application Language="C#" %>
<script runat="server">

Void Application_Start(object sender, eventargs e)
{
    // Code that runs on application startup
}

Void Application_End(object sender, eventargs e)
{
    // Code that runs on application shutdown
}

Void Application_Error(object sender, eventargs e)
{
    // Code that runs when an unhandled error occurs
}

Void Session_Start(object sender, eventargs e)
{
    // Code that runs when a new session is started
}
```

页面被发布到服务器。如果用户在 Web 应用程序中输入信息，这些信息可能会在浏览器的往返过程中丢失（MSDN）。

用一句话来说，状态管理维护并存储任何用户的信息，直到用户会话结束。与“ASP.NET 中的状态管理概念”一样，ASP.NET 中提供了两种类型的状态管理技术。

### 服务器端会话

会话是维护状态的一种非常重要的技术。通常，会话用于存储信息和标识。服务器使用 Sessionid 存储信息。

### 设置用户会话

```
Protected void btnsubmit_Click(object sender, eventargs e)
{
    Session["username"] = txtname.Text;
    Response.Redirect("Home.aspx");
}
```

### 会话事件

会话事件可以在项目的 Global.asax 文件中看到。

有两种类型的会话事件：

### Session_Start

每次新用户在没有会话 ID 的情况下发出请求时，都会引发 Session_Start 事件。

```
Void Session_Start(object sender, eventargs e)
{
    Session["master"] = "~/Master.master";
}
```

### Session_End

当用户或超时通过使用 Session end 方法结束会话时，将引发 Session_End 事件。

```
Void Session_End(object sender, eventargs e)
{
    Response.Write("Session_End");
}
```

在 ASP.NET 中，会话通过以下四种方式进行存储。

### Inproc 模式

这是默认的会话模式，值存储在 Web 服务器内存（IIS）中。在这种模式下，会话值随服务器启动而存储，并在服务器重启时结束。

### State Server 模式

在此模式下，会话数据存储在独立的服务器中。

### SQL Server 模式

在此模式下，会话存储在数据库中。这是一种安全模式。

### 自定义模式

通常情况下，会话数据存储在 inproc、SQL Server、State Server 等中。如果您使用其他新技术来存储会话数据，那么请使用 ASP.NET 提供的方式。

### 应用程序

应用程序状态是一种服务器端管理状态。它也称为应用程序级状态管理。在这种状态下，主要将用户活动存储在服务器内存中，并将应用程序事件存储在 Global.asax 文件中。

ASP.NET 中有三种类型的应用程序。

### Application_Start

此事件随域启动而开始。

```
Void Application_Start(object sender, eventargs e)
{
	Application["appstartmessage"] = "Welcome to csharp Corner Developer Community";
}
```

### Application_Error

在此节中管理未处理的异常错误。

```
Void Application_Error(object sender, eventargs e)
{
// Write an unhandled error code exception
}
```

### Application_End

此事件结束于域结束或 IIS 重启时。

```
Void Application_End(object sender, eventargs e)
{
Application["appendmessage"] = "Application Closed";
}
```

### 缓存

缓存存储在服务器端。它实现了页面缓存和数据缓存。缓存用于设置过期策略。

```
Response.Cache.setexpiretime(datetime.Now.adddays(1 ));
```

```
Response.Cookies["cookiename"].Value = "Test Cookies";
```

### 控件状态

控件状态技术是为了维护数据正常工作而开发的。我们可以使用视图状态，但假设用户禁用了视图状态，控件将无法按预期工作。为了获得控件的预期结果，我们必须使用控件状态。在应用程序中，Viewstate 默认为 true。有时我们需要使用自定义控件来正确管理应用程序。

```
If (!IsPostback)
{
    Lblmsg1.Text = "Welcome to C# corner";
    Lblmsg2.Text = "Welcome to C# corner community";
}
```

当在 Postback 事件上显示两条消息时，则通过使用自定义控件状态来控制显示哪一条。

## 3.10 隐藏字段

隐藏字段用于在客户端存储值。隐藏字段不会显示在浏览器中，但在请求时会起作用。

```
If (hiddenfield1.Value != null)
```

