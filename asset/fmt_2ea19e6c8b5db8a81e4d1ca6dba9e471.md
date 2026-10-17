
```html
<form id="form" runat="server">
<p>First Name:
<asp:TextBox ID="TextBox1" runat="server"/></asp:TextBox></p>
<p>Last Name:
<asp:TextBox ID="TextBox2" runat="server"/></asp:TextBox></p>
<p>Age:
<asp:TextBox ID="TextBox3" runat="server" Width="50px"
MaxLength="3"/></asp:TextBox></p>
<p>Are you a member?
<asp:RadioButtonList ID="RadButtonlist1" runat="server">
<asp:ListItem Value="Yes"/></asp:ListItem>
<asp:ListItem Value="No" Selected="True"/></asp:ListItem>
</asp:RadioButtonList></p>
<p><asp:Button ID="Button1" runat="server" Text="Submit"
OnClick="Button1_Click" /></p>
<hr />
<asp:Label ID="Label1" runat="server"/></asp:Label></p>
</form>
</body>
</html>
```

```csharp
<%@ Page Language="C#" %>
<script runat="server">
protected void Button1_Click(object sender, EventArgs e)
{
    if (Page.User.Identity.IsAuthenticated)
    {
        Profile.FirstName = TextBox1.Text;
        Profile.LastName = TextBox2.Text;
        Profile.Age = TextBox3.Text;
        Profile.Member = RadButtonlist1.SelectedItem.Text;
        Profile.LastVisited = DateTime.Now.ToString();

        Label1.Text = "Stored information includes:<p>" +
        "First name: " + Profile.FirstName + 
        "<br>Last name: " + Profile.LastName + 
        "<br>Age: " + Profile.Age + 
        "<br>Member: " + Profile.Member + 
        "<br>Last visited: " + Profile.LastVisited;";
    }
    else
    {
        Label1.Text = "You must be authenticated!";
    }
}
</script>
```

这与你过去处理 `Session` 对象的方式类似，但请注意你存储和检索的个性化属性不是基于键（key）的。因此，在操作它们时，你不需要记住键名。

个性化系统存储的所有项目都会被转换为特定的 .NET 数据类型。默认情况下，这些项目存储为 `String`，并且你对存储的项目具有早期绑定访问权限。要存储项目，你只需直接使用 `Profile` 对象填充个性化属性即可：

```
Profile.FirstName = TextBox.Text
```

要检索信息，你只需如所示获取 `Profile` 类的相应属性即可：

```
Label1.Text = Profile.FirstName
```

在代码视图中使用 `Profile` 类和个性化属性的巨大用处是，这种方法在生成页面时提供了 IntelliSense（智能提示）。当你在此视图中处理 `Profile` 类时，你定义的所有项目都可以通过 IntelliSense 功能作为可用选项，如图 15-2 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_764_0.png)

所有属性都可以在 IntelliSense 中访问。每当你保存对 `web.config` 文件所做的个性化更改时，`Profile` 类都会在后台隐藏并进行动态编译。

# 第 15 章：个性化

存储用户上次访问页面的日期和时间。除了之外，你还可以看到其余的个性化属性是使用特定的 .NET 数据类型定义的。

这是首选的方法，因为在您编写应用程序并使用已定义的个性化属性时，它能够提供类型检查功能。

## 使用自定义类型

从前面的示例中，你可以看到如何为个性化属性定义类型，定义这些属性并将其强制转换为 .NET Framework 中可用的特定类型是非常简单的。诸如 `System.Integer`、`System.String`、`System.DateTime`、`System.Byte` 和 `System.Boolean` 等项可以在 `web.config` 文件中轻松定义。但你如何定义复杂类型呢？

利用自定义类型的个性化属性，其定义方式与使用简单类型的个性化属性一样简单。自定义类型使你能够将诸如购物车信息或其他状态信息等项从一个应用程序存储到另一个应用程序。列表 15-6 首先显示了一个名为 `ShoppingCart`（购物车）的类，你将在稍后的其中一个个性化属性中使用它。

### 列表 15-6：创建一个用作个性化类型的类

```csharp
<Serializable()>
Public Class ShoppingCart
    Private PID As String
    Private CompanyProductName As String
    Private Number As Integer
    Private Price As Decimal
    Private DateAdded As DateTime

    Public Property ProductID() As String
        Get
            Return PID
        End Get
        Set(ByVal value As String)
            PID = value
        End Set
    End Property

    Public Property ProductName() As String
        Get
            Return CompanyProductName
        End Get
        Set(ByVal value As String)
            ProductName = value
        End Set
    End Property

    Public Property NumberSelected() As Integer
        Get
            Return Number
        End Get
        Set(ByVal value As Integer)
            Number = value
        End Set
    End Property

    Public Property ItemPrice() As Decimal
        Get
            Return Price
        End Get
        Set(ByVal value As Decimal)
            Price = value
        End Set
    End Property

    Public Property DateAdded() As DateTime
        Get
            Return DateAdded
        End Get
        Set(ByVal value As DateTime)
            DateAdded = value
        End Set
    End Property
End Class
```

### C#

```csharp
using System;

[Serializable]
public class ShoppingCart
{
  private string PID;
  private string CompanyProductName;
  private int Number;
  private decimal Price;
  private DateTime DateAdded;

  public ShoppingCart() { }

  public string ProductID
  {
    get { return PID; }
    set { PID = value; }
  }

  public string ProductName
  {
    get { return CompanyProductName; }
    set { CompanyProductName = value; }
  }

  public int NumberSelected
  {
    get { return Number; }
    set { Number = value; }
  }

  public decimal ItemPrice
  {
    get { return Price; }
    set { Price = value; }
  }

  public DateTime DateTimeAdded
  {
    get { return DateAdded; }
    set { DateAdded = value; }
  }
}
```

