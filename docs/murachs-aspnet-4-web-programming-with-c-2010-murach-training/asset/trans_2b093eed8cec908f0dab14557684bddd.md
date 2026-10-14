

![](img/c024ccf88e28c30c07dd410d4342288f_662_0.png)

## 网站管理工具的 Provider 选项卡

## 放宽默认密码策略的 web.config 文件中的元素

```xml
<membership defaultProvider="AspNetSqlMembershipProviderRelaxed">
    <providers>
        <add name="AspNetSqlMembershipProviderRelaxed"
             type="System.Web.Security.SqlMembershipProvider,
                   System.Web, Version=2.0.0.0, Culture=neutral,
                   PublicKeyToken=b03f5f7f11d50a3a"
             connectionStringName="LocalSqlServer"
             enablePasswordRetrieval="false"
             enablePasswordReset="true"
             requiresQuestionAndAnswer="true"
             applicationName="/"
             requiresUniqueEmail="false"
             passwordFormat="Hashed"
             maxInvalidPasswordAttempts="5"
             passwordAttemptWindow="10"
             passwordStrengthRegularExpression=""
             minRequiredPasswordLength="6"
             minRequiredNonalphanumericCharacters="0"/>
    </providers>
</membership>
```

## 描述

- 默认情况下，使用名为 AspNetSqlProvider 的 *数据提供程序* 将成员资格和角色数据存储在名为 AspNetDb.mdf 的 SQL Server Express 数据库中。但是，您可以使用单独的成员资格和角色提供程序，并且可以编写自己的自定义提供程序。
- 默认成员资格和角色提供程序的定义可以在 machine.config 文件中找到。该文件存储在 .NET Framework 4 安装文件夹下的 Config 文件夹中。
- 要放宽提供程序的密码限制，您可以在应用程序的 web.config 文件中更改密码长度和非字母数字字符的属性。

![](img/c024ccf88e28c30c07dd410d4342288f_662_1.png)

## 如何使用登录控件

一旦您限制了 Web 应用程序中部分或全部页面的访问，您就需要允许具有适当权限的用户登录并访问受限页面。此外，您可能还希望提供其他功能，例如允许用户注销、自行创建账户、恢复忘记的密码或更改密码。您可以使用工具箱中登录组中的控件自动处理这些任务。

## 如何使用 Login 控件

图 19-9 显示了如何创建一个包含 Login 控件的登录页面。当您创建登录页面时，应将其命名为 Login.aspx。因为 ASP.NET 在尝试对用户进行身份验证时会查找此名称的页面。此外，由于此页面用于整个应用程序，您通常希望使用简单的格式，以便它对应用程序的所有部分都同样适用。

一旦您创建了名为 Login.aspx 的页面，您只需向页面添加一个 Login 控件即可获得所有登录功能。为此，将工具箱中登录组中的 Login 控件拖到页面上。

与大多数登录页面一样，Login 控件包含两个文本框，让用户输入用户名和密码。此外，它还包含一个复选框，让用户指示下次访问应用程序时是否希望自动登录。如果用户选中此复选框，应用程序会创建一个包含身份验证票证的持久 cookie。

当用户在 Login 控件中单击“登录”按钮时，控件的代码会尝试对用户进行身份验证。它通过检查用户名和密码是否在成员资格数据存储中来执行此操作。然后，如果用户通过身份验证，代码会检查角色提供程序，以查看用户是否对请求的页面具有适当的授权。如果是，则此代码会继续将浏览器重定向到该页面。

如果您想自动对 Login 控件应用格式设置，可以从控件的智能标记菜单中选择“自动格式”命令。然后，您可以使用生成的“自动格式”对话框选择喜欢的方案。当您这样做时，Visual Studio 将更改控件的许多格式属性。此功能对于 CreateUserWizard、PasswordRecovery 和 ChangePassword 控件同样适用，这些控件在后面的页面中描述。

