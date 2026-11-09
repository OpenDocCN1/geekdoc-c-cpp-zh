
![](img/9862a98a1a2d3bb14334137965a1ec60_563_0.png)

图 ASP-5.16

出现“选择访问方法”页面（图 ASP-5.17）。

- 17. 在 **从 Internet** 选项旁选择单选按钮（图 ASP-5.17）。
- 18. 单击 **下一步** 按钮，如图 ASP-5.17 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_563_1.png)

图 ASP-5.17

出现“高级提供程序设置”页面（图 ASP-5.18）。

- 19. 单击 **下一步** 按钮，如图 ASP-5.18 所示。

![](img/9862a98a1a2d3bb14334137965a1ec60_563_2.png)

图 ASP-5.18

出现“定义角色”页面（图 ASP-5.19）。

- 20. 单击 **下一步** 按钮，如图 ASP-5.19 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_564_0.png)

图 ASP-5.19

出现“创建用户”页面（图 ASP-5.20）。

- 21. *输入*创建账户所需的所有详细信息，如图 ASP-5.20 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_564_1.png)

图 ASP-5.20

出现“您的账户已成功创建”消息（图 ASP-5.21）。

- 22. *单击*“下一步”按钮，如图 ASP-5.21 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_564_2.png)

图 ASP-5.21

出现“添加新访问规则”面板（图 ASP-5.22）。

- 23. 在“添加新访问规则”窗格的“规则应用于”面板中*选择* **所有用户** 单选按钮，并在“权限”面板中选择 **允许** 单选按钮（图 ASP-5.22）。
- 24. 在“添加新访问规则”窗格中*单击* **添加此规则** 按钮（图 ASP-5.22）。
- 25. *单击*“下一步”按钮，如图 ASP-5.22 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_565_0.png)

图 ASP-5.22

出现“正在完成安全设置向导”消息（图 ASP-5.23）。

- 26. *单击*“完成”按钮，如图 ASP-5.23 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_565_1.png)

图 ASP-5.23

- 27. 将 Default.aspx 页面*设置*为网站的起始页。
- 28. *按* F5 键执行应用程序（图 ASP-5.24）。
- 29. *输入*您已创建的账户的用户名和密码（图 ASP-5.24）。
- 30. *单击*“登录”按钮，如图 ASP-5.24 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_565_2.png)

图 ASP-5.24

出现 Default2.aspx 页面，显示您的用户名，如图 ASP-5.25 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_566_0.png)

图 ASP-5.25

了解了 LoginName 控件之后，现在我们来学习 LoginView 控件。

### 使用 LoginView 控件

LoginView 控件是一种 Web 服务器控件，用于根据用户当前是否已登录来显示任何网站网页的两种不同视图。LoginView 控件借助以下模板管理网页两种视图的内容：

- **AnonymousTemplate：** 当用户未登录时显示。
- **LoggedInTemplate：** 当用户已登录时显示。

表 5.6 列出了 LoginView 类的公共属性：

**表 5.6：LoginView 类的公共属性**

| 属性 | 描述 |
|---|---|
| `AnonymousTemplate` | 检索或设置向未登录到网站的用户显示的模板 |
| `Controls` | 检索包含 LoginView 控件的子控件的 ControlCollection 对象 |
| `EnableTheming` | 检索或设置一个值，该值指示是否将主题应用于 LoginView 控件 |
| `LoggedInTemplate` | 检索或设置向已登录到网站但不属于 RoleGroups 属性中指定的某个角色组成员的网站用户显示的模板 |
| `RoleGroups` | 检索角色组的集合，这些角色组将内容模板与特定角色关联 |
| `SkinID` | 检索或设置要应用于 LoginView 控件的外观 |

表 5.7 列出了 LoginView 类的公共方法：

**表 5.7：LoginView 类的公共方法**

| 方法 | 描述 |
|---|---|
| `DataBind` | 将数据源绑定到 LoginView 控件及其所有子控件。此方法被重写。 |
| `Focus` | 将输入焦点设置到控件。此方法被重写。 |

表 5.8 列出了 LoginView 类的公共事件：

**表 5.8：LoginView 类的公共事件**

