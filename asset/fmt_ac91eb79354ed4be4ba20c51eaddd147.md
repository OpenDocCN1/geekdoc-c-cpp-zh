
思路是当最终用户点击它时，会导致 ASP.NET 应用程序向 XML 服务发送 SOAP 请求。返回的 `DataSet` 绑定到 `GridView`，并且页面重绘，如图 31-10 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_1225_0.png)

图 30

`Customers` 服务通过实例化 `WroxCustomers.Customers` 代理对象来调用：

```vb
Dim As New WroxCustomers.Customers()
```

然后，你可以像使用项目中任何其他对象一样使用它。在列表 31-7 的代码示例中，`ws.GetCustomers()` 方法调的结果赋值给 `GridView` 的 `DataSource` 属性：

```vb
GridView.DataSource = ws.GetCustomers()
```

## 重载 WebMethod (Overloading WebMethods)

在 .NET 面向对象的世界中，代码中使用方法重载是可能的。真正的面向对象语言支持多态，方法重载是其中一部分。方法重载允许你有多个具有相同名称但签名不同的方法。通过方法重载，可以调用一个方法，并根据调用的完整签名将其路由到适当的方法。列表 31-8 显示了标准方法重载的示例。

### 列表 31-8: .NET 中的方法重载

```vb
Public Function HelloWorld() As String
    Return "Hello"
End Function
```

```vb
Public Function HelloWorld(ByVal FirstName As String) As String
    Return "Hello " & FirstName
End Function
```

```cs
public string HelloWorld() {
    return "Hello";
}
public string HelloWorld(string FirstName) {
    return "Hello " + FirstName;
}
```

在此示例中，两个方法具有相同的名称 `HelloWorld`。那么，当你调用 `HelloWorld` 时，执行的是哪一个方法呢？嗯，这取决于你传递给方法的签名。例如，你可能会提供以下内容：

`Label1.Text = HelloWorld();`

这产生的结果只是 `Hello`。然而，你可能会使用以下签名调用 `HelloWorld()` 方法：

`Label1.Text = "Hello Bill Evjen";`

然后你将得到 `Hello Bill Evjen` 的结果。如你所见，方法重载是你的 ASP.NET 可以轻松利用的一项强大功能——但你如何对 WebMethods 进行重载呢？

如果你已经尝试过对你的任何 WebMethods 进行重载，当你在浏览器中打开 Web 服务时，可能会遇到以下错误：

> Both System.String HelloWorld(System.String) and System.String HelloWorld() use the message name "HelloWorld". 使用 WebMethod 自定义属性的 Name 属性为方法指定唯一的消息名称。

如该错误所示，重载 WebMethods 所需的额外步骤是使用 `MessageName` 属性。列表 31-9 显示了方法。

### 列表 31-9：.NET 中的 WebMethod 重载

```vb
<WebMethod(MessageName="HelloWorld")
Public Function HelloWorld() As String
    Return "Hello"
End Function
```

```vb
<WebMethod(MessageName="HelloWorldWithFirstName")
Public Function HelloWorld(ByVal FirstName As String) As String
    Return "Hello " & FirstName
End Function
```

```cs
[WebMethod(MessageName="HelloWorldWithFirstName")]
public string HelloWorld(string FirstName) {
    return "Hello " + FirstName;
}
```

除了 `WebMethod` 属性的 `MessageName` 属性外，你必须禁用你的 Web 服务对 WS-I Basic Profile 规范的遵守——如果你通过不向代码添加 `<WebServiceBinding>` 属性来提供 WebMethod 重载，你就会这样做，如列表 31-10 所示。

### 列表 31-10：更改你的 Web 服务使其不符合 WS-I Basic Profile

```vb
<WebServiceBinding(ConformsTo = WsiProfiles.None)>
  Public Class MyOverloadingExample
  End Class
```

```cs
[WebServiceBinding(ConformsTo = WsiProfiles.None)]
public class WrowMath : System.Web.Services.WebService
{
    // 代码在此处
}
```

另一个选项是在 `web.config` 文件中关闭 WS-I Basic Profile 能力，如列表 31-11 所示。

