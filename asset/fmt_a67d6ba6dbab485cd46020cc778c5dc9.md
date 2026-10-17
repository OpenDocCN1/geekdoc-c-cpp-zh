
```vbnet
For each profileInfo As ProfileInfo In pic
Dim li As ListItem = New ListItem()
li.Text = proInfo.UserName.ToString()
DropDownList1.Items.Add(li)
Next
```

```vbnet
Label1.Text = outputInt.ToString()
End Sub
```

```html
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head1" runat="server">
<title>ProfileAdmin 页面</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<br>配置文件管理器<br />
<br />
系统中的用户总数：
<asp:Label ID="Label" runat="server"></asp:Label><br />
<asp:Panel>
<asp:DropDownList ID="DropDownList1" runat="server">
<asp:Button ID="Select-Button" runat="server"
OnClick="Select-Button_Click"
Text="获取配置文件信息" /><br />
<asp:DetailsView ID="DetailsView" runat="server" CellPadding="4"
Border="#333333" GridLines="None"
Height="50px"
<HeaderStyle Color="#1C85E5" Font-Bold="True" Foreground="White" />
<FooterStyle Color="#666666" Foreground="White" />
<HorizontalAlign="Center" />
<HeaderStyle Color="#1C85E5" Font-Bold="True" Foreground="White" />
<AlternatingRowStyle BackColor="#C5BBAF" Font-Bold="True" />
<CommandRowStyle BackColor="White" />
<RowStyle BackColor="#E3AEE6" />
<FieldHeaderStyle BackColor="#DDDDDD" Font-Bold="True" />
</asp:DetailsView>
<br />
<asp:Button ID="DeleteButton" runat="server"
Text="删除所选用户的配置文件信息"
OnClick="DeleteButton_Click" /><br />
</div>
</form>
</body>
</html>
```

```csharp
<%@ Page Language="C#" %>

<script runat="server">

protected void Page_Load(object sender, EventArgs e)
{
    if (DropDownList1.Items.Count == 0
```

# 594 | 第 14 章 个性化

# 列表 14-27（续）

```csharp
(
    WriteDropdownList();
    WriteUserOutput();
}
protected void DeleteButton_Click(object sender, EventArgs e)
{
    ProfileManager.DeleteProfile(DropDownList1.Text.ToString());
    DropDownList1.Items.Clear();
    WriteDropdownList();
    WriteUserOutput();
}
protected void SelectButton_Click(object sender, EventArgs e)
{
    WriteUserOutput();
}
protected void WriteUserOutput()
{
    int outInt;
    ProfileInfoCollection pic = new ProfileManager.FindProfilesByUsername(
        ProfileAuthenticationOption,
        DropDownList1.Text.ToString(), 0, 1, outInt);
    DetailsView.DataSource = pic;
    DetailsView.Bind();
}
protected void WriteDropdownList()
{
    int outInt;
    ProfileInfoCollection pic = ProfileManager.Provider.GetAllProfiles(
        ProfileAuthenticationOption, 0, 10000, outInt);

    foreach (ProfileInfo proInfo in pic)
    {
        ListItem li = new ListItem();
        li.Text = proInfo.UserName.ToString();
        DropDownList1.Items.Add(li);
    }
    Label.Text = outInt.ToString();
}
</script>
```

# 查看 ProfileManager.aspx 页面的代码

在查看 `ProfileManager.aspx` 页面的代码时，请注意 `ProfileManager` 类被用于执行几个不同的操作。

`ProfileManager` 类的 `GetAllProfiles()` 方法用于填充页面上的 `DropDownList` 控件。以下是该方法的构造函数：

```
GetAllProfiles(
    authenticationOption,
    pageIndex,
    pageSize,
    totalRecords)
```

`GetProfiles()` 方法接收多个参数，其中第一个参数允许你定义是使用此方法处理系统中的所有配置文件，还是仅处理系统中的匿名用户或已验证用户的配置文件。在示例中，使用此方法检索了所有配置文件。这是通过 `ProfileAuthenticationOption` 枚举实现的。然后，`GetProfiles()` 方法的其他参数要求你指定页码和从数据库中检索的记录数。它并没有提供“获取所有”的方法（因为可能检索的数据量过大）；因此在此实例中，你使用 `0` 指定了第一页数据，该页包含前 1000 条记录（这基本上等同于获取所有）。`GetProfiles()` 方法的最后一个参数允许你检索在应用程序中使用的记录。你可以遍历这些记录。`ProfileManager.aspx` 使用此数字显示在 `Label` 控件中。

