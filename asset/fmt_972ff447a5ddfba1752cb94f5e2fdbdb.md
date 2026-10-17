
```csharp
switch (month)
{
  case 1:
    MessageBox.Show("January");
    break;
  case 2:
    MessageBox.Show("February");
    break;
  case 3:
    MessageBox.Show("March");
    break;
  default:
    MessageBox.Show("Error: Invalid month");
    break;
}
```

在这个示例中，`testExpression` 是 `month` 变量。如果 `month` 变量的值为1，程序跳转到 `case 1:` 部分并执行紧随其后的 `MessageBox.Show("January")` 语句。如果 `month` 变量的值为2，程序跳转到 `case 2:` 部分并执行紧随其后的 `MessageBox.Show("February")` 语句。如果 `month` 变量的值为3，程序跳转到 `case 3:` 部分并执行紧随其后的 `MessageBox.Show("March")` 语句。如果 `month` 变量的值不是 1、2 或 3，程序跳转到 `default:` 部分并执行紧随其后的 `MessageBox.Show("Error: Invalid month")` 语句。

`switch` 语句可以作为对同一个变量或表达式进行多个不同值测试的 `if-else-if` 语句。例如，之前所示的 `switch` 语句像下面的 `if-else-if` 语句一样工作：

```csharp
if (month == 1) {
    MessageBox.Show("January");
} else if (month == 2) {
    MessageBox.Show("February");
} else if (month == 3) {
    MessageBox.Show("March");
}
else {
    MessageBox.Show("Error: Invalid month");
}
```

要查看使用 `switch` 语句的应用程序，请查看本书 `Chap4` 文件夹中的 `Switch Example` 项目。

### 检查点 (Checkpoint)

4.29 将以下 `if-else-if` 代码转换为 `switch` 语句：

```csharp
if (choice == 1)
{
    MessageBox.Show("You chose 1.");
} else if (choice == 2)
{
    MessageBox.Show("You chose 2.");
} else if (choice == 3)
{
    MessageBox.Show("You chose 3.");
}
else
{
    MessageBox.Show("Make another choice.");
}
```

### 4.11 列表框 (Introduction to List Boxes)

### 概念 (Concept)

列表框显示列表并允许用户从列表中选择项目。列表框显示列表并允许用户选择一个或多个项目。在 C# 中，你使用 `ListBox` 控件在表单创建一个列表框。图 4-31 显示了一个表单，带有两个 `ListBox` 控件。运行时，用户可以选择列表中的一个项目，使该项目被选中。

图 4-31 ListBox 示例

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_589_0.png)

图 4-31 中顶部的 `ListBox` 没有滚动条，但底部的有。运行时，用户可以选择列表中的一个项目，使该项目被选中。

在本教程中，你将创建一个应用程序，允许用户从 `ListBox` 控件中选择一个城市。当用户点击按钮时，应用程序将显示该城市时区的名称。图 4-33 显示了应用程序的表单以及列出了所有控件的名称。

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_593_0.png)

图 4-33 颜色主题表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_593_1.png)

**步骤 1：** 启动 Visual Studio 并创建一个名为 `Time Zone` 的 Windows Forms Application 项目。

**步骤 2：** 如图 4-33 所示设置应用程序的表单。
注意表单的 `Text` 属性设置为 `Time Zone`。控件的名称如图所示。在将每个控件放置在表单上时，请参考表 4-9 进行相关的属性设置。

## 表 4-9 控件属性设置

| 控件名称 | 控件类型 | 属性设置 |
| --- | --- | --- |
| promptLabel | Label | **Text:** 选择一个城市，我将告诉你它的时区。 |
| cityListBox | ListBox | **Items:** Denver Minneapolis New York San Francisco |
| outputDescriptionLabel | Label | **Text:** Time Zone: |
| timeLabel | Label | **AutoSize:** False **BorderStyle:** **Text:** （Text 属性的内容已被擦除。） **TextAlign:** MiddleCenter |
| okButton | Button | **Text:** OK |
| exitButton | Button | Text: 退出 |

**步骤 3：** 一旦你设置好了表单及其控件，就可以为 `Button` 控件创建 `Click` 事件处理程序了。在本教程的结束处，程序 4-6 显示了表单的完整代码。在编写事件处理程序时，将被指示参考程序 4-6。

在**设计器（Designer）**中，双击 `okButton` 控件。这将打开代码编辑器，你会看到一个名为 `okButton_Click` 的事件处理程序。通过输入程序 4-6 第 22-53 行所示的代码来完成 `okButton_Click` 事件处理程序。让我们仔细查看代码：

**第 22 行：**此行声明了一个名为 `city` 的 `string` 变量。它用于存储用户从 `ListBox` 中选择的城市名称。

**第 24 行：**此 `if` 语句确定用户是否在 `cityListBox` 控件中选择了一个项。如果选择了某项，控件的 `SelectedIndex` 属性设置为该项的索引（大于 0 的值），程序继续执行第 26 行。然而，如果没有选择任何项，控件的 `SelectedIndex` 属性将设置为 -1，程序跳转到第 49 行的 `else` 分句。

**第 27 行：**此语句从 `ListBox` 中获取选中的项并将其赋值给 `city` 变量。

**第 30 行：**此 `switch` 语句测试 `city` 变量并根据变量的值跳转到其中一个 `case` 语句：

- 如果 `city` 变量等于 "Honolulu"，程序跳转到第 32 行的 case 语句。
- 如果 `city` 变量等于 "San Francisco"，程序跳转到第 35 行的 case 语句。
- 如果 `city` 变量等于 "Denver"，程序跳转到第 38 行的 case 语句。
- 如果 `city` 变量等于 "Minneapolis"，程序跳转到第 41 行的 case 语句。
- 如果 `city` 变量等于 "New York"，程序跳转到第 44 行的 case 语句。

**步骤 4：** 将视图切回设计器并双击 `exitButton` 控件。在代码编辑器中，你会看到一个空的 `exit_Click` 事件处理程序。通过输入程序 4-6 第 58-59 行所示的代码来完成 `exitButton_Click` 事件处理程序。

**步骤 5：** 保存项目并运行应用程序。在 `ListBox` 控件中选择一个城市并点击 `OK` 按钮查看查看时区。测试每个城市，完成后点击 `Exit` 按钮，表单应该关闭。

## 程序 4-6 Time Zone 应用程序的完整 Form1 代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Time_Zone
{
public partial class Form1 : Form
{
public Form1()
{ InitializeComponent(); }
private void okButton_Click(object sender, EventArgs e)

string city; // 用于存储城市名称
if (cityBox.SelectedIndex != -1)
{ // 获取选中的项。
city = cityBox.SelectedItem.ToString();
// 确定时区。
switch (city)
{
case "Honolulu":
timeZoneLabel.Text = "Hawaii-Aleutian";
break;
case "San Francisco":
timeZoneLabel.Text = "Pacific";
break;
case "Denver":
timeZoneLabel.Text = "Mountain";
break;
case "Minneapolis":
timeZoneLabel.Text = "Central";
break;
case "New York":
timeZoneLabel.Text = "Eastern";
break;
}
}
else
{
MessageBox.Show("Select a city.");
}
}

private void exitButton_Click(object sender, EventArgs e)
{
this.Close();
}
}
}
```
