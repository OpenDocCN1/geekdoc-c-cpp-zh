

## 第四部分：Internet 应用程序

- **第 20 章：** Silverlight 与服务
- **第 21 章：** 使用 ASP.NET
- **第 22 章：** ASP.NET 高级功能
- **第 23 章：** ASP.NET MVC
- **第 24 章：** SharePoint 2010 开发

### 第 20 章：Silverlight 与服务

### 本章学习内容

- ASMX Web 服务
- ADO.NET 数据服务
- WCF RIA 服务
- 模型-视图-视图模型（MVVM）

如你在前一章中所看到的，Silverlight 为开发者提供了一个熟悉的应用开发环境。然而，Silverlight 的能力远不止创建外观出色的网站，它同样支持丰富的业务线（line-of-business）应用程序。通过 Silverlight 3，微软让开发者能够轻松创建各种业务应用程序，包括新的 DataForm 控件和 Validation 控件。Silverlight 4（目前处于测试阶段，即将发布）将继续加强 Silverlight 对业务线应用的支持，增加诸如受信任的离线功能和对离线更精细的控制等新特性。

在本章中，你将学习如何利用现有的 Web 服务技术，以及如何使用一些面向 Silverlight 的较新技术。与所有业务线应用程序一样，能够获取数据并将其更新回服务器非常重要。Silverlight 可以通过现有的 Web 服务（如 SOAP 或 WCF）稍加修改即可实现这一点，也可以使用 ADO.NET 数据服务和 RIA 服务等一些新产品。

本章还概述了一种常用于开发 Silverlight 业务线应用程序的推荐最佳实践——模型-视图-视图模型（Model-View-ViewModel，MVVM）。该最佳实践非常适合创建易于测试和维护的软件。

### 服务与 Silverlight

在前面的章节中，你已经了解了如何使用各种 Web 服务技术将数据获取到 Windows Forms 应用程序中，而我们将在 Silverlight 中继续使用这些概念。本章的大部分内容是对前面服务相关章节所学知识的回顾，但它指出了在 Silverlight 中调用这些服务与其他类型应用程序之间的差异。

### ASMX Web 服务

.NET 中最早提供的 Web 服务类型之一是 ASMX Web 服务，有时也称为 SOAP。这种简单协议使用 XML 在服务器和客户端之间来回发送消息。ASMX Web 服务旨在处理客户端与服务器之间的同步调用，但在 Silverlight 中，你必须采取略有不同的方法，因为 Silverlight 中的所有调用都必须是异步的，以防止 Web 浏览器在等待 Silverlight 应用程序从服务器获取响应时被锁定。

首先，我们将在 Visual Studio 中创建一个新的 Silverlight 应用程序，然后通过右键单击 ASP.NET 项目并选择“添加新项”来添加一个新的 Web 服务。在出现的列表中，选择“Web 服务”，如图 20-1 所示。

![图 20-1](img/d99870e80390742f93963da7be0b2e61_707_0.png)

创建 Web 服务后，你将看到以下代码：

```vb
Imports System.Web.Services
Imports System.Web.Services.Protocols
Imports System.ComponentModel

' To allow this Web Service to be called from script,
' using ASP.NET AJAX, uncomment the following line.
' <System.Web.Script.Services.ScriptService()> _
<System.Web.Services.WebService(Namespace:="http://tempuri.org/")> _
<System.Web.Services.WebServiceBinding(ConformsTo:=WsiProfiles.BasicProfile1_1)> _
<ToolboxItem(False)> _
Public Class WebService1
    Inherits System.Web.Services.WebService

    <WebMethod()> _
    Public Function HelloWorld() As String
        Return "Hello World"
    End Function

End Class
```

这是你能得到的最基本的 Web 服务——一个返回字符串的简单 HelloWorld 函数。下一步是从 Silverlight 应用程序中引用该 Web 服务。右键单击 Silverlight 项目并选择“添加服务引用”。此时将出现如图 20-2 所示的“添加服务引用”对话框。

