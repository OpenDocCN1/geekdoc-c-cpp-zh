
该服务的一个功能是你可以显示此时此刻有多少用户在线。对于希望访客通过其人气气来访问的门户网站或论坛来说，这是一个特别受欢迎的选项。

要显示在线用户数，你使用 `Membership` 类提供的 `GetNumberOfUsersOnline` 方法。你可以按照列表 16-20 所示的代码添加图 16-10 所示的 Default.aspx 页面。

### 16-20：显示在线用户数

```vb
<# Page Language="VB" %>
<script runat="server">
  Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Label1.Text = Membership.GetNumberOfUsersOnline().ToString()
  End Sub
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>登录或注销</title>
</head>
<body>
  <form id="form1" runat="server">
  <asp:LoginStatus ID="LoginStatus" runat="server" />
  <asp:Label ID="Label1" runat="server" />
  </form>
</body>
</html>
```

*(注：原文代码块中 16-20 的第一行标记为 `<#` 似为笔误，翻译时已根据上下文保留其逻辑)*

## 第 16 章：成员资格与角色管理

### 列表 16-22：在 web.config 文件中配置通过电子邮件发送密码

```xml
<configuration>
  <system.web>
    <!-- 为了清晰起见已移除 -->
  </system.web>

  <system.net>
    <mailSettings>
      <smtp from="someuser@email.com">
        <network host="localhost" port="25"
        defaultCredentials="true" />
    </mailSettings>
  </system.net>
</configuration>
```

设置好 `mailSettings` 元素后，你就可以开始使用 `PasswordRecovery` 控制了。列表 16-23 显示了 `PasswordRecovery` 控制的简单用法。

### 列表 16-23：使用 `PasswordRecovery` 控制

```asp
<@ Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>获取您的密码</title>
</head>
<body>
<form id="form1" runat="server">
<asp:PasswordRecovery Id="PasswordRecovery1" runat="server">
<MailDefinition From="someuser@email.com">
</MailDefinition>
</asp:PasswordRecovery>
</form>
</body>
</html>
```

`<asp:PasswordRecovery>` 元素需要一个 `<MailDefinition>` 子元素。`MailDefinition` 元素包含了要发送给终端用户的电子邮件详细信息。最低要求是使用 `From` 属性，它提供了邮件“发件人”部分的电子邮件地址。该属性的 `String` 值应该是一个电子邮件地址。`MailDefinition` 元素的其他属性包括：

- BodyFileName
- CC
- From
- IsBodyHtml
- Priority
- Subject

当你运行此页面时，`PasswordRecovery` 控制会要求用户输入用户名，如图 16-17 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_827_0.png)

图 16-17

当获取用户名后，成员资格服务将检索终端用户之前输入的的问题和答案，并生成如图 16-18 所示的视图。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_827_1.png)

图 16-18

如果问题回答正确（注意答案对大小写敏感），将生成包含包含密码的电子邮件并发送给终端用户。如果回答错误，则会显示错误消息。当然，如果你禁用了成员系统的“问题/答案”功能，将不会使用问题。

为了使整个过程生效，更改成员资格服务的设置非常重要。目前，由于用户密码的哈希处理方式，它无法工作。成员资格服务数据存储没有存储实际密码——只是其哈希版本。当然，对任何用户来说，接收哈希密码都是没有意义的。

为了能够向用户发送实际密码，你必须更改成员资格服务数据存储中存储密码的方式。正如本章所述，这通过更改成员数据提供程序的 `Passwordformat` 属性来实现。除了 `Hashed`（哈希）之外，其他可能的值还有 `Clear`（明文）和 `Encrypted`（加密）。将值改为 `Clear` 或 `Encrypted` 就可以以可读格式将密码发送给用户。

## 生成随机密码

某些应用程序在创建用户时必须生成随机密码。在 ASP.NET 1.0/1 时代，这是你需要自己编写的代码。另一方面，ASP.NET 2.0 和 3.5 包含一个允许你检索随机密码的辅助方法。列表 16-24 显示了创建一个提取随机密码的辅助方法的示例。

```vb
Protected Function GeneratePassword() As String
  Dim returnPassword As String
  returnPassword = Membership.GeneratePassword(10, 3)

  Return returnPassword
End Function
```

```csharp
protected string GeneratePassword()
{
    string returnPassword;
    returnPassword = Membership.GeneratePassword(10, 3);

    return returnPassword;
}
```

在 ASP.NET 2.0 或 3.5 中随机生成密码，可以使用 `GeneratePassword()` 辅助方法。该方法允许你生成指定长度的随机密码，并且你可以指定密码至少包含多少个非字母数字字符。该方法利用五次来产生此处的结果（当然，你的结果将是）：

