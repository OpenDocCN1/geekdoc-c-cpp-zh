
## 描述

- 每个标签可以包含两个或多个页。要添加标签，右键点击控件并选择 `Add` 命令。
- 设置标签的文本，选择标签并使用 `Text` 属性。
- 移除标签，右键点击标签并选择 `Delete` 命令。
- 你还可以通过 `TabPages` 添加、移动和删除标签。
- 你可以使用控件的 `SelectedIndex` 属性确定选择了哪个标签。
- 当选择另一个标签时会发生 `SelectedIndexChanged` 事件。

图 24-3 如何使用 Tab 控件

# 如何向表单添加菜单

为了访问应用程序的功能，你可以向表单添加菜单。菜单有时会重复按钮中已有的功能，但它们也可以提供其他处不可用的功能。

# 如何创建菜单

Visual Studio 为向表单添加菜单提供了易于使用的set。要执行此操作，你首先如图 24-4 所示向表单添加 `MenuStrip` 控件。当你添加此控件时，表单的 `MainMenuStrip` 属性会自动设置为该控件的名称，但它不会显示在表单上。相反，它显示在底部的组件设计器中。

向表单添加 `MenuStrip` 控件后，顶部会显示菜单设计器。然后，你可以通过在菜单设计器显示“在此输入”的地方输入你想要显示的文本来添加菜单和菜单项。当你输入第一个菜单的文本时，该菜单的下方和右侧会打开额外的区域。因此，输入新菜单、子菜单和菜单项非常方便。对于其他控件，在输入菜单项文本时可以使用取位符 (`&`) 来提供访问键。此外，你可以通过为菜单项文本使用破折号 (`-`) 来创建分隔条。一旦你为应用程序创建了菜单和菜单项，你可以轻松地右键点击菜单名称并从快捷菜单中选择“编辑下拉项”命令。这将显示“项目集合编辑器”对话框，方便你编辑每个菜单项的名称或设置项的任何其他属性。此对话框还允许你添加、移动和删除菜单项。

在设置每个菜单项的名称时，通常的约定使用 `mnu` 作为每个菜单项的前缀。例如，你可能使用 `mnuActionClear` 作为操作菜单中“清除”项的名称。否则，你可以接受菜单设计器分配的默认名称。例如，操作菜单中“清除”项的默认名称将是 `clearToolMenuItem`。如果你需要在菜单中插入新项，可以右键点击菜单项以显示快捷菜单。然后，你可以从插入子菜单中选择“项”命令来插入新项。或者，你可以从插入子菜单中选择“分隔符”命令来插入一个分隔条。此外，菜单项的快捷菜单提供了剪切、复制、粘贴和删除命令。

# Future Value 表单菜单的开始

![](img/3148667e42d4db35b3d08576aaa1fa01_758_0.png)

# 完整的 Action

![](img/3148667e42d4db35b3d08576aaa1fa01_758_1.png)

# 

- 要向表单添加菜单，请向表单添加 `MenuStrip` 控件。该控件将出现在表单设计器底部的组件设计器面板中，表单的 `MainMenuStrip` 属性将被设置为该控件名称。
- 要向菜单添加项，请点击菜单设计器中的“Type Here”（在此输入）处。然后输入菜单项的文本并按回车键。输入项下方和右侧会出现额外的输入区域。
- 若要编辑每个菜单项的名称，右键点击菜单名称，从快捷菜单中选择“Edit DropItems”命令。这将显示一个对话框，方便您编辑菜单上每个项的 `Menu` 属性。
- 若要插入新项（包括分隔符线），右键点击菜单项显示其快捷菜单，并从“Insert”子菜单中选择命令。

图 24-4 如何创建菜单

# 如何设置与菜单项相关的属性