这个简单的购物车构造现在可以在用户在电子商务网站上移动时保存其购物篮。当用户在其他时间返回网站时，购物车可以持久化。请注意，购物车在类声明之前需要一个 `Serializable` 属性，以确保正确转换为 XML 或二进制格式。

查看你如何在 `web.config` 文件中指定个性化属性为复杂类型，例如 `ShoppingCart` 类型。这在列表 15-7 中所示。

### 列表 15-7：为个性化属性使用复杂类型

```xml
<properties>
  <add name="FirstName" type="System.String" />
  <add name="LastName" type="System.String" />
  <add name="LastVisited" type="System.DateTime" />
  <add name="Age" type="System.Int32" />
  <add name="Member" type="System.Boolean" />
</properties>
```

正如基本类型存储在数据存储中一样，这种构造允许你轻松地将自定义类型序列化到你选择的数据存储中。`SerializeAs` 属性可以取以下值：

- **Binary**：以二进制格式序列化并存储该对象。
- **Provider**：基于提供程序序列化。
- **String**：将对象序列化为字符串格式。
- **XML**：将对象序列化为 XML 格式。

## 提供默认值

除了定义个性化类型之外，你可以在 `web.config` 文件中定义它们的默认值。这在列表 15-8 中所示。

### 列表 15-8：提供默认值

```xml
<properties>
  <add name="FirstName" type="System.String" />
  <add name="LastName" type="System.String" />
  <add name="LastVisited" type="System.DateTime" />
  <add name="Age" type="System.Int32" />
  <add name="Member" type="System.Boolean" defaultValue="false" />
</properties>
```

## 将个性化设为只读

可以将个性化属性设为只读。要实现此，只需在`<add>` 元素中添加 `readOnly` 属性：

```xml
<add name="StartDate" type="System.DateTime" readOnly="true" />
```

## 启用匿名识别

要启用用户的匿名识别，需要在 `<system.web>` 节点中添加 `<anonymousIdentification>` 元素。然后在 `<anonymousIdentification>` 元素内部使用 `enabled` 属性并将其值设置为 `true`。

### 列表 15-9：允许匿名识别

```xml
<configuration>
  <system.web>
    <anonymousIdentification enabled="true" />
  </system.web>
</configuration>
```

启用匿名识别后，ASP.NET 为每个访问应用程序的匿名用户使用唯一标识符。该标识符会在每次请求时发送，但在用户身份验证后将移除。

对于匿名用户，信息默认以 Cookie 的形式存储在用户的机器上。其他信息（你为匿名用户启用的个性化属性）存储在服务器指定的存储存储中。

要查看此操作，请关闭示例应用程序的 Windows 身份验证，改用表单身份验证。此更改在列表 15-10 中演示。

### 列表 15-10：关闭 Windows 身份验证并使用表单身份验证

```xml
<configuration>
  <system.web>
    <anonymousIdentification enabled="true" />
    <authentication mode="Forms" />
  </system.web>
</configuration>
```

### 列表 15-11：在 HTTP Header中设置匿名 Cookie

```http
HTTP/1.1 200 OK
Server: ASP.NET Server/8.0.0.0
Date: Sat, 11 Feb 2008 19:23:33 GMT
X-Aspnet-Version: 2.0.50727
Set-Cookie: ASASPANONYMOUS=UH5CftJ1xgEkKAAAZTKN2I3YjUtZDhkOS00NDE2LWF1yJEtOtVjMvMMZXRmHoBU
```

# 第 15 章：个性化

从此 HTTP 头部，你可以看到 cookie ...ASPXANONYMOUS — 被设置为一个哈希值，以供 ASP.NET 个性化系统后续检索。

## 更改匿名标识的 Cookie 名称

默认情况下，Cookie 使用名为 `.ASPXANOUSIdentification` 的 cookie 名称。你可以通过 `web.config` 文件中的 `<anonymousIdentification>` 元素使用 `cookieName` 属性更改 cookie 的名称，如列表 15-12 所示。

### 列表 15-12：更改 cookie 的名称

```xml
<configuration>
  <system.web>
    <anonymousIdentification
      enabled="true"
      cookieName="ASPXenWebApplication" />
  </system.web>
</configuration>
```

## 更改 Cookie 的存储长度

此外，默认情况下，存储在用户机器上的 cookie 存储时间为 100,000 分钟（大约 70 天）。如果你想更改此值，可以在 `<anonymousIdentification>` 元素中使用 `cookieTimeout` 属性进行设置，如列表 15-13 所示。

### 列表 15-13：更改 cookie 的存储长度

```xml
<configuration>
  <system.web>
    <anonymousIdentification
      enabled="true"
      cookieTimeout="1440" />
  </system.web>
</configuration>
```

在这种情况下，`cookieTimeout` 值被更改为 1440 — 意味着 1440 分钟（或一天）。这对于购物车之类的场景非常理想，因为你不希望长时间持久化用户的标识。

## 更改标识的存储方式

虽然匿名标识是通过 cookie 存储的，但你也可以轻松地更改。到目前为止，cookie 是实现标识的首选方式，但你也可以不使用 cookie。其他选项包括 URI 或设备配置文件。列表 15-14 显示了使用 URI 列出标识的示例。

### 列表 15-14：指定 cookie 的存储方式

```xml
<configuration>
  <system.web>
    <anonymousIdentification>
      enabled="true"
      cookieless="UseUri" />
    </anonymousIdentification>
  </system.web>
</configuration>
```

除了 `UseUri`，其他选项还包括 `UseCookies`、`AutoDetect` 和 `UseDeviceProfile`。以下列表回顾了每一项：