| 事件 | 描述 |
|---|---|
| ViewChanged | 在视图更改后调用 |
| ViewChanging | 在视图更改前调用 |

现在，您将通过执行以下步骤来学习如何在网站中使用 LoginView 控件：

- 1. *单击* **开始→所有程序→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010。**
- 2. 从菜单栏中*选择* **文件→新建→网站**。出现 **新建网站** 对话框。
- 3. 从 **已安装的模板** 窗格中*选择* **Visual C#**，然后在中间窗格中选择 **ASP.NET 空网站** 模板。
- 4. 将网站名称*设置*为 **LoginViewControl**。
- 5. *单击* **确定** 按钮。**LoginViewControl** 应用程序已创建。
- 6. *打开* **解决方案资源管理器** 窗口，并*右击*应用程序名称。在本例中，我们右击的是 **LoginViewControl** 应用程序。
- 7. 向 **LoginViewControl** 应用程序中*添加*一个 Web 窗体（**Default.aspx**）。
- 8. 在窗体上*拖放*一个 **Login** 控件，并像前面那样创建用户账户。
- 9. 向 **LoginViewControl** 应用程序中*添加*另一个 Web 窗体（**Default2.aspx**）。
- 10. 从 **工具箱** 中将 **LoginView** 控件*拖放*到 **Default2.aspx** Web 窗体上。
- 11. *单击*智能标记 (>) 按钮（图 ASP-5.26）。出现 LoginView 任务菜单（图 ASP-5.26）。
- 12. 从 **视图** 选项的下拉列表中*选择* **LoginView** 控件，如图 ASP-5.26 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_567_0.png)

图 ASP-5.26

- 13. 在 **LoginView** 控件中*添加*一个 **Label** 控件，并像前面那样将 **Label** 控件的 **Text** 属性设置为 **欢迎！**。
- 14. 在 **LoginView** 控件中*添加* **LoginName** 控件。
- 15. 将 **Default.aspx** 页面*设置*为网站的起始页。
- 16. *按* **F5** 键执行应用程序。
- 17. *输入*账户的详细信息，例如用户名和密码，并*单击* **登录** 按钮（图 ASP-5.27）。

出现 **Default2.aspx** 页面，显示欢迎消息，如图 ASP-5.28 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_568_0.png)

图 ASP-5.27    图 ASP-5.28

了解了 LoginView 控件之后，现在我们来学习 LoginStatus 控件。

### 使用 LoginStatus 控件

LoginStatus 控件是一种 Web 服务器控件，用于显示用户的当前状态，即用户当前是否已登录到网站。此控件上显示的文本会根据用户的登录状态而变化。LoginStatus 控件具有以下视图：

- **已注销：** 当用户未登录时显示。在此视图中，`LoginStatus` 控件上显示文本“登录”。
- **已登录：** 当用户已登录时显示。在此视图中，`LoginStatus` 控件上显示文本“注销”。

表 5.9 列出了 LoginStatus 类的属性：

**表 5.9：LoginStatus 类的公共属性**

| 属性 | 描述 |
|---|---|
| `LoginImageUrl` | 检索或设置用于登录链接的图像的 URL |
| `LoginText` | 检索或设置用于登录链接的文本 |
| `LogoutAction` | 检索或设置一个值，该值确定当用户使用 LoginStatus 控件从网站注销时所执行的操作 |
| `LogoutImageUrl` | 检索或设置用于注销按钮的图像的 URL |
| `LogoutPageUrl` | 检索或设置注销页面的 URL |
| `LogoutText` | 检索或设置用于注销链接的文本 |

表 5.10 列出了 LoginStatus 类的方法：

**表 5.10：LoginStatus 类的公共方法**

| 方法 | 描述 |
|---|---|
| `ApplyStyleSkin` | 应用在设计器中为该控件设置的视觉属性 |
| `ApplyStyle` | 将指定样式的任何非空白元素复制到 LoginStatus 控件 |

表 5.11 列出了 LoginStatus 类的公共事件：

**表 5.11：LoginStatus 类的公共事件**

| 事件 | 描述 |
|---|---|
| `LoggingOut` | 在用户通过单击注销链接向服务器发送注销请求后调用 |