您创建的每个菜单项都是独立的对象，拥有自己的属性。当您使用上图所示的技术创建菜单或菜单项时，您可以使用菜单设计器及其快捷菜单来设置每个菜单项的属性。通常，这是设置菜单项属性最简单的方法。不过，您也可以使用属性窗口来更改所选菜单项的属性。

图 24-5 总结了您最可能使用的某些菜单项属性。首先，您可以使用表单设计器在设计时设置这些属性。例如，您可以使用 `ShortcutKeys` 和 `ShowShortcutKeys` 来定义并显示菜单项的快捷键（如 `Ctrl+C`）。然后，如有必要，可以使用代码在运行时更改这些属性。例如，您可以使用 `Checked` 属性在菜单项旁边显示或隐藏勾选标记。或者，您可以使用 `Enabled` 和 `Visible` 属性来禁用或隐藏菜单项。

# 如何编写与菜单项配合的可互通的代码

图 24-5 中的第一个示例显示了 Action 菜单中 Clear 项的事件处理器。由于 `Click` 事件是菜单项的默认事件，您可以通过在菜单设计器中双击菜单项来生成事件处理器的声明。然后，您可以使用代码编辑器输入由事件处理器执行的代码。

第二个示例显示了 Action 菜单 `Click` 事件的处理器。由于此菜单项提供了与 Calculate 按钮相同的功能，该事件处理器中的唯一语句调用了 Calculate 按钮 `Click` 事件的事件处理器。为了使其正常工作，`mnuCalculate_Click` 方法的两个参数都作为 `binCalculate_Click` 方法的参数提供。

第三个示例显示了处理 Action 菜单中 Calculate 项 `Click` 事件的另一种方法。在这里，此事件处理器调用了 Calculate 按钮的 `PerformClick` 方法。这将导致 Calculate 按钮 `Click` 事件的事件处理器。

当然，您可以通过将两个事件都绑定到同一个事件处理器来更优雅地处理这种情况。例如，您可以将 Calculate 菜单项的 `Click` 事件和 Calculate 按钮的 `Click` 事件绑定到名为 `Calculate_Click` 的事件处理器。有关绑定事件处理器的复习课程，请参阅第 6 章。

# 常见菜单项属性

| 属性 | 说明 |
| --- | --- |
| `Text` | 显示在菜单中的文本。若要为菜单项提供访问键，请在此属性中包含一个和符号 (`&`)。 |
| `Name` | 代码中用于引用菜单项的名称。 |
| `Checked` | 决定选中菜单项时左侧是否出现勾选标记。 |
| `Enabled` | 决定菜单项是可用还是置灰。如果菜单项被禁用或启用，其所有子项也会被禁用或启用。 |
| `Visible` | 决定菜单项是显示还是隐藏。如果菜单项被隐藏或显示，其所有子项也会被隐藏或显示。 |
| `ShortcutKeys` | 指定与菜单项相关的快捷键。 |
| `ShowShortcutKeys` | 决定是否在菜单项右侧显示快捷键。 |

# 清四个控件的菜单项代码

```csharp
private void mnuClear_Click(object sender, System.EventArgs e)
{
    txtMonthlyInvestment.Text = "";
    txtInterestRate.Text = "";
    txtYears.Text = "";
    txtFutureValue.Text = "";
}
```

# 调用另一个事件处理器的代码

```cs
private void mnuCalculate_Click(object sender, System.EventArgs e)
{
    btnCalculate_Click(sender, e);
}
```

# 调用另一个事件处理器的另一种方法

```cs
private void mnuCalculate_Click(object sender, System.EventArgs e)
{
    btnCalculate.PerformClick();
}
```

# 注意事项

- `Click` 事件是菜单项的默认事件。您可以像处理任何其他 `Click` 事件一样为该事件编写事件处理器。
- 如果菜单项执行相同的代码，您可以将它们都绑定到同一个事件处理器上。

![](img/3148667e42d4db35b3d08576aaa1fa01_758_1.png)

# 垂直排列三个子窗的 MDI 应用程序

