
为了添加功能，将 `btnNew` 按钮对象设置为 `Form` 对象的 `AcceptButton` 属性的值。这允许用户在输入新条目后按 Enter 键。现在，Enter 键的功能与点击 `btnNew` 按钮对象的左鼠标键相同。当用户点击鼠标或按下 Enter 键时，会触发 `btnNew_Click()` 事件。在 `btnNew_Click()` 事件处理方法中，还使用 `Clear()` 方法清空了 `TextBox` 对象。这是在值输入到 `TextBox` 对象、被检索并添加到 `ListBox` 对象之后完成的。表 10-1 包含了为 ListBoxExample 应用程序设置的属性列表。

## 表 10-1 ListBoxExample 属性值

| 名称 | 对象类型 | 值 |
|---|---|---|
| ClubForm | Form | AcceptButton | btnNew |
| ClubForm | Form | BackColor | Blue (128,128,255) |
| ClubForm | Form | Font | SansSerif, 12 |
| ClubForm | Form | Text | 输入 "Computer Club Outing Sign Up" |
| 1stEvents | ListBox | BackColor | Yellow (255,255,192) |
| 1stEvents | ListBox | ForeColor | Blue (0,0,192) |
| 1stEvents | ListBox | SelectionMode | MultiExtended |
| 1stEvents | ListBox | Sorted | true |
| 1stEvents | ListBox | TabIndex | 1 |
| 1stEvents | ListBox | Items (集合) | 输入 "Amusement Park", "Boat Tour", "Dance", "Dinner", "Movie", "Sporting Event" |
| label1 | Label | Text | 输入 "Result" |
| label2 | Label | Text | 输入 "Select Event(s)" |
| label3 | Label | Text | 输入 "Add an Activity" |
| btnNew | TextBox | Text | 输入 "Add New One" |

示例 10-15 仅接触了 ListBox 对象可以做的一些皮毛。你想进一步探索此类。`Items`、`SelectedItems` 和 `SelectedIndices` 属性对于从 `ListBox` 对象获取选中项集合非常有用。除了在设计时输入值有用外，`ListBox` 对象还是一个可以在运行时填充新值的控件。通过在循环内部包含 `Add()` 方法，可以在应用程序运行期间将用户输入的值或从文件或数据库表中读取的值添加到控件中。表 10-2 描述了 `ListBox` 类的一些最有趣的的属性。

> 表 10-2 和 10-3 中包含的信息改编自 MSDN 文档。

## 表 10-2 ListBox 属性

| 属性 | 描述 |
| --- | --- |
| Items | 获取列表框中的值（项） |
| MultiColumn | 获取或设置一个值，指示列表框是否支持多列 |
| SelectedIndex | 获取或设置当前选中项的从零开始的索引 |
| SelectedIndices | 获取包含所有当前选中项的从零开始索引的集合 |
| SelectedItem | 获取或设置选中项 |
| SelectedItems | 获取一个包含当前选中项的集合 |
| SelectionMode | 获取或设置选择项目的方法（MultiExtended, MultiSimple, One, None） |
| Sorted | 获取或设置一个值，指示项目是否按字母顺序排序 |
| Text | 获取或搜索当前选中项的文本 |

表 10-3 给出了 `ListBox` 对象方法和事件的部分列表。请记住 `ListBox` 对象还继承了 `Control` 类的成员。第 9 章中的表 9-2 和 9-3 列出了 `Control` 类的许多成员。你应该复习那些表格。

## 表 10-3 ListBox 方法

| 方法（及事件） | 描述 |
| --- | --- |
| ClearSelected() | 取消所有项目的选择 |
| Enter() - 事件 | 进入控件时发生 |
| FindString() | 查找第一个与指定字符串开头的项 |
| FindStringExact() | 查找第一个完全匹配指定字符串的项 |
| Focus() - 事件 [继承自 Control] | 控件接收焦点时发生 |
| KeyPress() - 事件 [继承自 Control] | 控件拥有焦点时按下按键时发生 |
| Leave() - 事件 [继承自 Control] | 输入焦点离开控件时发生 |
| MouseEnter() - 事件 [继承自 Control] | 鼠标指针进入控件时发生 |
| MouseHover() - 事件 [继承自 Control] | 鼠标指针悬进入控件时发生 |
| MouseLeave() - 事件 [继承自 Control] | 鼠标指针离开控件时发生 |
| SelectedChanged() - 事件 [继承自 Control] | 选择发生变化时发生 |
| SetSelected() | 选择或清空选择 |

与 ListBox 类似的控件是 ComboBox。

当输入到文本区域时，它们可以被检索和处理。示例 10-16 显示了为 ComboBox 控件注册的两个事件。注意 ComboBox 对象的 `Name` 属性已设置为 `cmboFlowers`。

### 10-16

```
this.cmboFlowers.SelectedIndexChanged += new System.EventHandler
(this.cmboFlowers.SelectedIndexChanged);
this.cmboFlowers.KeyPress += new
    System.Windows.Forms.KeyPressEventHandler
    (this.cmboFlowers_KeyPress);
```

