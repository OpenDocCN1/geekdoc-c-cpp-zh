
或者，你可以通过检查属性窗口中的 `Items` 属性，可视化的向 `ListBox` 和 `CheckedListBox` 添加项。点击省略号按钮会打开字符串集合编辑器，其中包含一个用于添加项的文本区域；每个项单独占一行显示（图 15.17）。随后，Visual Studio 会编写代码将这些字符串添加到 `InitializeComponent` 方法内部的 `Items` 集合中。

![](img/57baed2319be0bb1b5f98674846f2711_658_0.png)

图 15.17 | 字符串集合编辑器。

图 15 使用 `ListBoxForm` 类从显示列表 `displayListBox` 添加、删除和清除项。`ListBoxForm` 类使用 `TextBox` 允许用户输入新项。当用户点击 `Add` 按钮时，新项将出现在 `displayListBox` 中。同样，如果用户选择一个项并点击 `Remove`，该项将被删除。点击 `Clear` 会删除 `displayListBox` 中的所有项目。用户通过点击 `Exit` 程序。

`addButtonClick` 处理程序（20–24）调用 `ListListBox` 中 `Items` 的 `Add` 方法。该方法从 `inputText`（第 22 行）获取用户输入的字符串。在项项后，`inputText` 会清空其内容（第 23 行）。

`removeButtonClick` 处理程序（27–34）使用 `RemoveAt` 方法从列表中删除项。事件处理程序使用第一个属性 `SelectedIndex` 来确定选中了哪个索引。如果 `SelectedIndex` 为 -1（即未选中任何项），第 32 行将删除与所选索引对应的项。

```
// Fig. 15.18: ListBoxForm.cs
// 添加、删除和清除 ListBox 项的程序。
using System;
using System.Windows.Forms;
namespace ListBoxTest
{
    // Form 使用 TextBox 和 Button 来添加、
    // 移除和清除 ListBox 项
    public partial class ListBoxTestForm : Form
    {
        // 构造函数
        public ListBoxTestForm()
        {
```

图 15.18 | 添加、删除和清除 ListBox 项的程序。（3 部分中的第 I）。

## 15.6 ListBox 

```
15 InitializeComponent();
16 }
17 
18 向 ListBox 添加新项（来自输入 TextBox 的文本）
19 // 清空输入 TextBox
20 private void addButton_Click(object sender, EventArgs e)
21 {
22 listBox.Items.Add(inputTextBox.Text);
23 inputTextBox.Clear();
24 }
25 
26 // 如果选中了项，则移除
27 private void removeButton_Click(object sender, EventArgs e)
28 {
29 // 检查是否选中了项；如果是，则移除
30 if (listBox.SelectedIndex != -1)
31 {
32 listBox.Items.RemoveAt(listBox.SelectedIndex);
33 }
34 }
35 
36 // 清空 ListBox 中的所有项
37 private void clearButton_Click(object sender, EventArgs e)
38 {
39 listBox.Items.Clear();
40 }
41 
42 // 退出程序
43 private void exitButton_Click(object sender, EventArgs e)
44 {
45 Application.Exit();
46 }
47 }
48
```

a) 添加 Dog、Cat 和 Chicken 之后添加 Cow 之前的 GUI
b) 添加 Cow 之后删除 Chicken 之前的 GUI

![](img/57baed2319be0bb1b5f98674846f2711_659_0.png)

图 15.18 | 添加、删除和清除 ListBox 项的程序。（3 部分中的第 2 部分。）

删除 Chicken 后的 GUI

清空 ListBox 后的 GUI

![](img/57baed2319be0bb1b5f98674846f2711_660_0.png)

图 15.18 | 添加、删除和清除 ListBox 项的程序。（3 部分中的第 III 部分。）

`clearButton_Click` 事件处理程序（第 37–40 行）调用 `Items` 集合的 `Clear` 方法（第 39 行）。这移除了 `displayListBox` 中的所有条目。最后，事件处理程序 `exitButton_Click`（第 43–46 行）通过调用 `Application.Exit` 方法（第 45 行）终止程序。

## 15.7 CheckedListBox 

