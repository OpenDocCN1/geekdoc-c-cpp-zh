

**表5.11：LoginStatus 类的公共事件**

| 事件 | 描述 |
|---|---|
| `LoggedOut` | 当用户注销过程完成时，由 LoginStatus 类调用 |
| `Load` | 当 LoginStatus 控件在 Page 对象中加载时调用 |

现在，您将通过执行以下步骤来学习如何在网站中使用 `LoginStatus` 控件：

- 1. 单击 **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**。
- 2. 从菜单栏选择 **文件→新建→网站**。出现 **新建网站** 对话框。
- 3. 从 **已安装的模板** 窗格中选择 **Visual C#**，然后在中间窗格中选择 **ASP.NET 空网站** 模板。将网站名称设置为 **LoginStatusControl**。
- 4. 单击 **确定** 按钮。创建 **LoginStatusControl** 应用程序。
- 5. 打开 **解决方案资源管理器** 窗口，并 *右键单击* 应用程序名称。在本例中，我们右键单击的是 **LoginStatusControl** 应用程序。
- 6. 向 **LoginStatusControl** 应用程序添加一个 Web 窗体（**Default.aspx**）。同样，向 **LoginStatusControl** 应用程序添加另一个 Web 窗体（**Default2.aspx**）。
- 7. 将 **Login** 控件 *拖放* 到窗体上，并创建用户帐户。另外，将 Login 控件的 **DestinationPageUrl** 属性设置为 **Default2.aspx**。
- 8. *拖放* 一个 **Label** 控件，并将其 **Text** 属性设置为 **WELCOME!**。另外，从工具箱中添加 **LoginName** 控件（图 ASP-5.29）。
- 9. 从工具箱中将 **LoginView** 控件 *拖放* 到 **Default2.aspx** Web 窗体上，然后单击智能标记以打开 **LoginStatus 任务** 菜单（图 ASP-5.29）。
- 10. 从 **视图** 下拉列表中选择 **已登录** 选项，如图 ASP-5.29 所示。
- 11. *右键单击* **LoginStatus** 控件，并从上下文菜单中选择 **属性** 选项，以打开属性窗口。
- 12. 将 **LogoutAction** 属性设置为 **Redirect**，如图 ASP-5.30 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_569_0.png)

- 13. 单击省略号 **[...]** 按钮，以在属性窗口中设置 **LogoutPageUrl** 属性。出现 **选择 URL** 对话框（图 ASP-5.31）。

**表5.12：PasswordRecovery 类的公共属性**

| 属性 | 描述 |
|---|---|
| `AnswerRequiredErrorMessage` | 使用此属性，可以在用户将答案字段留空时，为 PasswordRecovery 控件指定自定义错误消息 |
| `QuestionFailureText` | 使用此属性，可以在用户提供错误答案时，为 PasswordRecovery 控件指定自定义消息 |
| `SuccessText` | 使用此属性，可以在密码恢复任务成功完成时，为 PasswordRecovery 控件指定自定义消息 |

**表5.13：PasswordRecovery 类的公共事件**

| 事件 | 描述 |
|---|---|
| `AnswerLookupError` | 当发现用户对问题的回答不正确时调用 |
| `SendingMail` | 当用户答案被确认正确后，服务器发送包含密码的电子邮件时调用 |
| `VerifyingAnswer` | 当用户提交对密码恢复确认问题的答案时调用 |

现在，您将通过执行以下步骤来学习如何在网站中使用 **PasswordRecovery** 控件：

- 1. *单击* **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**。
- 2. 从菜单栏 *选择* **文件→新建→网站**。出现新建网站对话框。
- 3. 从 **已安装的模板** 窗格中 *选择* **Visual C#**，然后在中间窗格中选择 **ASP.NET 空网站** 模板。
- 4. 将网站名称 *设置* 为 **PasswordRecoveryControl**。
- 5. *单击* **确定** 按钮。创建 **PasswordRecoveryControl** 应用程序。
- 6. *打开* 解决方案资源管理器窗口，并右键单击应用程序名称。在本例中，我们右键单击的是 **PasswordRecoveryControl** 应用程序。
- 7. 向 **PasswordRecoveryControl** 应用程序 *添加* 一个 Web 窗体（**Default.aspx**）。同样，向 **PasswordRecoveryControl** 应用程序添加另一个 Web 窗体（**Default2.aspx**）。
- 8. 将 Login 控件 *拖放* 到窗体（**Default.aspx**）上，并像之前一样创建用户帐户。另外，将其 **DestinationPageUrl** 属性设置为 **Default2.aspx**。
- 9. 从工具箱中将 PasswordRecovery 控件 *拖放* 到 **Default2.aspx** 页面上。
- 10. *打开* 系统中的 IIS 管理器（图 ASP-5.34）。
- 11. 从 ASP.NET 部分 *双击* **简单邮件传输协议 (SMTP)** 电子邮件选项，如图 ASP-5.34 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_572_0.png)

图 ASP-5.34

出现 SMTP 电子邮件页面（图 ASP-5.35）。

