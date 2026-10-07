
- `loginUrl`：指定无有效 cookie 时重定向的路径。默认是 `Login.aspx`。

- `protection`：指定对身份验证后存储在最终用户机器上的 cookie 应用的保护程度。可能的设置包括 `All`、`None`、`Encryption` 和 `Validation`。你应该始终尝试使用 `All`。

- `timeout`：定义 cookie 过期的时间（分钟）。默认值为 30。

- `path`：指定应用程序使用的 cookie 路径。

- `requireSSL`：定义是否要求通过加密布线（SSL）而不是明文发送凭据。

- `slidingExpiration`：指定 cookie 的超时时间是否为滑动比例。默认值为 `true`。这意味着在最后一次请求应用程序后的 30 分钟（或 `timeout` 属性指定的持续）内，用户 cookie 不过期。如果 `slidingExpiration` 属性的值设置为 `false`，则 cookie 在第一次请求后 30 分钟过期。

- `cookies`：指定 ASP.NET 如何处理 cookie。可能的值包括 `UseDeviceProfile`、`UseCookies`、`AutoDetect` 和 `UseUri`。默认值为 `UseDeviceProfile`。它检测 cookie 是否基于设备代理程序。`UseCookies` 要求所有请求都带有 cookie 中的凭据。`AutoDetect` Determine 详细信息是存储在客户端 cookie 中还是 URI 中（通过发送测试 cookie 实现）。最后，`UseUri` 强制 ASP.NET 在所有实例中使用 URI 存储详细信息。

## 添加用户

要向成员服务添加用户，可以将用户注册到 Microsoft SQL Server Express 数据存储中。你提出的第一个问题可能是：“这个数据存储在哪里？”

# ASP.NET 4 身份验证

> 当然，你可以使用多个版本的 Microsoft SQL Server 来完成本书中的示例。尽管如此，本章在创建用户时使用了默认的成员身份系统。

用于成员系统的 Microsoft SQL Server 履行程序可以使用专门为成员服务结构化的 SQL Server 表达式文件（Expression file）（以及其他 ASP.NET 系统，如角色管理系统）。如果相应的文件尚不存在，ASP.NET 设置为自动为你创建此特定文件。要创建 `ASPNETDB.mdf` 文件，请使用利用成员服务某个方面的 ASP.NET 服务器控件。当应用程序需要 `ASPNETDB.mdf` 文件时，ASP.NET 会在 `App_Data` 文件夹中为你创建该文件。

数据存储到位后，就可以开始向数据存储中添加用户了。

# 使用 CreateUserWizard 服务器控件

`CreateUserWizard` 服务器控件可以配合成员服务使用。你可以在 Visual Studio 2010 工具箱的登录（Login）部分找到本章提到的此或其他控件。`CreateUserWizard` 控件允许你将注册的用户插入你的数据存储中，以备日后检索。如果你在应用程序中放置一个允许用户注册网站的页面，你至少需要从用户处获取登录名和密码，并将这些值存入数据存储中。这使得终端用户以后可以使用成员系统访问应用程序中的各项项。

为了让你的工作尽可能简单，`CreateUserWizard` 控件会代表你完成整个注册过程。图 15-3 显示了控件的简单用法。

### 列表 15-3：允许用户注册网站

```
<%@ Page Languages="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head run="server">
<title>Creating Users</title>
</head>
<<body>
<form id="form1" runat="server">
<asp:CreateUserWizard Id="CreateUserWizard" Runat="server"
BorderWidth="1px" BorderColor="#FFD0AD" BorderStyle="Solid"
BackColor="#FFB6D6" FontName="Verdana">
<TextStyle FontBold="True" BackgroundColor="#990000"
ForegroundColor="White"/>
</TextStyle>
</asp:CreateUserWizard>
</form>
</body>
</html>
```

此页面仅显示了 `CreateUserWizard` 控件，没有其他内容。此控件允许为你的 Web 应用程序注册终端用户。这个特定的 `CreateUserWizard` 控件应用了一些样式，但该控件可以简单到：

```
<asp:CreateUserWizard Id="CreateUserWizard" Runat="server">
</asp:CreateUserWizard>
```

当运行此代码时，终端用户将看到图 15-2 所示的表单。