ComboBox 对象的另一个选项是 `TextChanged()` 事件。`Changed()` 是 TextBox 对象的默认事件处理器。如果通过程序修改或用户交互更改了 `Text` 属性，就会触发 `Changed()` 事件。

## 编写事件处理器

针对图 10-7 所示的 ComboBox 和 ListBox 对象，编写了三个事件处理方法。添加了新的 TextBox 对象以存储从这些控件中检索的值。`cmboFlowers_SelectedIndexChanged()` 方法和 `cmboFlowers_KeyPress()` 方法都使用 `Text` 属性从 ComboBox 对象获取值。在检索值后，两个方法都为关联 TextBox 对象设置了文本。这两个事件处理器的主体包含以下语句：

```
this.TextBoxResult.Text = cmboFlowers.Text;
```

## 使用集合索引

由于 ListBox 对象允许多项选择，因此无法使用 `Text` 属性。`Text` 获取的是单个选择，即第一个被选中的项。要检索所有选择，你有几种选项。可以使用 `SelectedItems`、`SelectedIndexes` 或 `Items` 方法来检索选中的项目集合。这些集合是类似于数组的零索引结构。你可以利用它们类数组的特性，像访问数组元素一样访问它们。

`SelectedIndex` 是一个索引集合。因此，如果选择了第一个、第三和第七个项目，`SelectedIndices` 集合将包含 0、2 和 6，因为该集合是从零开始的。

可以使用 `int` 来遍历 `SelectedIndexes` 集合，如示例 10-17 所示。

### 示例 10-17

```
private void lstBoxTrees_SelectedIndexChanged(object sender,
    System.EventArgs e)
{
    this.txtBoxResultTrees.Text = " ";
    foreach (int i in lstBoxTrees.SelectedIndices)
    {
        this.txtBoxResultTrees.Text +=
        this.lstBoxTrees.Items[i] + " ";
    }
}
```

将示例 10-17 所示的事件处理器方法与示例 10-12 所示的 ListBox `SelectedIndexChanged()` 事件处理器方法进行比较。示例 10-12 使用 `SelectedItems` 属性访问项目，而不是 `SelectedIndices` 属性。示例 10-17 中的语句不是通过检索项目来访问选择，而是检索了索引。添加这些事件处理器方法后应用程序产生的输出如图 10-8 所示。

![](img/45e6f245af31396d967c3186f196d331_597_0.png)

图 10-8 触发的 KeyPress 和 SelectedChanged 事件

## MenuStrip 控件对象

Sunflower 在设计时没有放在集合列表中；它是在程序启动时输入的。`KeyPress()` 事件处理器在按下（多次）时触发。记住 `KeyPress()` 在每按下一个字符时都会触发。因此，在输入字符 S 时会触发；在输入字符 u 时再次触发，以此此类推。因此 `KeyPress()` 方法执行多次，以便从组合框获取字符并将它们显示在文本框中。`KeyPress()` 方法使用 ComboBox 的 `Text` 属性获取选择，并使用 TextBox 的 `Text` 属性设置显示属性的值。

从 ListBox 对象进行了两项选择。`SelectedIndexChanged()` 方法通过将选择项拼接 (+) 到 `Text` 属性中，设置了 TextBox 对象的文本。

大多数 Windows 应用程序包含许多菜单选项。在下一节中，你将为此应用程序添加菜单，并学习添加大多数 Windows 应用程序中常见的传统菜单是多么简单。

## MENSTRIP 控件对象

菜单的优点是占据窗口空间极小。它们允许你通过向用户提供额外选项来为应用程序添加更多功能。在 `System.Windows.Forms` 命名空间中提供了许多类，可以让你为应用程序添加多层菜单。

## 添加菜单

.NET Framework 类之一是 `MenuStrip` 类。`MenuStrip` 替换并增强了以前版本中单独控件的功能。保留 `Main` 是为了向后兼容以及以后如果你需要可以使用。使用 Visual Studio 工具箱可以轻松地将 `MenuStrip` 控件对象拖放到表单上。当你执行此操作时，代表 `MenuStrip` 对象的图标将放置在设计窗口下方称为“组件托盘”（Component Tray）的灰色区域。选择 `MenuStrip` 对象可以让你设置其属性，例如在属性窗口设置 `Name`。要为菜单选项添加文本，选择 `MenuStrip` 图标，然后点击表单左上角，如图 10-9 所示，那里显示“Type Here”字样。

![](img/45e6f245af31396d967c3186f196d331_599_0.png)

图 10-9 创建菜单的第一步

菜单结构是通过输入菜单选项的文本创建的，如图 10-9 所示。

## 第 10 章 基于事件的编程

![](img/45e6f245af31396d967c3186f196d331_601_0.png)

图 10-11 添加分隔符

如果你使用的是 `MainMenu` 控件而不是 `MenuStrip` 控件，必须拖动表单上的 `Menu` 属性来设置菜单上显示的文本，即 `MainMenu` 对象的名称。否则，启动应用程序时菜单将不会显示。如果你使用 `MenuStrip` 控件，则不需要设置此属性，系统会自动为你完成关联。