`CheckedListBox` 继承自 `ListBox`，并在每个项旁边显示一个复选框。可以通过 `Add` 和 `AddRange` 方法或字符串集合编辑器添加项。`CheckedListBox` 允许勾选多个项，但对项的选择限制更严格。`SelectionMode` 的唯一值是 `None` 和 `One`。`One` 允许单次选择，而 `None` 不允许任何选择。要使某项被勾选，如果你允许用户勾选项，必须将 `SelectionMode` 设置为 `One`。因此，在 `None` 和 `One` 之间切换 `SelectionMode` 可以启用或禁用用户勾选项的能力。`CheckedListBox` 的常用属性、方法和一个事件见图 15.19。

## 常见编程错误 15.1

> 如果你尝试在 CheckedListBox 的属性窗口中将 `SelectionMode` 属性设置为 `MultiSelect` 或 `Extended`，IDE 将显示错误消息。如果通过程序设置此值，则会发生运行时错误。

当用户勾选或取消勾选 CheckedListBox 项时，会发生 `ItemCheck` 事件。事件参数属性 `CurrentValue` 和 `NewValue` 分别返回项当前状态和新状态的 `CheckState` 值。通过对这些值进行比较，你可以判断 CheckedListBox 项是被勾选还是取消勾选。`CheckedListBox` 继承自 `ListBox`。然而，它保留了 `ListBox` 的属性、方法和事件。在 15.20 中，`CheckedListBox` 使用 `ListBox` 来显示用户的选择。在随附的图中，`CheckedListBox` 出现在左侧，`ListBox` 出现在右侧。字符串集合编辑器中的项包含了 C++、Visual Basic 和 C#（缩写为“如何”）。名为 `displayListBox` 显示用户的选择。

| CheckedListBox 属性、方法和事件 | 描述 |
|---|---|
| `CheckedItems` | 运行时可用的项集合。 |
| `CheckedIndices` | 运行时可用的索引。 |
| `SelectionMode` | 决定项被勾选还是取消勾选。 |
| `GetChecked` | 决定项是否被勾选。 |
| `ItemCheck` | 当项被勾选或取消勾选时生成。 |
| `CurrentValue` | 指明项的状态。 |
| `NewValue` | 指明项的新值。 |
| `Index` | 发生变化的项的从零开始索引。 |
| `CheckState` | 可选值为 `Checked`、`Unchecked` 或 `Indeterminate`。 |

`CheckedListBox` 允许勾选多个项，但对项的选择限制更严格。

15.2 

```
15 InitializeComponent();
16 }
17 
18 向 ListBox 添加新项（来自输入 TextBox 的文本）
19 // 清空输入 TextBox
20 private void addButton_Click(object sender, EventArgs e)
21 {
22 listBox.Items.Add(inputTextBox.Text);
23 inputTextBox.Clear();
24 }
25 
26 // 如果选中了项，则移除
27 private void removeButton_Click(object sender, EventArgs e)
28 {
29 // 检查是否选中了项；如果是，则移除
30 if (listBox.SelectedIndex != -1)
31 {
32 listBox.Items.RemoveAt(listBox.SelectedIndex);
33 }
34 }
35 
36 // 清空 ListBox 中的所有项
37 private void clearButton_Click(object sender, EventArgs e)
38 {
39 listBox.Items.Clear();
40 }
41 
42 // 退出程序
43 private void exitButton_Click(object sender, EventArgs e)
44 {
45 Application.Exit();
46 }
47 }
48
```

```
5
6 namespace CheckedListBoxTest
7 {
8     // Form 使用 Checked 将项添加到显示 ListBox
9     public partial class CheckedListBoxForm : Form
10    {
11        // 构造函数
12        public CheckedListBoxForm()
13        {
14            InitializeComponent();
15        }
16 
17        // 项勾选或取消勾选
18        // 添加或从 ListBox 移除
19        private void itemCheckedListBoxCheck(
20            object sender, ItemCheckArgs e)
21        {
22            // 选中项的引用
23            string item = itemCheckedListBox.SelectedItem.ToString();
24 
25            // 如果项被勾选，则添加到 ListBox
26            // 否则从 ListBox 移除
27            if (e.NewValue == CheckState.Checked)
28            {
29                ListBox.Items.Add(item);
30            }
31            else
32            {
33                ListBox.Items.Remove(item);
34            }
35        }
36    }
37 }
```

a) 程序执行时显示的初始 GUI

b) 选中前三个项后的 GUI
c) 取消选中 C++ 后的 GUI
d) 勾选 C# 后的 GUI
