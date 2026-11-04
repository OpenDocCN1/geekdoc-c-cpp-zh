

## 第19章：开发 Silverlight 应用程序

在 Signature 项目中，添加一个服务引用（参见图19-75）。

![](img/a977a875c7c627b45d939729705a252e_712_0.png)

图19-75

单击 Discover 按钮，然后点击 OK（参见图19-76）。

![](img/a977a875c7c627b45d939729705a252e_712_1.png)

图19-76

## 第二部分：使用 C# 进行应用程序开发

在 Page.xaml.cs 中，按如下方式修改 Save 按钮：

```
//---Save button---
void btnSave_MouseLeftButtonDown(
    object sender, MouseButtonEventArgs e)
{
    try
    {
        ServiceReference1.WebServiceSoapClient ws = new
            Signature.ServiceReference1.WebServiceSoapClient();

        //---wire up the event handler when the web service returns---
        ws.SaveSignatureCompleted += new
            EventHandler<Signature.ServiceReference1.
            SaveSignatureCompletedEventArgs>(ws_SaveSignatureCompleted);

        //---calls the web service method---
        ws.SaveSignatureAsync(GetSignatureLines());
    }
    catch (Exception ex)
    {
        txtStatus.Text = ex.ToString();
    }
}
```

在这里，你将签名异步发送到 Web 服务。当 Web 服务调用返回时，将调用 ws_SaveSignatureCompleted 事件处理程序。

编写 ws_SaveSignatureCompleted 事件处理程序，如下所示：

```
void ws_SaveSignatureCompleted(
    object sender,
    Signature.ServiceReference1.SaveSignatureCompletedEventArgs e)
{
    txtStatus.Text = "Signature sent to WS!";
}
```

在 Page.xaml.cs 中，按如下方式编写 Load 按钮代码：

```
//---Load button---
void btnLoad_MouseLeftButtonDown(
    object sender, MouseButtonEventArgs e)
{
    try
    {
        ServiceReference1.WebServiceSoapClient ws = new
            Signature.ServiceReference1.WebServiceSoapClient();

        //---wire up the event handler when the web service
        // returns---
        ws.GetSignatureCompleted +=
            new EventHandler<Signature.ServiceReference1.
            GetSignatureCompletedEventArgs>(ws_GetSignatureCompleted);
        //---calls the web service method---
        ws.GetSignatureAsync();
    }
    catch (Exception ex)
    {
        txtStatus.Text = ex.ToString();
    }
}
```

在这里，你调用 Web 服务来检索已保存的签名。当 Web 服务调用返回时，将调用 ws_GetSignatureCompleted 事件处理程序。

编写 ws_GetSignatureCompleted 事件处理程序，如下所示：

```
void ws_GetSignatureCompleted(
object sender,
Signature.ServiceReference1.GetSignatureCompletedEventArgs e)
{
    txtStatus.Text = "Signature loaded from WS!";
    DrawSignature(e.Result);
}
```

保存 Signature 项目。在“解决方案资源管理器”中，右键单击 SignatureWebSite 项目，然后选择“添加 Silverlight 链接”（参见图19-77）。

![](img/a977a875c7c627b45d939729705a252e_714_0.png)

图19-77

## 第二部分：使用 C# 进行应用程序开发

这会使 Visual Studio 2008 将 Silverlight 项目中的相关文件复制到当前项目。使用自动填充的默认值，并单击 Add（参见图19-78）。

![](img/a977a875c7c627b45d939729705a252e_715_0.png)

图19-78

请注意，项目中添加了一个名为 ClientBin 的新文件夹，其中包含 Signature.xap 文件（参见图19-79）。

![](img/a977a875c7c627b45d939729705a252e_715_1.png)

图19-79

## 第19章：开发 Silverlight 应用程序

在“解决方案资源管理器”中，右键单击 SignatureWebSite 项目，然后选择“设为启动项目”（参见图19-80）。

![](img/a977a875c7c627b45d939729705a252e_716_0.png)

图19-80

选择 SignatureTestPage.aspx，然后按 F5 测试项目。现在你可以将签名保存到 Web 服务，也可以从 Web 服务加载已保存的签名（参见图19-81）。

![](img/a977a875c7c627b45d939729705a252e_716_1.png)

图19-81

## 总结

本章演示了如何使用 Silverlight 构建富交互应用程序（RIA）。在撰写本书时，Silverlight 有两个版本——1.0 和 2——关键区别在于 Silverlight 2 中集成了 .NET Framework。要构建 Silverlight 应用程序的用户界面，可以使用 Microsoft Expression 系列应用程序，而编码可以使用 Visual Studio 2008 完成。

## Windows Communication Foundation

Windows Communication Foundation (WCF) 是 Microsoft 用于构建面向服务的应用程序（SOA）的统一编程模型。面向服务的应用程序的某些部分可以作为服务公开，供其他应用程序访问。