从 `GetProfiles()` 方法的返回值中，你将得到一个 `ProfileInfo` 对象，它是 `ProfileInfoCollection` 的集合。遍历 `ProfileInfoCollection` 中的所有 `ProfileInfo` 对象可以允许你提取特定用户配置文件信息中的一些主要属性。在示例中，`ProfileInfo` 对象的 `Username` 属性被用于填充 `DropDownList` 控件。

当用户选择某个配置文件时，通过遍历 `ProfileInfoCollection` 中的所有 `ProfileInfo` 对象，你可以提取出特定用户配置文件的某些主要属性。在示例中，`ProfileInfo` 对象的 `Username` 属性被用于填充 `DropDownList` 控件。

从 `GetProfiles()` 方法的返回值中，你将得到一个 `ProfileInfo` 对象，它是 `ProfileInfoCollection` 的集合。遍历 `ProfileInfoCollection` 中的所有 `ProfileInfo` 对象可以允许你提取出特定用户配置文件信息中的一些主要属性。在示例中，`ProfileInfo` 对象的 `Username` 属性被用于填充 `DropDownList` 控件。

当用户选择某个配置文件时，通过遍历 `ProfileInfoCollection` 中的所有 `ProfileInfo` 对象，可以允许你提取出特定用户配置文件信息中的一些主要属性。在示例中，`ProfileInfo` 对象的 `Username` 属性被用于填充 `DropDownList` 控件。

从 `GetProfiles()` 方法的返回值中，你将得到一个 `ProfileInfo` 对象，它是 `ProfileInfoCollection` 的集合。遍历 `ProfileInfoCollection` 中的所有 `ProfileInfo` 对象可以允许你提取出特定用户配置文件信息中的一些主要属性。在示例中，`ProfileInfo` 对象的 `Username` 属性被用于填充 `DropDownList` 控件。

当用户选择某个配置文件时，通过遍历 `ProfileInfoCollection` 中的所有 `ProfileInfo` 对象，可以允许你提取出特定用户配置文件信息中的一些主要属性。在示例中，`ProfileInfo` 对象的 `Username` 属性被用于填充 `DropDownList` 控件。

# 运行 ProfileManager.aspx

当你编译并运行 `ProfileManager.aspx` 时，你将看到类似于图 14-6 的结果。

#

![Figure 14-6](img/7040c2101b8e6c2312da3599ff8_655.png)

图 14-6

从该屏幕，你可以看到此页面正在处理匿名用户。你也可以看到 `IsAnonymous` 列确实被勾选了。

ASP.NET 提供的个性化功能使得能够非常轻松地为所有用户（无论已验证用户还是匿名用户）创建独特的应用程序。该系统允许你存储从 .NET 框架提供的数据到你创建的自定义类型。该系统使用 `Session` 或 `Application` 对象更具活性和扩展性。数据通过 ASP.NET 自带的几个内置个性化提供程序进行存储。这些提供程序包括连接 SQL Server Express 版或 SQL Server 2008、2005、2000 或 7.0 的提供程序。

### 总结

你还可以使用 `ProfileManager` 类来管理系统的配置文件信息。这包括根据你的需要监控和删除配置文件的能力。

## 598 | 第 15 章 成员与角色管理

在查看 ASP.NET 4 的成员和角色管理功能之前，理解身份验证和授权的基本原理至关重要。以下是相关内容的快速回顾：

- 身份验证（Authentication）是一个确定用户身份的过程。在用户通过身份验证后，开发者可以确定被识别出的用户是否有权限继续操作。在应用后续过程后向实体授予授权。ASP.NET 4 使用成员服务（membership service）提供身份验证。
- 授权（Authorization）是确定已验证的用户是否允许访问应用程序的任何部分或访问应用程序提供的特定数据集的过程。当你对用户或组进行身份验证和授权时，你可以根据用户类型或偏好自定义站点。ASP.NET 4 使用角色管理服务（role management service）提供授权。

## ASP.NET 4 身份验证

ASP.NET 4 提供了成员服务来处理用户访问页面或整个网站的身份验证。ASP.NET 管理服务不仅提供了用于管理用户的 API 接口，还提供了与此 API 配合运行的服务器控件。这些服务器控件通过身份验证过程与最终用户交互。稍后我们将查看这些控件的功能。

## 为你的网站设置成员资格服务