| 财务计算 | | | | |
| 文件 | 视图 | 窗口 | | |
| :--- | :--- | :--- | :--- | :--- |
| 未来价值 | 级叠排列 | | | SYD 折旧 |
| | 垂直平铺 | | | 资产初始成本: 2000 |
| 操作 | 水平平铺 | | | 资产最终价值: 0 |
| 每月投资 | 1 个未来价值 | | | 资产寿命（年）: 6 |
| 年利率 | 2 个未来价值 | | | SYD 折旧: 第1年: 5566.67 |
| 年限数 | 3 次 SYD 折旧 | | | 第2年: 5415.35 |
| 未来价值 | $3771.45 | | | 第3年: 5268.62 |
| | 计算 | 关闭 | | | 第4年: 5133.33 |
| | | $3830.88 | | | |

```csharp
private void mnuNewFutureValue_Click(object sender, System.EventArgs args)
{
    Form newForm = new frmFutureValue();
    newForm.MdiParent = this;
    newForm.Show();
}
```

创建并显示子窗体新实例的代码

引用子窗体的代码

```csharp
private void mnuClose_Click(object sender, System.EventArgs args)
{
    Form activeForm = this.ActiveMdiChild;
    if (activeForm != null)
    activeForm.Close();
}
```

将子窗体垂直排列的代码

```csharp
private void mnuTileVertical_Click(object sender, System.EventArgs args)
{
    this.LayoutMdi(MdiLayout.TileVertical);
}
```

退出应用程序并关闭所有子窗体的代码

```csharp
private void mnuExit_Click(object sender, System.EventArgs args)
{
    Application.Exit();
}
```

## 描述

- 你可以通过通过设置菜单条的 `MdiWindowListListItem` 属性为菜单的名称，在菜单中显示打开的子窗体列表。列表通常显示在“窗口”菜单中。
- 在此示例中，“操作”菜单存储在子窗体内。当包含该菜单的子窗体成为活动窗时，该菜单会出现在父窗中。

图 24-7 如何编写处理父子窗体的代码

# 如何向窗体添加工具栏

在本章的前面的部分，你学习了如何向窗体添加菜单以提供访问应用程序的功能。现在，你将学习如何添加工具栏。
在大多数情况下，工具栏上的按钮与菜单系统提供的功能重复。然而，工具栏按钮允许用户通过单击即可访问这些功能。

# 如何创建工具栏

要创建工具栏，你需要向窗体添加一个 `ToolStrip` 控件。与 `MenuStrip` 控件一样，该控件出现在组件设计器工具箱中。默认情况下，它将停靠在窗体的顶部，位于窗体上任何菜单下方，并跨越窗体的整个宽度。
图 24-8 展示了工具栏两个示例。在这里，第一个工具栏包含了保存、打印、剪切和粘贴等功能的标准工具栏按钮。你可以使用 `ToolStrip` 智能菜单中的“插入项”命令创建这样的工具栏。第二个工具栏有两个自定义按钮，允许用户显示“未来价值”。要添加自定义按钮，可以使用此图中所示的“集合编辑器（Items Collection Editor）”。默认情况下，你添加到工具栏的每个按钮都会显示图形。要为按钮指定图像，您可以使用按钮的 `Image` 属性显示一个对话框，允许你选择图像。在此图中，第二个工具栏中的两个按钮使用存储在 `bmp` 文件中的图像，而这些 `bmp` 文件存储在相同目录下。如果你正在处理图形，可以创建自己的图形。或者你可能可以在互联网上找到可以使用的图像。

为按钮指定了合适的图像后，你需要设置按钮的 `Text` 属性。当你设置此属性时，它会自动设置 `ToolTip` 属性，该属性指定了当用户将指针悬停在按钮上时显示的文本。这种文本被称为工具提示（tooltip），它很重要，因为用户往往很难仅从按钮的图像判断其的功能。然而，如果用户指向第一个按钮，它将显示为“打开未来价值”的工具提示，这让用户清楚地知道按钮的作用。

