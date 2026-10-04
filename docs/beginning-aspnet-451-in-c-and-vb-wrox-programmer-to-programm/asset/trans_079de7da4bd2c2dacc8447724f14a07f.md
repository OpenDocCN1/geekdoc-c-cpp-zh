
通过此配置，ASP.NET 运行时将在用户需要提供凭据时从网站根目录下的 Account 文件夹中加载 LoginPage.aspx 页面。

> **注意：** 如果您安装了 ASP.NET FriendlyUrls 包（第 7 节已讨论），您需要将 `loginUrl` 配置为 `/Login/` 而不是默认的 `~/Login.aspx`。如果您不进行此更改，Login 控件将无法包含 Login 控件的页面与配置的 Login URL 之间找到精确匹配。这反过来会导致在用户登录后将用户重定向回原始请求页的功能失效。您将在下一个练习中学习如何配置此项。

关于登录页面（在 `loginUrl` 属性中配置），Login 控件的 `VisibleLoggedIn` 属性不起作用。在配置的登录页面上，Login 控件始终是可见的。如果您想将其作为登录控件使用，正如您在随后的练习中看到的。

除了这些属性外，Login 控件有一系列 `Text` 属性，例如 `LoginButtonText`、`RememberText`、`TitleText` 和 `UserNameLabelText`，用于设置在控件及其各种子控件（如构成用户界面的 Button 和 Label 控件）中显示的文本。

与数据绑定控件一样，登录控件也拥有许多样式属性，允许您调整其外观。鼓励您检查控件属性格中的 `Styles` 类别，以查看如何设置样式选项。请记住，您可以将大部分样式信息移动到皮肤文件和 CSS 文件中。

Login 控件还暴露了一些您通常不需要处理的事件，但有时会派上用场。例如，`isLoggedIn` 事件在用户登录成功后立即触发，如果 `DestinationUrl` 不够灵活，它是动态地将用户发送到另一个页面的良好位置。

# LoginView

LoginView 是一个实用的控件，允许您为不同的用户显示不同的数据。它能够让您区分匿名用户和已登录用户，您甚至可以区分不同角色的用户。LoginView 是模板驱动的，因此它允许您定义不同的模板来显示给不同的用户。下表描述了两个主要模板和特殊的 `Role` 元素。

| 模板 | 描述 |
| :--- | :--- |
| AnonymousTemplate | 此模板中的内容仅对未身份验证的用户显示。 |
| LoggedInTemplate | 此模板中的内容仅对已登录用户显示。此模板与 AnonymousTemplate 互斥。两个模板在任何时候只能有一个可见的。 |

# 介绍登录控件

# RoleGroups

此控件可以包含一个或多个 `RoleGroup` 元素，这些元素又包含一个 `ContentTemplate` 元素，用于定义指定角色的内容。允许查看内容的角色或角色在 `Roles` 属性中定义，该属性接受用逗号分隔的角色列表。`RoleGroups` 元素与 `LoggedInTemplate` 互斥。这意味着如果用户是 `RoleGroup` 某个角色的成员，则 `LoggedInTemplate` 中的控件将不可见。此外，仅显示与用户角色匹配的第一个 `RoleGroup` 的内容。

LoginView 本身输出的标记并不比您在控件子元素中定义的内容要多，您可以轻松地将其嵌入一对 HTML 标签（如 `<h1>` 和 `<li>`）之间，以创建自定义的标题或列表项。

以下代码段显示了一个为三类用户定义内容的 LoginView：网站匿名访问者、已登录用户以及已登录且是 Managers 成员的用户：

```asp
<asp:LoginView Id="LoginView" runat="server">
  <AnonymousTemplate>
    Hi visitor. Would you be interested in signing up for an account?
  </AnonymousTemplate>
  <LoggedInTemplate>
    Hi visitor and welcome back to LoginWrox.com.
  </LoggedInTemplate>
  <RoleGroups Roles="Managers">
    <ContentTemplate>
      Hi manager. You can proceed to the Management section.
    </ContentTemplate>
  </RoleGroups>
</asp:LoginView>
```

您在本章稍后的部分可以了解到如何配置角色。

# LoginStatus

正如练习所示，LoginStatus 控件提供了有关用户当前状态的信息。当用户未身份验证时，它提供登录链接，当设置 `LoginText` 和 `LogoutText` 属性显示文本时，它提供注销链接。或者，您可以使用 `LoginImageUrl` 和 `LogoutImageUrl` 属性显示图像而不是文本。如果您同时设置了图像和文本，则显示文本并作为备用文本。最后，您可以设置 `LogoutAction` 来决定当前页面是刷新用户用户，还是在登录后将用户带到另一个页面。该目标页面通过设置 `LogoutPageUrl` 指定。

除了这些属性外，该控件还能触发两个事件：`LoggingOut` 和 `LoggedOut`，它们分别在用户注销之前和之后触发。

# LoginName

LoginName 是一个极其简单的控件。它所做的只是显示已登录用户的名称。要将用户名嵌入某些文本中（例如“You are logged in as Imar”），可以使用它。

（注：由于提供的原文似乎在此处结束，翻译根据提供的文本完成）
