

# 604 | ASP.NET 网站安全

在运行时，`{}` 将替换为用户名。

默认情况下，LoginStatus 显示一个允许用户登录和注出的链接。因为 Menu 已经包含了一个指向登录页的链接，所以使用 LoginView 会再次在用户登录时显示退出文本。如果你想添加登录链接，可以扩展 LoginView 的匿名模板，或者移除 LoginView 使 LoginStatus 对所有用户可见。

除了这些允许用户登录并显示相关内容的控件外，`TextBox` 还会包含更多控件，允许用户在网站上注册新账户、更改密码以及找回密码。这些控件将在下文中讨论。

## CreateUserWizard

简要介绍 CreateUserWizard 在练习中的用法。该控件提供的功能比标准行为多得多。

开始时，控件有一长系列 Text 属性，如 `CancelButtonText`、`SuccessText`、`UserNameLabelText` 和 `CreateButtonText`，它们影响控件使用的文本。所有属性都有默认值，但你可以根据需要更改它们。

控件有一系列以 ImageUrl 结尾的属性，例如 `CreateUserButtonImageUrl`。如果你希望为生成图像而不是按钮，你还需要设置 `ButtonType`。为了将创建改为图像，你需要设置 `CreateUserButtonImageUrl` 为有效的图像，并将 `ButtonType` 设置为 Image。

`ButtonType` 的默认值是 Button，默认渲染标准按钮。你也可以将 `ButtonType` 设置为 Link，使其渲染为标准 Link 控件。在本节开头介绍的相关属性。

此外，控件暴露了许多实用属性，你可以更改其行为和外观，如下所示。

| 属性 | 描述 |
| --- | --- |
| ContinueDestinationPageUrl | 定义用户注册后点击继续时跳转的页面。 |
| DisableCreatedUser | Determine账户创建时是否将用户标记为禁用。设置为 True 时，用户在启用之前无法登录网站。稍后将查看如何手动激活和禁用账户。默认值为 False。 |

## 介绍登录控件

| LoginCreatedUser | Determine账户创建后是否自动登录。默认值为 True。 |
| RequireEmail | Determine 是否允许用户提供电子邮件地址。默认值为 True。 |
| MailDefinition | 包含许多子属性，允许你定义在注册后发送给用户的（可选）电子邮件。 |

你可能会发现控件没有任何属性来更改至少六个字符的密码策略。因为多个控件都需要访问这些设置，你需要在底层程序上进行配置。在本章稍后的“配置你的 Web 应用程序”部分，将查看它是如何工作的。

CreateUserWizard 可以向用户发送新账户创建成功的电子邮件。此邮件也可以作为用户名和密码的提醒。在接下来，你将看到如何配置 MailDefinition 元素，让 CreateUserWizard 向用户发送确认账户的电子邮件，并发送用户名和密码。

## 使用 CreateUserWizard 测试发送确认邮件

在本练习中，你需要配置 .system.net 文件，指定有效的邮件服务器名称或本地提取文件夹。如果你没有这些设置且不知道如何配置，请参阅第 9 章。

1. 在 App_Data 文件夹中新建一个文本文件，并命名为 SignUpConfirmation.txt。
2. 在文件中添加以下文本并保存：

你好 <% UserName %>

感谢你在 www.PlanetWrox.com 注册新账户。

请使用以下详情登录网站：

用户名：<% UserName %>
密码：<% Password %>

我们期待你的贡献。

Planet Wrox 团队
3. 打开 SignUp.aspx，切换到设计视图。在 CreateUserWizard 控件的属性网格中，找到 MailDefinition 属性并展开它。点击 BodyFileName 属性，点击省略号浏览并选择在 App_Data 文件夹中创建的 SignUpConfirmation.txt。
4. 将 Subject 属性设置为 "Your New Account at PlanetWrox.com"。设置后，属性网格将如图 16-11 所示。
5. 保存所有更改并在浏览器中刷新 SignUp.aspx。输入你的账户详情并点击“Create User”进行注册。如果收到关于 From 地址的错误，请确保在 Web.config 文件的 from 属性中输入有效的电子邮件地址：

```xml
<smtp deliveryMethod="SpecifiedPickupDirectory" from="planetwrox@example.com">
```

参阅第 9 章查看如何添加此属性。确保你输入的是有效的电子邮件地址，否则邮件服务器可能会拒绝它。
6. 一段时间后，你应该会收到一封包含第 2 步中输入的文本的电子邮件。图 16-12 显示了带有内置功能的邮件。

## 工作原理

在指定 MailDefinition 之前，CreateUserWizard 不发送消息。你使用 BodyFileName 指向你想作为正文的文件。在正文中，你可以使用占位符 <% UserName %> 和 <% Password %>它们会被自动替换为用户名和密码。

## PasswordRecovery

PasswordRecovery 控件允许用户检索现有密码或获取新密码。PasswordRecovery 控件的大部分属性现在应该已经熟悉。它有一系列 Text 属性，如 `GeneralFailureText` 和 `SuccessText`，允许你设置文本。它还有许多以 ButtonType 结尾的属性，如 `ButtonText` 和 `ButtonImageUrl`，允许你更改按钮的外观。当密码恢复成功时，将 SuccessPageUrl 设置另一个页面。

与 CreateUserWizard 类似，PasswordRecovery 控件也有一个 MailDefinition 元素可以指向一个文件。如果你漏掉了 MailDefinition，控件将使用默认正文。

## ChangePassword

ChangePassword 控件允许现有和已登录的用户更改密码。它拥有许多属性来更改文本、错误消息和按钮，类似于 CreateUserWizard 和 PasswordRecovery 控件。它还包含 MailDefinition 元素，允许你向用户的电子邮件地址发送新密码的确认。

## 测试实现密码功能

在本测试中，你在网站上添加 PasswordRecovery 和 ChangePassword 控件以允许用户更改和恢复密码。由于更改密码对已登录的用户才有意义，你将 ChangePassword 控件添加到单独的页面中。在下一章中，你将保护此页面，使只有经过验证的用户才能访问。

1. 在标记视图下打开 Login.aspx，找到 `<AnonymousTemplate>` 内部的结束标签 `</asp:Login>`。在它之后输入两个 `<br />` 元素，为 Login 控件下方留出空间。
2. 从工具箱拖入一个 PasswordRecovery 控件到代码编辑器中，就在你在第 1 步中添加的两个 `<br/>` 元素之后。