WCF 是一个庞大的主题，无法用一章完全涵盖。但本章对这一新技术进行了简要介绍，并展示了它如何解决当前技术的一些局限性。虽然大多数书籍和会议都重点讨论 WCF 背后的理论，但本章会教你如何构建 WCF 服务，然后再解释其背后的理论。

简而言之，本章探讨：

- 传统 ASMX Web Services 与 WCF 有何不同
- WCF 的 ABC
- 构建不同类型的 WCF 服务

## 什么是 WCF？

要理解 WCF 背后的原理，了解当前可用的产品是很重要的。在 Visual Studio 的早期版本（Visual Studio 2005 和 Visual Studio .NET 2003）中，可以使用 ASP.NET 应用程序模型创建 ASMX XML Web Services，向希望使用这些服务的客户端公开功能。

出于向后兼容的考虑，Visual Studio 2008 仍支持 ASMX Web Services，但展望未来，Microsoft 建议开发人员在构建服务时使用 WCF。

为了比较 WCF 和 ASMX Web Services，我们首先使用 Visual Studio 2008 创建一个新的 ASP.NET Web Service Application 项目。将项目命名为 StocksWS。

## 第20章：Windows Communication Foundation

为 Web 服务命名（比如 StocksWebService），然后点击 OK。项目中添加了对该 Web 服务的引用（参见图20-5）。

![](img/a977a875c7c627b45d939729705a252e_722_0.png)

图20-5

StocksWebService 是 Visual Studio 2008 生成的代理类，负责处理将参数映射到 XML 元素，然后通过网络将 SOAP 消息发送到 Web 服务的所有工作。在幕后，Visual Studio 实际上已经从 Web 服务下载了 WSDL（Web 服务描述语言）文档，以便确切了解服务提供什么、需要什么。你可以通过在 Web 服务 URL 的末尾附加 ?WSDL 来查看 WSDL 文档，如下所示：

```
http://localhost:1044/Service1.asmx?WSDL
```

要访问 Web 服务提供的服务，你可以通过编程方式创建代理类的实例，然后调用相应的方法。以下是 Check Price 按钮的代码：

```
private void btnCheckPrice_Click(object sender, EventArgs e)
{
    StocksWebService.Service1SoapClient ws =
        new StocksPriceChecker.StocksWebService.Service1SoapClient();
    MessageBox.Show("Price for " + txtSymbol.Text +
        " is " + ws.GetStockPrice(txtSymbol.Text));
}
```

在 Visual Studio 2008 中，将 StocksPriceChecker 项目设置为启动项目，然后按 F5 调试应用程序。当你输入股票代码并点击 Check Price 时，Web 服务会返回指定股票的价格（参见图20-6）。

![](img/a977a875c7c627b45d939729705a252e_722_1.png)

图20-6

## 第二部分：使用 C# 进行应用程序开发

从这个非常简单的示例中，你需要注意以下几点：

- 即使是简单的 ASMX Web Service，也需要将其托管在 IIS 之类的 Web 服务器上。
- 要访问 Web 服务，客户端使用 HTTP 这一无状态协议，这意味着每个请求都被视为新请求。如果你要编写的应用程序需要 Web 服务记住其之前的状态，则需要实现自己的“有状态”机制。
- ASMX Web Service 使用请求/响应通信模型。Web 服务仅在客户端请求时响应。在此示例中，如果你想监控股票价格，并希望在股票跌破某个价格时收到通知，则必须不断轮询 Web 服务以获取最新价格。更好的方式是让服务在服务端发生特定事件时自动调用客户端。本章后面你将看到如何使用 WCF 实现这一点。

## 比较 WCF 与 ASMX Web Services

既然你已经创建了一个传统的 ASMX Web Service，那么我们来比较 ASMX 和 WCF，看看它们有何不同：

- ASMX Web Services 使用公开的 Web 方法。Web 方法使用请求/响应通信模型。在 WCF 中，这些 Web 方法称为*操作*，你可以使用三种不同类型的通信模型中的任意一种：单向事务、请求/响应和全双工。
- Web 服务使用通过 HTTP 传输的简单对象访问协议（SOAP）消息传递。WCF 可以使用不同的消息协议——SOAP、Plain Old XML（POX）等——并通过各种通信协议（包括 TCP 和 HTTP）进行传输。
- Web 服务在特定的端口号（如端口 80）上侦听；WCF 可以有多个端点在不同端口号上侦听。
- Web 服务由 Web 服务器（如 IIS）托管；WCF 可以以不同形式托管，如 Windows 服务、Windows 应用程序或仅是进程。

## 你的第一个 WCF 服务

使用 Visual Studio 2008 开发 WCF 服务将有助于将其与传统 ASMX Web Services 进行比较。

使用 Visual Studio 2008 创建一个新的 WCF Service Library 应用程序，并将其命名为 `WcfServiceLibraryTest`（参见图20-7）。