- 12. *选择* **将电子邮件存储在拾取目录中** 选项，并 *浏览* 一个拾取目录，密码详细信息将发送到该目录，如图 ASP-5.35 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_572_1.png)

图 ASP-5.35

- 13. *关闭* Internet 信息服务 (IIS) 管理器。
- 14. *单击* Web 应用程序中 Login 控件的智能标记。出现 Login 任务菜单。
- 15. 从 Login 任务菜单中 *选择* **管理网站** 选项。出现 ASP.NET 网站管理工具主页（图 ASP-5.36）。
- 16. *选择* **应用程序选项卡**（图 ASP-5.36）。
- 17. 从 SMTP 设置窗格中 *选择* **配置 SMTP 电子邮件设置** 选项，如图 ASP-5.36 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_573_0.png)

图 ASP-5.36

配置 SMTP 设置页面出现在应用程序选项卡中（图 ASP-5.37）。

- 18. 将 **服务器名称** 输入为 *smtpout.secureserver.net*（图 ASP-5.37）。
- 19. 将 **服务器端口** 输入为 25（图 ASP-5.37）。
- 20. 在 **发件人** 文本框中输入电子邮件 ID（图 ASP-5.37）。
- 21. 选择 **基本** 选项（图 ASP-5.37）。
- 22. 在 **发件人的用户名** 文本框中输入您的电子邮件 ID（图 ASP-5.37）。
- 23. 将 **发件人的密码** 输入为您的密码（图 ASP-5.37）。
- 24. 单击 **保存** 按钮，如图 ASP-5.37 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_573_1.png)

图 ASP-5.37

配置 SMTP 设置窗格中出现“SMTP 设置已保存”消息（图 ASP-5.37）。

- 25. 单击 **确定** 按钮，如图 ASP-5.38 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_574_0.png)

图 ASP-5.38

ASP.NET 网站管理工具窗口再次出现。

- 26. 关闭 ASP.NET 网站管理工具。
- 27. 将 Default.aspx 页面设置为起始页（图 ASP-5.39）。
- 28. 按 F5 键在浏览器中执行应用程序（图 ASP-5.39）。
- 29. 单击“忘记密码?”链接（图 ASP-5.39）。出现 Default2.aspx 页面，显示 PasswordRecovery 控件（图 ASP-5.40）。
- 30. 在“用户名”文本框中输入用户名（图 ASP-5.40）。
- 31. 单击“提交”按钮，如图 ASP-5.40 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_574_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_574_2.png)

图 ASP-5.39

图 ASP-5.40

出现问题页面（图 ASP-5.41）。

- 32. 在“答案”文本框中输入答案（图 ASP-5.41）。
- 33. 单击“提交”按钮，如图 ASP-5.41 所示。出现成功窗口，显示消息“您的密码已发送给您”，如图 ASP-5.42 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_575_0.png)

图 ASP-5.41

![](img/9862a98a1a2d3bb14334137965a1ec60_575_1.png)

图 ASP-5.42

现在，在了解了 PasswordRecovery 控件之后，让我们学习如何使用 web.config 文件为密码恢复配置虚拟 SMTP 电子邮件服务器。

## 为密码恢复配置 web.config 文件

在使用 PasswordRecovery 控件时，您需要在应用程序的 **web.config** 文件中指定邮件服务器设置，以便在您的电子邮件 ID 上接收密码。配置文件包含 `<system.net>` XML 标签元素。此元素在其子元素 `<mailSettings>` 标签中定义了电子邮件配置。由于 SMTP 是 ASP.NET Web 应用程序用来传输电子邮件的网络标准，因此用户的电子邮件会在 `<smtp...>` `</smtp>` XML 元素标签中被识别。

**web.config** 文件中 `<system.net>` XML 标签的代码片段如下：

```xml
<system.net>
    <mailSettings>
        <smtp from="puneet.saxena@kogentindia.com">
            <network host="smtpout.secureserver.net" password="puneet"
userName="puneet.saxena@kogentindia.com" />
        </smtp>
    </mailSettings>
</system.net>
```

在前面的代码片段中，`<smtp>` 元素有一个属性 **from**，它指定发送包含所检索密码的电子邮件的电子邮件 ID。`<smtp>` 元素还包含一个称为 `<network>` 的子元素。`<network>` 子元素具有以下属性：

- **host：** 包含主机服务器的值
- **password：** 包含发送电子邮件的电子邮件帐户的密码
- **userName：** 包含发送电子邮件的用户的电子邮件 ID

## 总结

本章讨论 ASP.NET 4.0 中可用的各种登录控件，例如 Login、LoginView、PasswordRecovery、LoginStatus、LoginName 和 ChangePassword。您还学习了如何实现这些控件，以及如何通过使用 **ASP.NET 网站管理工具** 在 ASP.NET 中创建用户帐户。本章还讨论了所有这些控件值得注意的属性和方法。

在下一章中，您将学习 ADO.NET 及其体系结构。除此之外，您还将学习各种数据源和数据绑定控件，例如 SqlDataSource、AccessDataSource、GridView、DataList 和 DetailsView。