![图 20-2](img/d99870e80390742f93963da7be0b2e61_708_0.png)

生成你的项目，然后点击右侧的“发现”按钮。当它找到你刚创建的 Web 服务时，点击“确定”。完成此操作后，你的 Silverlight 项目将包含对该服务的引用，以及一个名为 `ServiceReferences.ClientConfig` 的新文件，其中包含类似的代码：

```xml
<configuration>
    <system.serviceModel>
        <bindings>
            <basicHttpBinding>
                <binding name="WebService1Soap" maxBufferSize="2147483647"
                    maxReceivedMessageSize="2147483647">
                    <security mode="None" />
                </binding>
            </basicHttpBinding>
        </bindings>
        <client>
            <endpoint address="http://localhost:38588/WebService1.asmx"
                binding="basicHttpBinding"
                bindingConfiguration="WebService1Soap"
                contract="ServiceReference1.WebService1Soap"
                name="WebService1Soap" />
        </client>
    </system.serviceModel>
</configuration>
```

使用大多数 Web 服务时都会添加此文件。如代码所示，它将终结点地址定义为本地测试 Web 服务器。在将 Silverlight 应用程序从开发环境迁移到生产环境时，你需要更改该属性，使其指向生产地址。

此外，在创建 Web 服务引用时，Visual Studio 会自动生成一个代理类，使调用 Web 服务变得更加容易。在本示例中，它被命名为 `WebService1SoapClient`，你可以通过 `ServiceReference1.WebService1SoapClient` 来引用它。这与向其他项目类型添加 Web 服务相同，不同之处在于，它会为 Web 服务中公开的每个函数生成一个名为 `<functionname>Async` 的函数，以及一个名为 `<functionname>Completed` 的事件。你将在此事件中接收 Web 服务函数调用的结果。

若要从 Silverlight 应用程序中调用该服务，请打开 MainPage.xaml 的代码视图并创建以下代码：

```vb
Private WithEvents svc As New ServiceReference1.WebService1SoapClient

Private Sub MainPage_Loaded(ByVal sender As Object,
ByVal e As System.Windows.RoutedEventArgs) Handles Me.Loaded
    TestSoapCall()
End Sub

Private Sub TestSoapCall()
    svc.HelloWorldAsync()
End Sub

Private Sub svc_HelloWorldCompleted(ByVal sender As Object,
ByVal e As ServiceReference1.HelloWorldCompletedEventArgs) Handles svc.HelloWorldCompleted
    MessageBox.Show(e.Result)
End Sub
```

*来自 WebService1SoapClient 的代码片段*

与从其他类型的应用程序调用 Web 服务不同，在 Silverlight 中，由于异步限制，你需要创建一个事件处理程序来处理 `HelloWorldCompleted` 事件。这与你可能在其他 Web 服务中使用的做法略有不同，而且使用此方法时需要记住一些事项，包括更新用户界面以通知用户正在等待服务器的响应，以及禁用可能需要服务器返回数据的按钮。

使用 ASMX Web 服务时，你还可以向 Silverlight 传递比字符串更复杂的对象。这为从数据库或其他服务器系统传递数据提供了大量可能性。虽然 ASMX Web 服务很简单，但它们并不总是来回发送数据的最佳方式，因为每个对象都会被序列化为 XML，且不会进行压缩。正如你将在下一个示例中看到的，WCF 服务无需特殊配置或编码即可提供其中一些选项。

### WCF 服务

WCF 服务在创建与服务器的连接方面几乎与 ASMX Web 服务方法相同，但相比 ASMX Web 服务，它提供了许多性能和安全性方面的优势。

首先创建另一个服务：右键单击你的 ASP.NET 应用程序，然后选择“添加新项”。在 Silverlight 类别下，你会找到支持 Silverlight 的 WCF 服务，如图 20-3 所示。

![图 20-3](img/d99870e80390742f93963da7be0b2e61_709_0.png)

创建支持 Silverlight 的 WCF 服务与创建普通 WCF 服务几乎完全相同；唯一的区别是以下选项：

