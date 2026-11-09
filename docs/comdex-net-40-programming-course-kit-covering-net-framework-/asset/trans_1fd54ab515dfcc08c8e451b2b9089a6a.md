
## 使用 RequiredFieldValidator 控件

**RequiredFieldValidator** 控件确保用户已在其关联的输入控件（例如 **TextBox** 控件）中输入所需数据。例如，如果您在输入控件中输入购买 T 恤的数据，则有必要输入您要购买的 T 恤尺码。如果未输入尺码，验证控件会显示错误消息。**RequiredFieldValidator** 控件位于 **System.Web.UI.WebControls** 命名空间中。

RequiredFieldValidator 类的值得注意的属性列于表 4.3：

**表 4.3：RequiredFieldValidator 类的值得注意的属性**

| 属性 | 描述 |
|---|---|
| `InitialValue` | 处理关联输入控件的初始值 |

执行以下步骤以学习使用 **RequiredFieldValidator** 控件：

- 1. *打开 Microsoft Visual Studio 2010*，如图 ASP-4.1 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_536_0.png)

图 ASP-4.1

- 2. *选择* **文件→新建→网站** 以创建新网站，如图 ASP-4.2 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_537_0.png)

图 ASP-4.2

这将打开 **新建网站** 对话框（图 ASP-4.3）。

- 3. 在 **已安装的模板** 窗格中选择 **Visual C#**，如图 ASP-4.3 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_537_1.png)

图 ASP-4.3

- 4. 从 **中间** 窗格中选择 **ASP.NET 网站** 模板（图 ASP-4.3）。
- 5. 将其命名为 **RequiredFieldExample**，如图 ASP-4.3 所示（也可在 CD 上获取）。
- 6. 单击 **确定** 按钮，如图 ASP-4.3 所示。

这将在 **源** 视图中打开 **Default.aspx** 网页，如图 ASP-4.4 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_538_0.png)

- 7. *选择* **设计** 选项卡以查看网页的设计（图 ASP-4.4）。
- 8. *拖放* 两个 **标签** 控件、两个 **文本框** 控件和一个 **按钮** 控件，从 **工具箱** 的 **标准** 选项卡到 Default.aspx 页面上。
- 9. *右键单击* 每个控件，从上下文菜单中选择 **属性** 选项以打开 **属性** 窗口，并设置其属性，如表 4.4 所列：

**表 4.4：为控件设置的属性**

| 控件名称 | 属性名称 | 值 |
|---|---|---|
| Label1 | Text | 用户名： |
| Label2 | Text | 密码： |
| Button1 | Text | 提交 |
| TextBox1 | Text | [空白] |
| TextBox1 | Text | [空白] |

- 10. *选择* **工具箱** 下的 **验证** 选项卡。*拖放* 两个 **RequiredFieldValidator** 控件，从 **验证** 选项卡到 **Default.aspx** 页面上（图 ASP-4.5）。
- 11. *重新定位* **Default.aspx** 网页上的所有控件，如图 ASP-4.6 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_538_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_538_2.png)

- 12. 右键单击每个 **RequiredFieldValidator** 控件。从上下文菜单中选择 **属性** 选项以打开 **属性** 窗口，并设置其属性，如表 4.5 所列：

**表 4.5：RequiredFieldValidator 控件的属性**

| 控件 ID | 属性名称 | 值 |
|---|---|---|
| RequiredFieldValidator1 | ControlToValidate | TextBox1 |
| RequiredFieldValidator1 | ErrorMessage | 用户名不能为空 |
| RequiredFieldValidator2 | ControlToValidate | TextBox2 |
| RequiredFieldValidator2 | ErrorMessage | 密码不能为空 |

- 13. 按 F5 键运行应用程序，并在“用户名”和“密码”旁边的两个文本框中未输入任何文本的情况下单击“提交”按钮。错误消息会出现在两个文本框旁边，如图 ASP-4.7 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_539_0.png)

图 ASP-4.7

现在，让我们讨论 **RangeValidator** 控件。

## 使用 RangeValidator 控件

**RangeValidator** 控件检查输入控件的值是否位于指定范围内。此控件位于 **System.Web.UI.WebControls** 命名空间中。还需要为输入控件中输入的数据定义数据类型。因此，为输入控件中的值设置数据类型的 **Type** 属性。以下数据类型用于这些值：

- **字符串：** 指字符串数据类型
- **整数：** 指整数数据类型
- **双精度：** 指双精度数据类型
- **日期：** 指日期数据类型
- **货币：** 指货币数据类型