# 602 | 第15章 成员身份与角色管理

![](img/7040c21013b8e6c23c612d6da3599ff8_661_0.png)

图 15-2

此截图显示了终端用户填写表单后的样子，包括用户名、密码、电子邮件地址以及安全问题问答部分。点击“创建用户”（Create User）按钮会将这些定义的用户信息存入数据存储中。

通过此控件提供的用户名和密码允许终端用户以后通过登录服务器控件登录应用程序。`CreateUser` 控件的表单中包含一个“确认密码”（Confirm password）文本框，以确保（以防用户忘记登录凭据并希望在以后某个时间将凭据通过电子邮件发送给他们）。最后包含了电子邮件文本框，安全问题和答案用于在通过浏览器更改或修改任何凭据或用户信息之前验证终端用户的身份。

终端用户点击此表单上的“创建用户”按钮后，将显示信息存储的确认（参见图 15-3）。

![](img/7040c21013b8e6c23c612d6da3599ff8_661_1.png)

图 15-3

# 查看用户存储的位置

现在你已经使用 `CreateUserWizard` 控件向成员服务添加了用户，让我们看看这些信息存储在何处。如果你使用 Visual Studio 创建了存储用户信息的 Microsoft SQL Server 版本文件，该文件会在运行上一个示例并你按照前几个图所示完成表单时被创建。当示例运行并完成后，你可以点击解决方案资源管理器中的“刷新”按钮来找到 `ASPNET.sdf` 文件，它位于项目的 `App_Data` 文件夹中。该文件中包含许多不同的表，但你感兴趣的是 `asp_Membership` 表。

当你打开 `asp_Membership` 表（通过在解决方案资源管理器中右键单击表并选择“显示表数据”）时，你输入的用户已在系统中，如图 15-4 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_662_0.png)

图 15-4

表中的用户密码不是以明文存储的；而是经过哈希处理的，这是一种无法轻易反向的单向加密形式。

# 604 | 第15章 成员身份与角色管理

### 列表 15-4：修改 web.config 中的成员履行程序

```
<configuration>
  <system.web>
    <membership>
      <providers>
        <clear />
        <add name="ASNetSqlProvider,System.Web,
             Version=4.0.0,Culture=neutral,
             connectionString="ApplicationServices"
             enablePasswordRetrieval="false"
             enablePasswordSheet="true"
             requiresQuestionAnswer="false"
             uniqueEmail="true"
             passwordFormat="Hashed"
             minRequiredAlphanumeric="0"
             minRequiredLength="3" />
      </providers>
    </membership>
  </system.web>
</configuration>
```

# 使用 CreateUserWizard 控件

当你使用 `CreateUserWizard` 控件时，请注意 `ContinueButtonClick()` 事件和 `CreatedUser()` 事件。`ContinueButtonClick()` 事件在成功用户后点击第二页上的“继续”按钮时触发（参见列表 15-5）。

### 列表 15-5：ContinueButtonClick 事件

```VB
Protected Sub CreateUserWizard_ContinueButtonClick(ByVal sender As Object, ByVal e As System.EventArgs)

  Response.Redirect("Default.aspx")

End Sub
```

```csharp
protected void CreateUserWizard_ContinueButtonClick(object sender, EventArgs e)
{
  Response.Redirect("Default.aspx");
}
```

当用户在数据存储中成功创建时，会触发 `CreatedUser()` 事件。列表 15-6 显示了该事件的使用。

### 列表 15-6：CreatedUser() 事件

```vb
VB Protected Sub CreateUserWizard1_CreatedUser(ByVal sender As Object, ByVal e As System.EventArgs)

' 代码在此处
End Sub

C# protected void CreateUserWizard1_CreatedUser(object sender, EventArgs e)
{
    // 代码在这里
}
```

如果你想在用户注册到服务时执行任何额外操作，请使用此事件。

### 在注册过程中结合个性化属性

正如你在前一节关于个性化的章节中所看到的，使用 ASP.NET 自带的个性化管理系统并存储用户特定的详细信息非常简单。`CreateUser` 控件提供的注册过程是从用户处检索这些信息并直接存储在个性化系统中的理想位置。将检索过程整合到你的代码中并不困难。

