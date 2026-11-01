
_(续)_

| 控制 | 描述 |
|---|---|
| `LoginName` | 此控件输出当前已登录用户的用户名。 |
| `CreateUserWizard` | 此控件显示一个表单，用户可通过该表单注册到您的网站并加入用户列表。与其他登录控件一样，存在大量与布局格式相关的属性，但默认设置完全可用。 |
| `ChangePassword` | 此控件使用户能够更改其密码。有三个字段，分别是旧密码、新密码和确认密码。存在许多样式属性。 |

你可以在“PCSDemoSite 中的安全性”部分看到其中一些的实际应用。

## 保护目录

最后要讨论的一个问题是如何限制对目录的访问。你可以通过前面提到的站点配置工具来实现，但实际上自己操作也非常容易。

在 PCSAuthenticationDemo 中添加一个名为 `SecureDirectory` 的目录，以及该目录中的一个 `Default.aspx` 网页和一个新的 web.config 文件。用以下内容替换 web.config 的内容：

```xml
<?xml version="1.0" ?>
<configuration>
  <system.web>
    <authorization>
      <deny users="?" />
      <allow roles="Administrator" />
      <deny roles="User" />
    </authorization>
  </system.web>
</configuration>
```

_代码片段 PCSAuthenticationDemo/SecureDirectory/web.config_

`<authorization>` 元素可以包含一个或多个表示权限规则的 `<deny>` 或 `<allow>` 元素，每个元素都可以有一个 users 或 roles 属性，说明该规则适用于谁。规则从上到下应用，因此如果规则的成员资格重叠，则更具体的规则通常应靠近顶部。在此示例中，`?` 指匿名用户，他们将被拒绝访问此目录，连同 User 角色中的用户一起。请注意，同时具有 User 和 Administrator 角色的用户只有在本文所示的 `<allow>` 规则位于 User 角色的 `<deny>` 规则之前时才会被允许访问——所有用户的角色都会被考虑在内，但规则顺序仍然适用。

现在，当你登录网站并尝试导航到 `SecureDirectory/Default.aspx` 时，只有在你属于 Admin 角色时才会被允许。其他用户或未通过身份验证的用户将被重定向到登录页面。

## PCSDemoSite 中的安全性

PCSDemoSite 站点使用了你已经见过的 Login 控件，以及 LoginView 控件、LoginStatus 控件、LoginName 控件、PasswordRecovery 控件和 ChangePassword 控件。

一个区别是包含了一个 Guest 角色，其结果之一是访客用户不应能够更改其密码——这正是 LoginView 的理想用途，如 Login.aspx 所示：

```aspx
<asp:Content ID="Content1" ContentPlaceHolderID="ContentPlaceHolder1"
    Runat="server">
    <h2>Login Page</h2>
<asp:LoginView ID="LoginView1" runat="server">
<RoleGroups>
<asp:RoleGroup Roles="Guest">
<ContentTemplate>
You are currently logged in as <br>
<asp:LoginName ID="LoginName1" runat="server" /></br>.
<br />
<br />
<asp:LoginStatus ID="LoginStatus1" runat="server" />
</ContentTemplate>
</asp:RoleGroup>
<asp:RoleGroup Roles="RegisteredUser,SiteAdministrator">
<ContentTemplate>
You are currently logged in as <br>
<asp:LoginName ID="LoginName2" runat="server" /></br>.
<br />
<br />
<asp:ChangePassword ID="ChangePassword1" runat="server">
<br />
<br />
<asp:LoginStatus ID="LoginStatus2" runat="server" />
</ContentTemplate>
</asp:RoleGroup>
</RoleGroups>
<AnonymousTemplate>
<asp:Login ID="Login1" runat="server">
</asp:Login>
<asp:PasswordRecovery ID="PasswordRecovery1" runat="Server" />
</AnonymousTemplate>
</asp:LoginView>
</asp:Content>
```

代码片段 PCSAuthenticationDemo/Login.aspx

此处视图显示多个页面之一：

- 对于匿名用户，会显示 `Login` 和 `PasswordRecovery` 控件。
- 对于 Guest 用户，会显示 `LoginName` 和 `LoginStatus` 控件，提供已登录的用户名以及在需要时注销的功能。
- 对于 `RegisteredUser` 和 `SiteAdministrator` 用户，会显示 `LoginName`、`LoginStatus` 和 `ChangePassword` 控件。

该站点还在各个目录中包含各种 web.config 文件以限制访问，并且导航也按角色受限。

> *请注意，站点的配置用户显示在 About 页面上，或者你可以添加自己的用户。基础站点中的用户（及其密码）为 User1 (User1!!)、Admin (Admin!!!) 和 Guest (Guest!!)。*

这里需要注意的一点是，尽管站点的根目录拒绝匿名用户，但 Themes 目录（在下一节中描述）通过允许匿名用户来覆盖此设置。这是因为如果没有这样做，匿名用户将看到一个无主题的站点，因为主题文件将无法访问。此外，根 web.config 文件中的完整安全规范如下：

