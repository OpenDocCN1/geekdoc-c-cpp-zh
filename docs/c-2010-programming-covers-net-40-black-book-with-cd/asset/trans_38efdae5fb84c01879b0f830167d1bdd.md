

## 表 16.15：CreateUserWizard 类的显著属性

| 属性 | 描述 |
|---|---|
| ErrorMessageStyle | 检索样式属性集合以定义错误消息的外观。 |
| HelpPageIconUrl | 检索或指定要显示在帮助页面链接旁边的图像的 URL。 |
| HelpPageText | 检索或指定帮助页面链接的文本。 |
| HelpPageUrl | 检索或指定帮助页面的 URL。 |
| HyperLinkStyle | 检索或指定定义超链接外观的属性集合。 |
| InstructionText | 检索或指定创建新用户帐户的帮助文本。 |
| InstructionTextStyle | 检索属性集合以定义说明文本的外观。 |
| InvalidAnswerErrorMessage | 检索或指定在密码检索答案无效时显示的消息。 |
| InvalidEmailErrorMessage | 检索或指定在输入的电子邮件地址无效时显示的消息。 |
| InvalidPasswordErrorMessage | 检索或指定在输入的密码无效时显示的消息。 |
| InvalidQuestionErrorMessage | 检索或指定在密码检索问题无效时显示的消息。 |
| LabelStyle | 检索属性集合以定义标签的外观。 |
| LoginCreatedUser | 检索或指定一个值，指示在创建用户帐户后新用户是否可以登录。 |
| MailDefinition | 检索属性集合以定义发送给新用户的电子邮件消息的特征。 |
| MembershipProvider | 检索或指定用于创建用户帐户的 Membership 服务提供程序。 |
| Password | 检索用户输入的密码。 |
| PasswordHintStyle | 检索属性集合以定义描述密码要求的文本的外观。 |
| PasswordHintText | 检索或指定描述密码要求的文本。 |
| PasswordLabelText | 检索或指定密码文本框的标签文本。 |
| PasswordRegularExpression | 检索或指定用于验证提供的密码的正则表达式。 |
| PasswordRegularExpressionErrorMessage | 检索或指定在输入的密码不符合特定模式时显示的错误消息。 |
| PasswordRequiredErrorMessage | 检索或指定在用户未输入密码时显示的错误消息文本。 |
| Question | 检索或指定用户输入的密码恢复确认问题。 |
| QuestionLabelText | 检索或指定问题文本框的标签文本。 |
| QuestionRequiredErrorMessage | 检索或指定在用户未输入密码确认问题时显示的错误消息。 |
| RequireEmail | 检索或指定一个值，指示网站用户是否需要电子邮件地址。 |
| SkipLinkText | 检索或指定一个值，用于提供替代文本以通知屏幕阅读器跳过侧边栏区域的内容。这是重写后的属性 |
| TextBoxStyle | 检索样式属性的引用以定义 TextBox 控件的外观。 |
| TitleTextStyle | 检索样式属性的引用以定义标题的外观。 |
| UnknownErrorMessage | 检索或指定在 Membership 提供程序返回的错误未定义时显示的错误消息。 |
| UserName | 检索或指定用户输入的用户名。 |
| UserNameLabelText | 检索或指定 User Name 文本框的标签文本。 |
| UserNameRequiredErrorMessage | 检索或指定在 User Name 文本框为空时显示的错误消息。 |
| ValidatorTextStyle | 检索对样式对象的引用，允许您设置验证错误消息的外观。 |
| WizardSteps | 检索对包含为控件定义的全部 WizardStepBase 对象的集合的引用。这是重写后的属性。 |

表 16.16 列出了 CreateUserWizard 类的显著事件：

## 表 16.16：CreateUserWizard 类的显著事件

| 事件 | 描述 |
|---|---|
| ContinueButtonClick | 在用户单击 Continue 按钮时引发。Continue 按钮显示为用户帐户创建过程的最后一步。 |
| CreatedUser | 在 Membership 服务提供程序创建新的网站用户帐户后引发。 |
| CreateUserError | 在 Membership 服务提供程序在创建用户帐户时抛出错误时引发。 |
| CreatingUser | 在调用 Membership 服务提供程序创建用户帐户之前引发。 |
| SendingMail | 在成功创建用户后发送确认电子邮件之前引发。 |
| SendMailError | 在向新用户发送电子邮件时发生 SMTP 错误时引发。 |

CreateUserWizard 控件具有默认的步骤集合来收集用户信息。您还可以向向导添加额外的步骤以收集额外的用户信息。以下是用于创建 CreateUserWizard 控件步骤的一些重要组件：

- CreateUserWizardStep – 包含创建新用户的用户界面和逻辑。这是预定义的步骤。
- CompleteWizardStep – 在用户帐户成功创建时显示信息。这是预定义的步骤。
- WizardSteps 集合 – 指在创建用户过程中显示的所有用户定义步骤的集合。一次只显示一个步骤。
- 导航按钮 – 允许用户在 CreateUserWizard 控件中前往下一 步和上一步。
- SideBar – 列出所有 WizardSteps 步骤；从而使用户能够随机访问任何 WizardSteps 步骤。这是可选组件。
- Header – 为用户提供有关每个步骤的信息。它位于向导顶部。这也是可选组件。

您可以简单地从工具箱中拖放此控件将其添加到 Web 页面。

图 16.8 显示了设计时期的 CreateUserWizard 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_800_0.png)

图 16.8：显示 CreateUserWizard 控件

现在您已经了解了各个登录控件，让我们继续学习 Web Parts 控件。

## 介绍 Web Parts 控件

Web Parts 控件是指一组控件，允许用户在运行时动态个性化其网站。有了这些控件的帮助，用户可以通过更改 Web 页面的内容、行为和外观来根据自己的喜好个性化 Web 页面。由一个用户所做的更改可以应用于特定用户或网站的所有用户。可以通过 Web Parts 控件执行以下活动：

- 内容个性化 – 在 Web Parts 控件的帮助下，您可以个性化 Web 页面的内容，例如添加更多内容、删除现有内容或隐藏内容。
- 页面布局个性化 – 更改 Web Parts 控件的外观、行为或属性并将其拖到 Web 页面上的不同区域或区域。
- 连接创建 – 通过 Web Parts 控件在两个 Web Parts 控件之间维护连接。
- 控件的导出和导入 – 将 Web Parts 控件及其外观设置和数据导入或导出到其他 Web 页面，以减少用户端的重新配置。
- 站点级设置个性化 – 设置站点级设置并根据其角色向选定用户授予访问权限。此操作只能由经过身份验证的用户执行。

在此，您将了解具有 Web Parts 控件的 Web 页面的显示模式。您还将了解各个 Web Parts 控件 – WebPartManager、ProxyWebPartManager、WebPartZone、CatalogZone 和 EditorZone 控件。让我们从 Web Parts 页面的显示模式开始。

## WebPartManager 控件

WebPartManager 控件充当管理 Web 页面上所有其他 Web Parts 控件、功能和事件的中心点。此控件协调 Web Parts 控件之间的交互以及 Web 页面上发生的事件。WebPartManager 控件管理 Web 页面上 Web Parts 控件的个性化状态。个性化允许存储用户信息和所有运行时自定义