- [D]Xq6s[
- $[M9]*x2-
- Q+1Iy2#D\%
- %KWZL@zy&f
- o&IhL#U1

有了你的辅助方法，你可以像列表 16-25 所示创建带有随机密码的用户。

```vb
Membership.CreateUser(TextBox1.Text, GeneratePassword().ToString())
```

```csharp
Membership.CreateUser(TextBox1.Text, GeneratePassword().ToString());
```

## ASP.NET 3.5 授权

处理完访问 Web 应用程序的用户注册和验证后，下一步是授权。他们被允许查看什么？他们承担什么角色？这些对于任何 Web 应用程序都是重要的。首先学习向已验证用户显示某些项目，同时向未验证用户显示不同的项目。

## 使用 LoginView 控件

`LoginView` 控件允许你控制页面特定部分的视图。使用 `LoginView` 控制，你可以规定哪些部分是给已验证用户的，哪些部分是给未验证用户的。列表 16-26 显示了此示例。

### 列表 16-26：通过 LoginView 控制控制视图

```asp
<%@ Language="VB" %>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>获取您的密码</title>
</head>
<body>
<form id="form1" runat="server">
<asp:PasswordRecovery Id="PasswordRecovery1" runat="server">
<MailDefinition From="someuser@email.com">
</MailDefinition>
</asp:PasswordRecovery>
</form>
</body>
</html>
```

## 第 16 章：成员与角色管理

本章涵盖了应用程序身份验证的所有细节，而角色管理服务则负责授权。正如成员服务可以使用之前列出的任何数据提供程序一样，角色管理服务也可以使用专注于 SQL Server 的提供程序（`SqlRoleProvider`）或任何自定义提供程序。事实上，该服务在许多方面与成员服务是可以相拟的。图 16-21 显示了一个详细说明角色管理服务若干细节的简单图。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_832_0.png)

图 16-21

## 修改 `<roleManager>` 节

使用角色管理服务的第一步是在 `machine.config` 或 `web.config` 文件中更改角色管理提供程序的任何行为。如果你查看 `machine.config` 文件，将看到一个专门处理角色管理服务的节（参见见列表 16-28）。

### 列表 16-28：machine.config 文件中的角色管理提供程序设置

```xml
<roleManager
enabled="false"
cacheRolesInCookie="false"
cookieName="*.ASPXROLES"
cookieTimeout="30"
cookiePath="/*"
cookieRequireSSL="false"
cookieSlidingExpiration="true"
cookieProtection="All"
defaultProvider="AspNetNetSqlRoleProvider" />
```

```xml
createPersistentCookie="false"
maxCachedResults="25"
<providers>
  <clear />
  <add connectionString="LocalSqlServer" applicationName="AspNetNetSqlProvider" type="System.Web.SqlProvider,System.Web,2.0.0,Culture=neutral,PublicKeyToken=b035f7f7f11d50a3" />
  <add applicationName="AspNetNetWindowsTokenProvider" name="AspNetWindowsTokenProvider" type="System.Web.Security.WindowsTokenProvider,System.Web,Version=2.0.0,Culture=neutral,PublicKeyToken=b035f7f7f11d50a3" />
</providers>
</roleManager>
```

角色管理服务在 `machine.config` 文件中定义其设置，如之前的代码列表所示。你可以直接在 `machine.config` 文件中更改这些设置，或者通过更改 `web.config` 文件来覆盖你可能拥有的任何高级别设置（从而仅对特定应用程序进行更改）。

主要设置定义在 `<roleManager>` 元素中。`<roleManager>` 元素的某些属性定义在下表中。

| 属性 | 描述 |
| --- | --- |
| enabled | 定义是否为应用程序启用角色管理服务。此属性接受一个布尔值，默认设置为 False。这意味着默认情况下角色管理服务是禁用的。这样做是为了避免从 ASP.NET 1.0/1.1 迁移到 ASP.NET 2.0 或 3.5 时发生破坏性更改。因此，你必须首先在 `machine.config` 或 `web.config` 中将此值更改为 True。 |
| cacheRolesInMemory | 定义是否可以将用户的角色存储在客户端机器的 cookie 中。此属性接受一个布尔值，默认设置为 True。在理想情况下，从 cookie 中检索角色可以防止 ASP.NET 通过角色管理提供程序查找用户角色。如果你希望为所有实例检索角色，请将其设置为 False。 |
| cookieName | 定义用于发送到客户端以存储角色管理信息的 cookie 的名称。默认情况下，此 cookie 名为 .ASPXROLES，你可能不会更改它。 |
| cookieTimeout | 定义 cookie 过期后的时间（分钟分钟）。默认值为 30 分钟。 |
| cookieRequireSSL | 定义是否要求角色管理信息通过加密通道（SSL）发送，而不是以明文形式发送。默认值为 False。 |
| cookieExpiration | 指定 cookie 的超时是否基于滑动刻度。默认值为 True。这意味着在用户向应用程序发送最后一次请求后，在未达到 30 分钟（或 `cookieTimeout` 属性中指定的时间）之前，用户的 cookie 永远不会过期。如果 `cookieSlidingExpiration` 属性的值为 False，则 cookie 将从第一次请求起 30 分钟后过期。 |
| createPersistentCookie | 指定 cookie 是过期还是无限期。默认设置为 False，因为出于安全考虑，不建议使用持久性 cookie。 |
| cookieProtection | 指定你希望对存储在用户机器上用于管理信息的 cookie 的保护程度。可能的设置包括 All（全部）、None（无）、Encryption（加密）和 Validation（验证）。 |
| defaultProvider | 定义用于角色管理服务的提供程序。默认设置为 AspSqlClientProvider。 |

## 修改 web.config

下一步是配置你的 `web.config` 文件，使其与角色管理服务配合。应用程序的某些页面或子节可能仅限特定角色的人员访问。为了管理此，请在 `web.config` 文件中定义访问权限。必要的更改如列表 16-29。

### 列表 16-29：更改 web.config 文件
