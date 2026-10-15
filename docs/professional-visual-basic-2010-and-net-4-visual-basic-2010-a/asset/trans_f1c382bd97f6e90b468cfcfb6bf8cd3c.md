

```
' Code
End Class
Namespace MyChildNamespace
    Class MyClass2
        ' Code
    End Class
End Namespace
End Namespace
```

这是在你自定义命名空间内部引用其他命名空间时需要注意的另一个要点。请考虑以下示例：

```
Imports System
Imports System.Data
Imports System.Data.SqlClient
Imports System.IO
Namespace MyMetaNamespace1
    Class MyClass1
        ' Code
    End Class
End Namespace
Namespace MyMetaNamespace2
    Class MyClass2
        ' Code
    End Class
End Namespace
```

在此示例中，文件中引用了多个不同的命名空间。代码列表顶部引用的四个命名空间——System、System.Data 和 System.Data.SqlClient 命名空间引用——可供文件中开发的每个命名空间使用。这是因为这三个引用位于任何特定命名空间声明之外。然而，System.IO 命名空间引用并非如此。因为此引用是在 MyMetaNamespace2 命名空间内进行的，因此它对文件中的任何其他命名空间都不可用。

> 当你创建自己的命名空间时，Microsoft 建议你使用 CompanyName.TechnologyName 的约定——例如，Wrox.Books。这有助于确保所有库都以一致的方式组织。

有时当你使用自定义命名空间时，你可能会发现自己由于命名冲突而无法访问命名空间的特定分支。Visual Basic 包含 Global 关键字，可用作 .NET Framework 类库中可用的最外层根类。图 4-14 显示了使用 Global 关键字时类结构的外观图。

这意味着你可以进行如下指定

```
Global.System.String
```

或

```
Global.Wrox.System.Titles
```

## THE MY KEYWORD

My 关键字是一个新颖的概念，它在 .NET Framework 2.0 中引入，目的是让你快速访问你的应用程序、你的用户、你的资源、

![](img/d99870e80390742f93963da7be0b2e61_261_0.png)

FIGURE 4-14

计算机，或应用程序所在的网络。My 关键字被认为是一种快速拨号常用但复杂的资源的方式，你需要访问这些资源。使用 My 关键字，你可以快速访问各种各样的项目，例如用户详细信息或请求者浏览器的特定设置。

虽然 My 并不是真正意义上的命名空间，但你所做的 My 对象声明的工作方式与你习惯使用的 .NET 命名空间结构相同。为了举例说明，让我们先看看如何使用传统的命名空间结构获取用户的机器名称：

```
Environment.MachineName.ToString()
```

对于此示例，你只需使用 Environment 类并使用此命名空间来获取 MachineName 属性。以下显示了如何使用 My 关键字完成此相同任务：

```
My.Computer.Info.MachineName.ToString()
```

查看此示例，你可能会想知道重点是什么，如果使用 My 的示例比仅使用 Environment 命名空间的第一个示例更长。记住，重点不是访问特定类时输入的长度，而是一种逻辑方式，可以在不花费大量时间寻找的情况下找到经常访问的资源。你是否会知道在 Environment 类中查找以获取用户计算机的机器名称？也许会，也许不会。使用 My.Computer.Info.MachineName.ToString 是一个非常有逻辑的方法；并且一旦编译，此命名空间声明将被设置为与前面显示的相同类一起工作，而不会产生性能损失。

如果你在 Windows 窗体应用程序中输入 My 关键字，IntelliSense 会为你提供七个可用的项目：Application、Computer、Forms、Resources、Settings、User 和 WebServices。虽然此关键字在 Windows 窗体环境中效果最佳，但在 Web 窗体世界中仍然有一些可用的内容。如果你正在处理 Web 应用程序，那么你将从 My 关键字获得三个项目：Application、Computer 和 User。每个项目在以下各节中进一步描述。

## My.Application

My.Application 命名空间让你可以快速访问与整体应用程序相关的特定设置和点。表 4-2 详细说明了 My.Application 命名空间的属性和方法。

**TABLE 4-2: My.Application Properties and Methods**

| PROPERTY/METHOD | DESCRIPTION |
|---|---|
| `ApplicationContext` | 返回有关 Windows 窗体应用程序线程的上下文信息 |
| `ChangeCulture` | 一种方法，使你能够更改当前应用程序线程的文化 |
| `ChangeUICulture` | 一种方法，使你能够更改资源管理器正在使用的文化 |
| `Culture` | 返回当前线程正在使用的当前文化 |
| `Deployment` | 返回 ApplicationDeployment 对象的实例，该对象允许以编程方式访问应用程序的 ClickOnce 功能 |
| `GetEnvironmentVariable` | 一种方法，使你能够访问环境变量的值 |
| `Info` | 提供对 Windows 窗体的程序集的快速访问。你可以检索程序集信息，例如版本号、名称、标题、版权信息等。 |
| `IsNetworkDeployed` | 返回一个布尔值，指示应用程序是否通过 ClickOnce 功能通过网络分发。如果为 True，则应用程序已使用 ClickOnce 部署，否则为 False。 |

# TABLE 4.2 (continued)

| PROPERTY/METHOD | DESCRIPTION |
|---|---|
| Log | 使你能够向应用程序的事件日志侦听器写入内容 |
| MinimumSplashScreenDisplayTime | 使你能够设置启动画面显示的时间 |
| OpenForms | 返回 FormCollection 对象，允许访问当前打开窗体的属性 |
| SaveMySettingsOnExit | 提供在退出应用程序时保存用户设置的功能。此方法仅适用于 Windows 窗体和控制台应用程序。 |
| SplashScreen | 使你能够以编程方式为应用程序分配启动画面 |
| UICulture | 返回资源管理器当前使用的文化 |

使用 My.Application 命名空间可以完成很多工作。作为其用法的示例，让我们关注 Info 属性。此属性提供对应用程序 AssemblyInfo.vb 文件中存储的信息以及有关类文件的其他详细信息的访问。在你的一个应用程序中，你可以创建一个使用以下代码显示的消息框：

```
MessageBox.Show("Company Name: " & My.Application.Info.CompanyName & vbCrLf &
"Description: " & My.Application.Info.Description & vbCrLf &
"Directory Path: " & My.Application.Info.DirectoryPath & vbCrLf &
"Copyright: " & My.Application.Info.Copyright & vbCrLf &
"Trademark: " & My.Application.Info.Trademark & vbCrLf &
"Name: " & My.Application.Info.AssemblyName & vbCrLf &
"Product Name: " & My.Application.Info.ProductName & vbCrLf &
"Title: " & My.Application.Info.Title & vbCrLf &
"Version: " & My.Application.Info.Version.ToString())
```

来自 Message Box - Assembly.txt 的代码片段

从此示例可以清楚地看出，你可以获取有关正在运行应用程序程序集的相当多的信息。运行此代码会产生类似于图 4-15 所示的消息框。

来自 My.Application 命名空间的另一个有趣的属性是 Log 属性。此属性使你能够处理应用程序的日志文件。例如，你可以通过首先更改应用程序的 app.config 文件以包含以下内容来轻松地向系统的应用程序事件日志写入内容：

![](img/d99870e80390742f93963da7be0b2e61_263_0.png)

# FIGURE 4-15

```
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.diagnostics>
    <sources>
      <source name="DefaultSource" switchName="DefaultSwitch">
        <listeners>
          <add name="EventLog" />
        </listeners>
      </source>
    </sources>
    <switches>
      <add name="DefaultSwitch" value="Information" />
```