### 列表 31-11：使用 web.config 文件关闭一致性

```xml
<configuration>
  <system.web>
    <webServices>
      <conformanceWarnings>
        <remove name="BasicProfile_1" />
      </conformanceWarnings>
    </webServices>
  </system.web>
</configuration>
```

在你定义了重载 WebMethods 的服务后，当浏览器中打开 Web 服务接口测试页面时，你可以看到通过它们的 `MessageName` 值属性定义的两个 WebMethods（见图 31-11）。

![](img/7040c21013b8e6c23c612d6da3599ff8_1227_0.png)

图 31-11

尽管你可以看到 WebMethods 的名称相同，但 `MessageName` 属性显示它们是不同的方法。当开发者使用 Web 服务时，他将只看到一个可用方法（在本例中为 `HelloWorld`）。它通过使用这些方法的应用程序中的 Visual Studio 2010 IntelliSense（智能感知）显示（见图 31-12）。

### 缓存 Web 服务响应

![](img/7040c21013b8e6c23c612d6da3599ff8_1228_0.png)

图 31-12

在你用于引导开发者签名结构的框中，你可以看到两个选项 —— 一个空签名，另一个需要单个字符串。

## 缓存 WEB 服务 响应

缓存是你使用 .NET 构建的几乎每个应用程序中都包含的一项重要功能。第 22 节涵盖了你在 ASP.NET 中可以使用的大部分功能，但 .NET 中 服务的特定功能允许你缓存发送到任何服务消费者的 SOAP 响应。

首先，作为回顾，请记住缓存是维护内存存储的能力，其中数据、对象和项目被存储起来以供重用。此功能提高了你构建和管理的应用程序的响应速度。有时，返回缓存结果可以极大影响性能。

XML Web 服务使用一个属性来控制 SOAP 响应的缓存——`CacheDuration` 属性。列表 31-12 显示了用法。

### 列表 31-12：利用 CacheDuration 属性

```vb
[Method(CacheDuration=60)]
Public Function GetSqlServer() As String
    Return DateTime.Now.ToString();
End Function
```

```cs
[Method(CacheDuration=60)]
public string GetSqlServer() {
    return DateTime.Now.ToString();
}
```

如你所见，`CacheDuration` 在 `Method` 属性中的用法就像 `Description` 和 `Name` 属性。在你定义了重载 WebMethods 的服务后，当你在浏览器中打开 Web 服务接口测试页面时，你可以看到通过它们的 `MessageName` 值属性定义的两个 WebMethods（见图 31-11）。

## 使用头部

扩展 SOAP 消息常用形式之一是在头部部分添加有关请求的元数据。图 31-13 显示了 SOAP 消息的结构。

整个 SOAP 消息被称为封包（envelope）。SOAP 消息包含正文（body）——这是消息的要素元素。SOAP 消息的一个可选组件是头部（header）。

在 SOAP 头部应该包含什么信息？它可以包含很多内容。放在 SOAP 头部中的常见项目之一是消费你的 Web 服务所需的任何身份验证/授权功能。在消息头部放置用户名和密码是你可能包含内容的示例。

## 构建带有 SOAP 头部的 Web 服务

你可以基于首次打开时的默认 `.asmx` 页面（列表 31-4）进行构建。将新的 `.asmx` 文件命名为 `HelloSoapHeader.asmx`。第一步是添加一个表示要放置在 SOAP 头部对象的类，如列表 31-13 所示。

> 列表 31-13：代表 SOAP 头部的类

```vb
Public Class HelloHeader
Inherits System.Web.Services.Protocols.SoapHeader

    Public Username As String
    Public Password As String
End Class
```

```cs
public class HelloHeader : System.Web.Services.Protocols.SoapHeader
{
    public string Username;
    public string Password;
}
```

### 列表 3-14：利用 SOAP 标头的 Web 服务类

```vb
<WebService(Namespace="http://www.wrox.com/helloworld")
<WebServiceBinding(ConformsTo=WsiProfiles.BasicProfile_1,
    EmitConfigurationClaims=True)>
Public Class HelloSoapHeader
    Inherits System.Web.Services.WebService
```