默认情况下，你添加到工具栏的项显示为推入按钮（push buttons）。你可以通过从“项集合”对话框顶部的组合框中选择不同类型的项来创建其他类型的工具栏项。例如，如果你从此组合框中选择 `DropDown`，你可以创建一个从按钮处弹出的菜单。通过一些实验，你应该能够使用此对话框向工具栏添加各种控件。

# 第 24 章如何增强用户界面

# 带有标准项的 ToolStrip
img/3148667e42d4b35b3d08576aaa1fa01_766_0.png

# 带有两个自定义按钮的 ToolStrip
img/3148667e42d4b35b3d08576aaa1fa01_766_1.png

# ToolStrip 的项集合对话框
img/3148667e42d4b35b3d08576aaa1fa01_766_2.png

## 描述

- 要创建工具栏，向窗体添加 `ToolStrip`。默认情况下，工具栏停靠在窗体顶部，位于菜单下方并跨越窗体宽度。
- 要插入上述项，请从 `ToolStrip` 控件的智能标记菜单中选择“插入项”命令。
- 要显示 `ToolStrip` 的项集合对话框，从 `ToolStrip` 的智能标记菜单中选择“编辑项”命令。你可以使用此对话框向工具栏添加按钮并设置这些按钮的属性。
- 要在一个按钮上包含图像，你可以使用按钮的 `Image` 属性显示对话框，允许你为按钮指定图像文件。此对话框支持现代图像文件，包括 `gif`、`jpg`、`bmp`、`wmf` 和 `png`。
- 要指定用户用鼠标指向按钮时显示的文本（称为工具提示），你可以在按钮的 `Text` 属性中输入文本。这会自动设置按钮的 `ToolTip` 属性。

图 24-8 如何创建工具栏

# 如何编写处理工具栏的代码

在你为窗体创建工具栏后，需要编写让它们工作的代码。为了这样做，你可以像图 24-9 这样编写事件处理程序。

第一个示例显示或隐藏工具栏。它使用了未来价值菜单项的 `PerformClick` 方法。这样，你就不需要重复创建和显示窗体的代码。

第二个示例显示或隐藏工具栏。在这种情况下，主菜单中添加了视图菜单，该菜单包含一个名为 `mnuToolbar` 的单个菜单项。此项的点击事件使用菜单项的 `Checked` 属性来判断工具栏是否当前显示。如果是，它将工具栏的 `Visible` 属性设置为 `false` 将其隐藏。相反，如果菜单项的 `Checked` 属性为 `false`，则将其设置为 `true` 以显示勾标记，并将工具栏的 `Visible` 属性设置为 `true` 以显示工具栏。

另一种编写此处理程序的方法如下：

```csharp
mnuToolbar.Checked = !mnuToolbar.Checked;
lblMain.Visible = !lblMain.Visible;
```

在这里，使用了非运算符 `!` 来反转菜单项的 `Checked` 属性和工具栏的 `Visible` 属性。虽然这种代码没有图中代码那么容易理解，但这种类型的非常常见。

# ToolStrip 按钮点击事件的代码

```csharp
private void btnFutureValue_Click(object sender, EventArgs e)
{
    mnuNewFutureValue.PerformClick();
}
```

# 显示或隐藏工具栏的视图菜单
img/3148667e42d4b35b3d08576aaa1fa01_768_0.png

# 根据菜单选择显示或隐藏工具栏的代码

```csharp
private void mnuToolbar_Click(object sender, System.EventArgs e)
{
    if (mnuToolbar.Checked == true)
    {
        mnuToolbar.Checked = false;
        lblMain.Visible = false;
    }
    else if (mnuToolbar.Checked == false)
    {
        mnuToolbar.Checked = true;
        lblMain.Visible = true;
    }
}
```