尽管本图中未显示，登录页面应始终强制页面使用安全连接。然后，如果黑客设法拦截了用户的用户名和密码，您的应用程序也不会受到损害。

## Web 窗体设计器中的 Login 控件

![](img/c024ccf88e28c30c07dd410d4342288f_664_0.png)

## Login 控件的 aspx 代码

```aspx
<asp:Login ID="Login1" runat="server">
</asp:Login>
```

## Login 控件的常用属性

| 属性 | 描述 |
|---|---|
| DisplayRememberMe | 确定是否显示“记住我”复选框。默认情况下，此项设置为 True。 |
| RememberMeText | RememberMe 文本框标签的文本。 |
| RememberMeSet | 确定是否向用户计算机发送持久 cookie，这取决于 RememberMe 复选框是否被选中。 |
| FailureText | 登录尝试失败时显示的文本。 |

## 描述

- 当用户尝试访问需要身份验证的页面时，ASP.NET 会自动将用户重定向到应用程序的登录页面。此页面必须命名为 Login.aspx。
- 要自动对 Login 控件应用格式设置，请从控件的智能标记菜单中选择“自动格式”命令。然后，从显示的对话框中选择一个方案。

## 如何使用 LoginStatus 和 LoginName 控件

图 19-10 显示了如何使用 LoginStatus 和 LoginName 控件。在此图的顶部页面中，您可以看到 LoginName 控件提供了已登录用户的名称。相比之下，LoginStatus 控件在用户尚未登录时提供登录链接，在用户已登录时提供注销链接。请注意，此页面还包含一个超链接，用户可以单击该链接如果显示的用户名不正确。此超链接不是 LoginName 或 LoginStatus 控件的一部分。

要使用这些控件，只需从工具箱的登录组中将它们拖到窗体上。然后，您可以根据需要更改属性。例如，您可以使用 LoginStatus 控件的 LoginText 和 LogoutText 属性来更改链接显示的文本。您还可以使用 LoginName 控件的 FormatString 属性在用户名占位符之前或之后添加文本。

当用户单击 LoginStatus 控件的登录链接时，用户将被重定向到登录页面并需要输入用户名和密码。然后，在用户通过身份验证后，用户将被重定向到原始页面。相反，当用户单击注销链接时，用户将被重定向到登录页面（Login.aspx）。

当用户已通过身份验证时，LoginName 控件将显示用户名。否则，控件不会显示用户名。但是，它将显示 FormatString 属性中指定的任何其他文本。

## 如何使用 CreateUserWizard 控件

如果您的应用程序只有少数几个用户，您可以使用本章前面描述的 Web Site Administration Tool 来创建和管理用户。然后，您可以使用 Login、LoginStatus 和 LoginName 控件允许用户登录和注销。通常，您希望允许用户自行创建用户账户。为此，您可以使用图 19-11 所示的 CreateUserWizard 控件。

默认情况下，CreateUserWizard 控件使用两个步骤创建新用户：创建用户步骤和完成步骤。要显示这些步骤，您可以使用本图中所示的智能标记菜单中的下拉列表。

通常，这些步骤的工作方式与您期望的一样。在这种情况下，您只需将控件的 ContinueDestinationPageUrl 属性设置为指示用户在完成步骤中单击“继续”按钮时被定向到的页面即可。

如果您需要修改任一步骤的行为，可以从控件的智能标记菜单中为该步骤选择“自定义”命令。然后，您可以通过修改该步骤的控件和属性来自定义该步骤。如果您修改完成步骤，请注意，您可以通过设置该按钮的 PostBackUrl 属性而不是设置 CreateUserWizard 控件的 ContinueDestinationPageUrl 属性来指定用户单击“继续”按钮时显示的页面。

当您使用 CreateUserWizard 控件生成的页面时，您应该意识到成员资格提供程序正被用来将数据写入适当的数据源。这与 Web Site Administration Tool 的工作方式相同。