```vb
Public myHeader As HelloHeader

[WebMethod(), SoapHeader("myHeader")
Public Function HelloWorld() As String
    If (myHeader Is Nothing) Then
        Return "Hello World"
    Else
        Return "Hello " & myHeader.Username & " * " & &
               <br>Your password is: " & myHeader.Password
    End If
End Function
```

```vb
End Class
```

```csharp
[WebService(Namespace = "http://www.wrox.com/helloworld")]
[WebServiceBinding(ConformsTo=WsiProfiles.BasicProfile_1)]
public class HelloSoapHeader : System.Web.Services.WebService
{
    public HelloHeader myHeader;

    [WebMethod()]
    [SoapHeader("myHeader")]
    public string HelloWorld() {
        if (myHeader == null) {
            return "Hello World";
        }
        else {
            return "Hello " + myHeader.Username + " * " +
                   "<br>Your password is: " + myHeader.Password;
        }
    }
}
```

该服务 `HelloSoapHeader` 包含一个 `WebMethod` — `HelloWorld`。在 Web 服务类内部，但在 `WebMethod` 之外，你创建了 `SoapHeader` 类的实例。你可以通过以下代码行来实现：

```vb
Public myHeader As HelloHeader
```

现在，你已经有了之前创建的名为 `myHeader` 的 `HelloHeader` 类实例，你可以在你的 `WebMethod` 中使用该实例化。由于服务可以包含任意数量的 `WebMethod`，并不要求所有 `WebMethod` 都必须使用 SOAP 标头的实例化。你通过在 `WebMethod` 声明之前放置 `SoapHeader` 特性，来指定某个 `WebMethod` 是否使用某个特定的 SOAP 标头实例化。

```vb
[WebMethod(), SoapHeader("myHeader")]
    Public Function HelloWorld() As String
        Code here
    End Function
```

在本示例中，`SoapHeader` 特性接收一个实例化的 `SoapHeader` 类名称字符串值——在此情况下为 `myHeader`。

## 1172 | 第 31 章 处理服务

从这里开始，`WebMethod` 实际上使用了 `myHeader` 对象。如果没有找到 `myHeader`（这意味着客户端在其构建的 SOAP 消息中没有发送 SOAP 头部），则返回简单的 "Hello World"。但是，如果 SOAP 请求的 SOAP 头部提供了值，则会在返回的字符串中使用这些值。

### 使用 SOAP Header消耗 Web 服务

构建一个使用 SOAP 头部向 Web 服务发送 SOAP 请求的 ASP.NET 是非常困难的。与不包含 SOAP 标头的 Web 服务一样，你直接在 Visual Studio 中对远程 Web 服务创建引用（Web Reference）。

对于 ASP.NET 页面，创建一个带有单个 `Label` 控件的简单页面。Web 服务的输出放在 `Label` 控件中。列表 31-15 显示了 ASP.NET 页面的代码。

### 列表 31-15：使用 SOAP 标头的 XML Web 服务 ASP.NET 页面

```vb
<script runat="server">
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Dim ws As New localhost.HelloSoapHeader()
    Dim wsHeader As New localhost.HelloHeader()

    wsHeader.Username = "Bill Evjen"
    wsHeader.Password = "Bubbles"
    ws.HelloHeaderValue = wsHeader
    Label1.Text = ws.HelloWorld()
End Sub
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Working with SOAP headers</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label Id="Label1" Runat="server"></asp:Label>
</div>
</form>
</body>
</html>
```

```csharp
<@ Page Language="C#" %>
<script runat="server">
protected void Page_Load(object sender, System.EventArgs e) {
    localhost.HelloSoapHeader ws = new localhost.HelloSoapHeader();
    localhost.HelloHeader wsHeader = new localhost.HelloHeader();

    wsHeader.Username = "Bill Evjen";
    wsHeader.Password = "Bubbles";
    ws.HelloHeaderValue = wsHeader;

    Label1.Text = ws.HelloWorld();
}
</script>
```