正如你在上一节关于个性化的章节中所学习的，第一步是在应用程序的 `web.config` 文件中定义一些个性化点，如列表 15-7 所示。

### 列表 15-7：在 web.config 文件中创建个性化属性

```xml
<configuration>
  <system.web>
    <profile>
      <add name="FirstName" />
      <add name="LastName" />
      <add name="LastVisited" />
      <add name="Age" />
      <add name="Member" />
    </profile>
  </system.web>
</configuration>
```

现在由于这些属性已经在 `web.config` 文件中定义，你就可以在 ASP.NET 成员系统中创建用户时使用它们。同样，使用 `CreateUser` 控件，你可以控制一个需要用户在第一步输入其首选用户名和密码的过程，然后在第二步询问这些自定义的个性化点。列表 15-8 显示了一个结合此想法的 `CreateUser` 控件。

### 列表 15-8：使用 CreateUserWizard 控件使用个性化属性

```asp
<@ Page Language="VB" %>
```

```vb
<script runat="server">
Protected Sub CreateUserWizard1_CreatedUser(ByVal sender As Object, ByVal e As System.EventArgs)
Dim pc As ProfileCommon = New ProfileCommon()
pc.Initialize(CreateUserWizard1.UserName.ToString(), True)
pc.FirstName = FirstName.Text
pc.LastName = LastName.Text
pc.Age = Age.Text
pc.Save()
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head id="Head" runat="server">
<title>使用个性化创建用户</title>
</head>
<body>
<form id="form" runat="server">
<asp:CreateUserWizard Id="CreateUserWizard1" runat="server"
BorderWidth="1px" BorderColor="#FFADAD" BorderStyle="Solid"
BackgroundColor="#FFFEF6" FontName="Verdana"
LoginUserServer="true" OnCreated="CreateUserWizard1_CreatedUser">
<WizardSteps>
<asp:CreateUserWizardStep Id="WizardStep1" Runat="server" 
Title="附加信息" StepType="Start">
<table width="100%">
<tr>
<td>FirstName:</td><td>
<asp:TextBox Id="FirstName" Runat="server"></asp:TextBox>
</td>
</tr>
<tr>
<td>LastName:</td><td>
<asp:TextBox Id="LastName" Runat="server"></asp:TextBox>
</td>
</tr>
<tr>
<td>Age:</td><td>
<asp:TextBox Id="Age" Runat="server"></asp:TextBox>
</td>
</tr>
</table>
</asp:CreateUserWizardStep>
<asp:CreateUserWizardStep Runat="server"
Title="为您的新账户注册">
</asp:CreateUserWizardStep>
<asp:CompleteUserWizardStep Runat="server" Title="完成" />
</asp:CompleteUserWizardStep>
</WizardSteps>
<StepStyle BorderColor="#FFADAD" FontName="Verdana"
BackgroundColor="#FFFEF6" BorderStyle="Solid"
BorderWidth="1px"/></StepStyle>
<TitleStyle Font-Bold="True" BackgroundColor="#990000"
ForegroundColor="White"/></TitleStyle>
</asp:CreateUserWizard>
</form>
</body>
</html>
```

```csharp
<script runat="server">
protected void CreateUserWizard_Created(object sender, EventArgs e)
{
    ProfileCommon pc = new ProfileCommon();
    pc.Initialize(CreateUserWizard1.Username.ToString(), true);
    pc.FirstName = FirstName.Text;
    pc.LastName = LastName.Text;
    pc.Age = Age.Text;
    pc.Save();
}
</script>
```

通过此更改，标准的注册过程由请求存储的属性的默认实例和 `CreateUserWizard` 定义，你的注册系统现在包含了从 `ProfileCommon` 对象存储和检索的属性。然后，使用 `ProfileCommon.Initialize()` 方法，它会初始化当前用户的属性值。接下来，你通过对 `ProfileCommon` 对象可用属性的强类型访问来设置属性值。在设置所有值后，你使用 `Save()` 方法完成最后。

610 | 第 15 章 成员与角色管理

# 列表 15-9（续）

```html
<p>
  <asp:Label ID="Label1" Runat="server"/></asp:Label>
</p>
</form>
```