你可以为控件（如文本框或菜单项）分配工具提示（ToolTip），这样当光标悬停在组件上方时就会显示文本。要创建工具提示，从工具箱中拖入 `ToolTip` 控件并到表单任意位置。它将位于表单下方的组件区中。`ToolTip` 不与任何特定的控件对象关联。将其放置在表单后，控件的属性窗口中就会多出一个新属性。要为特定控件定义工具提示，选择该控件并在属性窗口的 `ToolTip` 属性中输入你想要显示的内容。例如，为了提醒用户可以在持有树名称的列表框中进行多选，`lstBoxTrees` 控件的 `ToolTip` 属性被设置为“按住 Ctrl 键进行多项选择”，如图 10-12 所示。

## MenuStrip 控件对象

![](img/45e6f245af31396d967c3186f196d331_602_0.png)

图 10-12 设置 ToolTip 属性

当你使用 `MenuStrip` 控件创建结构时，会为你输入的可选菜单选项创建独立的 `ToolStripMenuItem` 对象。完成布局后，可以在选择属性窗口中的 `Name` 属性之前，先选择单个菜单项来设置这些 `ToolStripMenuItem` 对象的 `Name` 属性。如果菜单项将绑定到事件，这一点尤为重要，因为控件的名称将成为事件处理方法名称的一部分。

将方法绑定到如菜单选项之类的事件上，意味着你将事件与特定方法关联。在方法绑定到选项后，当点击菜单选项时，会自动执行该方法。当菜单选项被点击时，可以认为事件被触发（或引发）。这是事件驱动程序开发前的底层概念之一。

![](img/45e6f245af31396d967c3186f196d331_602_1.png)

在表单设计器中选择每个 `ToolStripMenuItem` 后，在属性窗口中设置了 `menuExit`、`menuFont`、`menuColor` 和 `menuHelp` 等属性名称。通过双击选项可以注册点击事件。表单设计器会生成相应的点击事件处理方法。`menuExit` 选项的点击事件方法名为 `menuExit_Click()`；`menuFont` 选项的处理器程序为 `menuFont_Click()`。

## 第 10 章 基于事件的编程

如果你在将事件处理程序绑定到菜单项后为该项命名，那么事件处理方法将不包含控件的名称。这不会影响结果，只是会导致代码可读性降低。你实际上可以更改方法名以匹配控件名称；但是，如果你这样做，也必须同时更改将事件处理程序绑定到对象的语句中的方法名。

当你在表单上放置 `MenuStrip` 时，控件的智能标签（smart tag）会显示一个名为“插入标准菜单项”的选项。选择此选项会在表单顶部放置“文件”、“编辑”、“工具”和“帮助”。在“文件”菜单中会获得标准选项（新建、打开、保存、另存为、打印、打印预览和退出）。撤销、重做、剪切、复制、粘贴和全选会自动添加到“编辑”菜单中。当然，你可以根据需要添加额外选项或移除任何不想包含在应用程序中的项。

“退出”和“关于”菜单项的点击事件处理方法如示例 10-18 所示。

### 示例 10-18

```c
private void menuExit_Click(object sender, System.EventArgs e)
{
    Application.Exit(0);
}
```

```c
private void menuAbout_Click(object sender, System.EventArgs e)
{
    MessageBox.Show("园艺指南应用程序\n\n版本" + "1.0", "关于园艺");
}
```

当用户点击“关于”选项时，会显示消息对话框。当用户点击“退出”选项时，所有窗口将关闭且程序终止。

## 添加内置标准 Windows 对话框

NET 包含了一些预配置的对话框。它们包括看起来类似于标准 Windows 文件打开、文件保存、文件打印、文件打印预览、格式和格式颜色的对话框。通过将控件对象拖放到表单上，可以将其添加到你的应用程序中。图 10-13 显示了控件的部分列表，突出显示了 `FontDialog` 和 `ColorDialog` 控件。

![](img/45e6f245af31396d967c3186f196d331_604_0.png)

### 图 10-13 将对话框添加到菜单项

为了查看字体和颜色的效果，控件的智能标签会显示一个名为“插入标准菜单项”的选项。选择此选项会在表单顶部放置“文件”、“编辑”、“工具”和“帮助”。在“文件”菜单中会获得标准选项（新建、打开、保存、另存为、打印、打印预览和退出）。撤销、重做、剪切、复制、粘贴和全选会自动添加到“编辑”菜单中。你可以根据需要添加额外选项或移除任何不想包含在应用程序中的项。

“退出”和“关于”菜单项的点击事件处理方法见示例 10-18。

### 示例 10-20

```sharp
// GardeningForm.cs    Author: Doyle
// 设计中包含了 Menu, ListBox, ComboBox, Label 和 TextBox
// 对象。编写了 KeyPress()、
// Click( ) 和 SelectedIndexChanged( ) 事件。添加了字体（Font）和颜色（Color）对话话框。
using System;
using System.Drawing;
using System.Collections.Generic;
```