在使用 ASP.NET 4 提供的安全控件之前，你必须先配置应用程序以与成员服务配合。这取决于你如何处理安全框架。

默认情况下，ASP.NET 4 使用内置的 `SqlMembershipProvider` 实例来设置应用程序注册用户的详细信息。对于初始演示，本章的示例基于表单的身份验证（forms-based authentication）。你可以假设这些示例中的应用程序位于公共互联网上，因此对外开放注册和查看。如果是基于局域网的应用程序（意味着所有用户都在私有网络上），可以使用 Windows 集成验证（Windows Integrated Authentication）来验证用户。

如你所知，ASP.NET 4 提供了一种数据提供程序模型，处理与多种类型的底层数据存储交互所需的详细信息。图 15-1 显示了 ASP.NET 4 成员服务的图。

![](img/7040c21013b8e6c23c612d6da3599ff8_657_0.png)

图 15-1

## ASP.NET 身份验证 | 599

从图中可以看到，其余的 ASP.NET 提供程序模型可以访问各种底层数据存储。在图中，你可以看到内置的 Microsoft SQL Server 数据。你也可以构建自己的成员提供程序，以访问任何带有用户凭据的自定义数据存储。在图中成员提供程序的正上方，你可以看到一组关注安全的服务器控件，这些控件利用成员提供程序授予的权限在身份验证过程中与用户进行交互。

## 在 web.config 文件中添加 <authentication> 元素

为了让你在带有成员服务的 Web 应用程序中使用表单身份验证元素，第一步是在 `web.config` 文件中启用表单身份验证。执行此操作，请创建一个 `web.config` 文件（如果你的应用程序中还没有该文件）。接下来，将列表 15-1 所示的节添加到此文件中。

列表 15-1：向 `web.config` 文件添加属性

```xml
<xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <authentication mode="Forms" />
  </system.web>
</configuration>
```

在 `web.config` 文件中简单地添加 `<authentication>` 元素即可启动由 ASP.NET 4 提供的成员服务所需的所有内容。要使用此元素启用表单身份验证，只需为 `mode` 属性赋值。这是一个表单身份验证示例，但 `mode` 属性的其他可能值包括 Windows、Passport 或 None。

IIS 身份验证方案包括基本（basic）、摘要（digest）和集成 Windows 验证。Passport 身份验证指向由微软提供的中央服务，该服务为任何成员提供单一登录和核心配置服务。使用 Passport 需要付费，且它已被微软弃用。

由于我们示例中的 `mode` 属性被设置为 Forms，你可以继续下一步添加用户数据存储。此时，你也可以通过对 `web.config` 文件进行一些修改来更改表单身份验证系统的行为。接下来将介绍这些可能性。

## 在 web.config 文件中添加 <forms> 元素

使用表单身份验证，你可以根据用户在 Web 表单中输入的凭据为其提供访问站点或材料。当最终用户尝试访问 Web 站点时，他使用的是匿名身份验证进入站点，这是默认的身份验证模式。如果发现他是匿名的，可以将其重定向（ASP.NET）到指定的登录页面。在最终用户输入正确的登录信息并通过身份验证后，他将获得一个 HTTP cookie，该 cookie 将用于任何后续请求。

你可以通过在 `web.config` 文件的 `<forms>` 节中定义该行为来修改表单身份验证的行为。你可以在列表 15-2 中看到表单身份验证设置的可能性，该列表显示了 `web.config` 文件中该节的可能更改。

列表 15-2：修改表单身份验证行为

```xml
<xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <authentication mode="Forms">
      <forms name="ASPXAUTH"
            loginUrl="Login.aspx"
            protection="All" />
    </authentication>
  </system.web>
</configuration>
```

## 列表 15-2（继续）

```xml
<xml version="1.0" encoding="utf-8"?>
<configuration>
  <system.web>
    <authentication mode="Forms">
      <forms name="ASPXAUTH"
            loginUrl="Login.aspx"
            protection="All"
            timeout="30"
            path="/"
            requireSSL="false"
            slidingExpiration="true"
            cookies="UseDeviceProfile" />
    </authentication>
  </system.web>
</configuration>
```

你可以根据需要设置这些值，并且选项比显示的要得多。此外，如前所述，这些值不是强制的。你可以按照 15-1 所示的配置立即使用成员服务。以下列表描述了 `<element>` 的属性：

- name：定义身份验证后发送给用户的 cookie 名称。默认情况下此 cookie 为 AUTH。