**RangeValidator** 类的值得注意的属性列于表 4.6：

**表 4.6：RangeValidator 类的值得注意的属性**

| 属性 | 描述 |
|---|---|
| MaximumValue | 获取或设置验证范围的最大值 |
| MinimumValue | 获取或设置验证范围的最小值 |

![](img/9862a98a1a2d3bb14334137965a1ec60_539_1.png)

> 如果设置了其中一个属性，则必须同时设置另一个属性。

执行以下步骤以创建使用 **RangeValidator** 控件的 Web 应用程序：

- 1. *打开* **Microsoft Visual Studio 2010**。
- 2. *选择* **文件→新建→网站** 以创建新网站。这将打开 **新建网站** 对话框。
- 3. *选择* **已安装的模板** 窗格中的 **Visual C#**。
- 4. *选择* 中间窗格中的 **ASP.NET 网站** 模板。
- 5. *命名* 它为 **RangeValidatorExample**（也可在 CD 上获取）。
- 6. *单击* **确定** 按钮。这将在 **源** 视图中打开 **Default.aspx** 网页。
- 7. *选择* **设计** 选项卡以查看网页的设计。
- 8. *拖放* 两个 **标签** 控件、两个 **文本框** 控件和一个 **按钮** 控件，从 **工具箱** 的 **标准** 选项卡到 **Default.aspx** 页面上。
- 9. *右键单击* 标签和按钮控件，从上下文菜单中选择 **属性** 选项以打开 **属性** 窗口并设置属性，如表 4.7 所列：

**表 4.7：为控件设置的属性**

| 控件名称 | 属性名称 | 值 |
|---|---|---|
| Label1 | Text | 请输入您的年龄： |
| Label2 | Text | 出生日期（MM/DD/YYYY 格式）： |
| Button1 | Text | 提交 |

- 10. *拖放* 两个 **RequiredFieldValidator** 控件，从 **验证** 选项卡到 **Default.aspx** 页面上。*右键单击* **RequiredFieldValidator1**，从上下文菜单中选择 **属性** 选项以打开 **属性** 窗口并设置属性，如表 4.8 所列：

**表 4.8：为 RequiredFieldValidator 控件设置的属性**

| 控件 ID | 属性名称 | 值 |
|---|---|---|
| RequiredFieldValidator1 | ControlToValidate | TextBox1 |
| RequiredFieldValidator1 | ErrorMessage | 您必须输入年龄。 |
| RequiredFieldValidator2 | ControlToValidate | TextBox2 |
| RequiredFieldValidator2 | ErrorMessage | 您必须输入出生日期 |

- 11. *选择* **工具箱** 中的 **验证** 选项卡。*拖放* 两个 **RangeValidator** 控件到 **Default.aspx** 页面上（图 ASP-4.8）。
- 12. *重新定位* **Default.aspx** 网页上的所有控件，如图 ASP-4.9 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_540_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_540_1.png)

- 13. *右键单击* 每个 **RangeValidator** 控件，从上下文菜单中选择 **属性** 选项以打开 **属性** 窗口并设置属性，如表 4.9 所列：

**表 4.9：为 RangeValidator 控件设置的属性**

| 控件 ID | 属性名称 | 值 |
|---|---|---|
| RangeValidator1 | ControlToValidate | TextBox1 |
| RangeValidator1 | ErrorMessage | 无效的年龄。年龄应介于 18 到 99 之间 |
| RangeValidator1 | Type | Integer |
| RangeValidator1 | MinimumValue | 18 |
| RangeValidator1 | MaximumValue | 99 |
| RangeValidator2 | ControlToValidate | TextBox2 |
| RangeValidator2 | ErrorMessage | 无效的日期。请输入介于 1900/1/1 到 2007/1/1 之间的日期 |
| RangeValidator2 | Type | Date |
| RangeValidator2 | MinimumValue | 1900/1/1 |
| RangeValidator2 | MaximumValue | 2007/1/1 |

添加控件并设置其属性后，将显示 **Default.aspx** 页面，如图 ASP-4.10 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_541_0.png)

图 ASP-4.10

- 14. *按* **F5** 键以在 Web 浏览器中查看输出（图 ASP-4.11）。
- 15. 在 **TextBox1** 和 **TextBox2** 中分别输入值 **11** 和 **12/3/2008**，然后 *单击* **提交** 按钮，如图 ASP-4.12 所示：

