

# 表 16.13：ChangePassword 类的显著属性

| Property | Description |
|---|---|
| PasswordRequiredErrorMessage | 检索或指定在用户将 Current Password 文本框留空时显示的错误消息。 |
| SuccessPageUrl | 检索或指定在成功更改密码后向用户显示的页面的 URL。 |
| SuccessTemplate | 检索或指定用于显示 ChangePassword 控件的 Success 和 Change Password 视图的 ITemplate 对象。 |
| SuccessTemplateContainer | 检索 ChangePassword 控件用于创建 SuccessTemplate 模板实例的容器。这提供了对子控件的编程访问。 |
| SuccessText | 检索或指定在 SuccessTitleText 和 Continue 按钮之间在 Success 视图上显示的文本。 |
| SuccessTextStyle | 检索样式属性以定义 Success 视图上文本的外观。 |
| SuccessTitleText | 检索或指定 Success 视图的标题。 |
| TextBoxStyle | 检索样式属性的引用以定义 ChangePassword 控件上 TextBox 控件的外观。 |
| TitleTextStyle | 检索样式属性的引用以定义 ChangePassword 控件上标题的外观。 |
| UserName | 检索或指定要更改密码的用户名。 |
| UserNameLabelText | 检索或指定 User Name 文本框的标签。 |
| UserNameRequiredErrorMessage | 检索或指定在用户将 User Name 文本框留空时显示的错误消息。 |
| ValidatorTextStyle | 检索样式属性的引用以定义与 ChangePassword 控件使用的任何输入验证关联的错误消息的外观。 |

表 16.14 列出了 ChangePassword 类的显著事件：

# 表 16.14：ChangePassword 类的显著事件

| Event | Description |
|---|---|
| CancelButtonClick | 在用户单击 Cancel 按钮以停止更改密码过程时引发 |
| ChangedPassword | 在用户帐户的密码更改时引发 |
| ChangePasswordError | 在更改用户帐户的密码时发生错误时引发 |
| ChangingPassword | 在更改用户帐户的密码之前引发 |
| ContinueButtonClick | 在用户单击 Continue 按钮时引发 |
| SendingMail | 在向用户发送密码已更改的电子邮件确认之前引发 |
| SendMailError | 在向用户发送电子邮件消息时发生 SMTP 错误时引发 |

您可以简单地从 Toolbox 将 ChangePassword 控件拖放以将其添加到 Web 页面。图 16.7 显示了设计时状态下的 ChangePassword 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_796_0.png)

# 图 16.7：显示 ChangePassword 控件

# CreateUserWizard 控件

CreateUserWizard 控件使用 Membership 服务在 Membership 数据存储中创建新用户。此控件是已存在的 Wizard 控件的扩展版本。CreateUserWizard 控件由 CreateUserWizard 类提供，并且可以通过使用模板和样式属性进行自定义。

以下代码片段显示了 CreateUserWizard 类的类层次结构：

```
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.CompositeControl
                System.Web.UI.WebControls.Wizard
                    System.Web.UI.WebControls.CreateUserWizard
```

CreateUserWizard 类包含各种方法、属性和事件。

表 16.15 列出了 CreateUserWizard 类的显著属性：

| Property | Description |
|---|---|
| **ActiveStepIndex** | 检索或指定当前显示给用户的步骤。这是重写后的属性。 |
| **Answer** | 检索或指定最终用户对密码恢复确认问题的回答。 |
| **AnswerLabelText** | 检索或指定密码确认答案文本框的标签文本。 |
| **AnswerRequiredErrorMessage** | 检索或指定在用户未回答密码确认问题时显示的错误消息。 |
| **AutoGeneratePassword** | 检索或指定是否自动为新用户帐户生成密码的值。 |
| **CompleteStep** | 定义创建用户的过程的最后一步。 |
| **CompleteSuccessText** | 检索或指定在网站用户帐户成功创建时显示的文本。 |

# 表 16.15：CreateUserWizard 类的显著属性

| Property | Description |
|---|---|
| CompleteSuccessTextStyle | 检索属性集合以定义在网站用户帐户成功创建时显示的文本的外观。 |
| ConfirmPassword | 检索用户输入的第二个密码。 |
| ConfirmPasswordCompareErrorMessage | 检索或指定在密码文本框中的密码与确认密码不匹配时要显示的错误消息。 |
| ConfirmPasswordLabelText | 检索或指定第二个密码文本框的标签文本。 |
| ConfirmPasswordRequiredErrorMessage | 检索或指定在用户将确认密码文本框留空时显示的错误消息。 |
| ContinueButtonImageUrl | 检索或指定用于显示继续按钮的图像的 URL。继续按钮显示为创建用户帐户过程的最后一步。 |
| ContinueButtonStyle | 检索属性集合以定义继续按钮的外观。 |
| ContinueButtonText | 检索或指定在 Continue 按钮上显示的文本标题。 |
| ContinueButtonType | 检索或指定作为 Continue 按钮呈现的按钮类型。 |
| ContinueDestinationPageUrl | 检索或指定用户在成功页面上单击 Continue 按钮后将看到的页面的 URL。 |
| CreateUserButtonImageUrl | 检索或指定为 Create User 按钮显示的图像的 URL。 |
| CreateUserButtonStyle | 检索属性集合以定义 Create User 按钮的外观。 |
| CreateUserButtonText | 检索或指定在 Create User 按钮上显示的文本标题。 |
| CreateUserButtonType | 检索或指定作为 Create User 按钮呈现的按钮类型。 |
| CreateUserStep | 检索显示创建用户帐户步骤的模板。 |
| DisableCreatedUser | 检索或指定是否允许新用户登录网站的值。 |
| DisplaySideBar | 检索或指定是否显示控件的侧边栏区域的值。这是重写后的属性。 |
| DuplicateEmailErrorMessage | 检索或指定在用户输入的电子邮件地址已在 Membership 服务提供程序中使用的情况下显示的错误消息。 |
| DuplicateUserNameErrorMessage | 检索或指定在用户输入的用户名已在 Membership 服务提供程序中使用的情况下显示的错误消息。 |
| EditProfileIconUrl | 检索或指定用于在指向用户配置文件编辑页面的链接旁边显示的图像的 URL。 |
| EditProfileText | 检索或指定指向用户配置文件编辑页面的链接的文本标题。 |
| EditProfileUrl | 检索或指定用户配置文件编辑页面的 URL。 |
| Email | 检索或指定用户输入的电子邮件地址。 |
| EmailLabelText | 检索或指定电子邮件文本框的标签文本。 |
| EmailRegularExpression | 检索或指定用于验证电子邮件地址的正则表达式。 |
| EmailRegularExpressionErrorMessage | 检索或指定在输入的电子邮件地址未通过网站对电子邮件地址的标准时显示的错误消息。 |
| EmailRequiredErrorMessage | 检索或指定在电子邮件文本框中未输入电子邮件地址时向用户显示的消息。 |

