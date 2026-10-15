

- 存储会员信息，例如用户名、密码、电子邮件地址以及其他支持数据
- 对网站访客进行身份验证
- 允许用户创建和重置密码
- 为已认证用户创建唯一的识别系统

ASP.NET 4.0 登录控件如下：

- Login
- LoginView
- LoginStatus
- LoginName
- CreateUserWizard
- PasswordRecovery
- ChangePassword

您可以在工具箱的 Login 选项卡下找到这些控件，如图 16.1 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_782_0.png)

**Figure 16.1: The Login Controls Displayed in the Toolbox**

### The Login Control

Login 控件提供了一个用户界面，用于对用户进行身份验证，并根据用户填写的凭据（如用户名和密码）授予他们访问所需服务或资源的权限。由于它可以限制对其他网页的访问，因此 Login 控件通常放置在网站的主页中。

Login 控件由 Login 类提供。以下代码片段显示了 Login 类的类层次结构：

```
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.CompositeControl
                System.Web.UI.WebControls.Login
```

## Chapter 16: Login and Web Parts Controls in ASP.NET 4.0

Login 类包含用于操作 Login 控件的各种方法、属性和事件。这些成员使您能够自定义 Login 控件，例如显示自定义消息并创建用于更改密码或恢复忘记密码的链接。Login 控件包含内置的身份验证逻辑；但是，您可以通过处理 Authenticate 事件来创建自己的逻辑。

表 16.1 列出了 Login 类值得注意的方法：

| Method name | Description |
|---|---|
| `CreateChildControls` | 创建 Login 控件的各个控件并将其事件处理程序与其事件关联 |
| `OnAuthenticate` | 引发 Authenticate 事件以对用户进行身份验证 |
| `OnLoggedIn` | 用户在成功身份验证后登录网站时引发 LoggedIn 事件 |
| `OnLoggingIn` | 用户在身份验证发生前输入登录信息后引发 LoggingIn 事件 |
| `OnLoginError` | 用户登录失败时引发 LoginError 事件 |

Login 类值得注意的属性在表 16.2 中列出：

| Property | Description |
|---|---|
| `BorderPadding` | 检索或指定 Login 控件边框的内边距。 |
| `CheckBoxStyle` | 检索 Style 对象的引用以定义“记住我”复选框的显示设置。 |
| `CreateUserIconUrl` | 检索用于显示新用户注册链接的图像的位置。 |
| `CreateUserText` | 检索或指定指向新用户注册页面的链接的文本。 |
| `CreateUserUrl` | 检索或指定新用户注册页面的 URL。 |
| `DestinationPageUrl` | 检索或指定登录尝试成功时向用户显示的页面的 URL。 |
| `DisplayRememberMe` | 检索或指定指示是否显示“记住我”复选框的值。 |
| `FailureAction` | 检索或指定登录尝试失败时发生的操作。 |
| `FailureText` | 检索或指定登录尝试失败时显示的文本。 |
| `FailureTextStyle` | 检索样式属性的引用以定义失败文本的外观。 |
| `HelpPageIconUrl` | 检索用于显示登录帮助页面链接的图像的位置。 |
| `HelpPageText` | 检索或指定指向登录帮助页面的链接的文本。 |
| `HelpPageUrl` | 检索或指定登录帮助页面的 URL。 |
| `HyperLinkStyle` | 检索属性集合以定义 Login 控件中超链接的外观。 |
| `InstructionText` | 检索或指定用户的登录说明文本。 |
| `InstructionTextStyle` | 检索 TableItemStyle 对象的引用以定义说明文本的样式。 |
| `LayoutTemplate` | 检索或指定用于显示 Login 控件的模板。 |
| `LoginButtonImageUrl` | 检索或指定用作登录按钮的图像的 URL。 |

![](img/e073a4882197be4ab61103cbe0bcb394_785_0.png)

### The LoginView Control

LoginView 控件是一个 Web 服务器控件，用于根据用户是否已作为注册用户或访客登录到网站的某个网页来显示该网页的两种不同视图。LoginView 控件提供了一种更改页面外观或向不同用户组显示不同内容的方法。此控件具有内置功能，可收集当前用户的状态和角色。如果用户已通过身份验证，控件将借助以下视图模板向用户显示适当的信息：

- AnonymousTemplate – 用户未登录时显示
- LoggedInTemplate – 用户已登录时显示
- RoleGroups – 用户已登录且是具有定义角色组模板的特定角色成员时显示

LoginView 控件由 LoginView 类提供。以下代码片段显示了 LoginView 类的类层次结构：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.LoginView
```

LoginView 类包含用于操作 LoginView 控件的各种方法、属性和事件。

表 16.4 列出了 LoginView 类值得注意的方法：

| Method | Description |
|---|---|
| DataBind | 将数据源绑定到 LoginView 控件及其所有子控件 |
| Focus | 指定输入焦点到 LoginView 控件 |
| OnViewChanged | LoginView 控件更改其视图后引发 ViewChanged 事件 |
| OnViewChanging | LoginView 控件更改其视图前引发 ViewChanging 事件 |

### The LoginName Control

LoginName 控件负责显示所有已认证用户的名称。它使用 Page.User.Identity.Name 命名空间返回用户名的值。如果没有用户登录，则此控件不会在页面上显示。LoginName 控件由 LoginName 类提供。

以下代码片段显示了 LoginName 类的类层次结构：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.LoginName
```

LoginName 类不包含任何不是从其他类（如 Control 类）继承的方法、属性或事件。它包含的唯一非继承属性是 FormatString，用于在 LoginName 控件中显示格式项字符串。您可以简单地从工具箱中拖放此控件将其添加到网页中。

图 16.4 显示了设计时期的 LoginName 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_787_0.png)

Figure 16.4: Displaying the LoginName Control

### The LoginStatus Control

LoginStatus 控件指定特定用户是否已登录到网站。此控件上显示的文本会根据用户的登录状态而变化。当用户未登录时，此控件会以超链接形式显示 Login 文本，便于用户导航到登录页面。为此，LoginStatus 控件使用 web.config 文件的身份验证部分并检索登录页面的 URL。当用户已登录到网站时，LoginStatus 控件会以超链接形式显示 Logout 文本，并在用户单击注销链接后立即删除身份验证信息。

LoginStatus 控件提供以下两个视图：

- Logged Out — 用户未登录时显示。此视图提供指向登录页面的链接。
- Logged In — 用户已登录时显示。此视图提供注销网站的链接。

LoginStatus 控件由 LoginStatus 类提供。以下代码片段显示了 LoginStatus 类的类层次结构：

```
System.Object
  System.Web.UI.Control
    System.Web.UI.WebControls.WebControl
      System.Web.UI.WebControls.CompositeControl
        System.Web.UI.WebControls.LoginStatus
```