```xml
<location path="Stylesheet.css">
<system.web>
<authorization>
<allow users="*"/>
</authorization>
</system.web>
</location>
<system.web>
  <authorization>
    <deny users="?" />
  </authorization>
</system.web>
```

*代码片段 PCSDemoSite/web.config*

这里使用 <location> 元素通过 path 属性为特定文件覆盖默认设置，在本例中为文件 StyleSheet.css。<location> 元素可用于将任何 <system.web> 设置应用于特定文件或目录，如果需要，还可用于将所有目录特定设置集中在一处（作为多个 web.config 文件的替代方案）。在前面的代码中，允许匿名用户访问网站的根样式表，这是必要的，因为该文件定义了主页面中 <div> 元素的布局。如果没有这样做，匿名用户登录页面上显示的 HTML 将难以阅读。

另一个需要注意的点是在会议室预订用户控件的代码隐藏文件中，在 Page_Load() 事件处理程序中：

```csharp
void Page_Load(object sender, EventArgs e)
{
    if (!this.IsPostBack)
    {
        nameBox.Text = Context.User.Identity.Name;
        DateTime trialDate = DateTime.Now;
        calendar.SelectedDate = GetFreeDate(trialDate);
    }
}
```

*代码片段 PCSDemoSite/MRB/MRB.ascx.cs*

这里用户名是从当前上下文中提取的。请注意，在你的代码隐藏文件中，你可能也会经常使用 Context.User.IsInRole() 来检查访问权限。

## 主题

通过将 ASP.NET 页面与母版页和 CSS 样式表结合使用，你可以在很大程度上分离形式和功能，从而使页面的外观与操作分开定义。使用主题，你可以更进一步，从你自己提供的多个主题中动态应用这种外观。

一个主题包含以下内容：

- 主题名称
- 可选的 CSS 样式表
- 允许对单个控件类型进行样式设置的 Skin（.skin）文件

这些可以通过两种不同的方式应用于页面——使用 Theme 或 StyleSheetTheme 属性：

- **Theme** — 所有皮肤属性都应用于控件，覆盖页面上控件可能已有的任何属性。
- **StyleSheetTheme** — 现有控件属性优先于皮肤文件中定义的属性。

CSS 样式表的工作方式相同，无论使用哪种方法，因为它们以标准的 CSS 方式应用。

### 将主题应用于页面

你可以通过多种方式将主题应用于页面，声明式或编程式。应用主题最简单的声明式方法是使用 Theme 或 StyleSheetTheme 属性通过 <%@ Page %> 指令：

```
<%@ Page Theme="myTheme" ... %>
```

or:

```
<%@ Page StyleSheetTheme="myTheme" ... %>
```

这里 myTheme 是为主题定义的名称。

或者，你可以使用网站 web.config 文件中的条目指定站点中所有页面使用的主题：

```
<configuration>
  <system.web>
    <pages Theme="myTheme" />
  </system.web>
</configuration>
```

这里你也可以使用 Theme 或 StyleSheetTheme。你还可以使用 <location> 元素通过更具体的设置来覆盖单个页面或目录的此设置，就像本节前面用于安全信息时使用该元素一样。

以编程方式，你可以在页面的代码隐藏文件中应用主题。唯一允许这样做的地方——在 Page_PreInit() 事件处理程序中，该事件在页面的生命周期中非常早时触发。在此事件中，你只需将 Page.Theme 或 Page.StyleSheetTheme 属性设置为要应用的主题的名称，例如：

```
protected override void OnPreInit(EventArgs e)
{
    Page.Theme = "myTheme";
}
```

因为你使用代码来执行此操作，所以你可以从一组主题中动态应用主题文件。这种技术在“PCSDemoSite 中的主题”部分中使用。

### 定义主题

主题在 ASP.NET 中的另一个“特殊”目录中定义——在本例中为 App_Themes。App_Themes 目录可以包含任意数量的子目录，每个主题一个，其中子目录的名称定义了主题的名称。

定义主题涉及将主题所需的文件放在主题子目录中。对于 CSS 样式表，你不必担心文件名；主题系统只需查找具有 .css 扩展名的文件。同样，.skin 文件可以有任何文件名，尽管建议你使用多个 .skin 文件，每个要皮肤的控件类型一个，并且每个都以其皮肤的控件命名。

皮肤文件包含服务器控件定义，其格式与你在标准 ASP.NET 页面中使用的格式完全相同。不同之处在于，皮肤文件中的控件永远不会添加到你的页面中；它们只是用于提取属性。一个按钮皮肤的定义，通常放在名为 Button.skin 的文件中，可能如下所示：

```
<asp:Button runat="server" BackColor="#444499" BorderColor="#000000" ForeColor="#ccccff" />
```

此皮肤实际上取自 PCSDemoSite 中的 DefaultTheme 主题，并负责本章前面看到的会议室预订页面上按钮的外观。

当你以这种方式为控件类型创建皮肤时，你不使用 ID 属性。
