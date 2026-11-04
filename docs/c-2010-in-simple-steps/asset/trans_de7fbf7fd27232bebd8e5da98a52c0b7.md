

12 在“属性”窗口中选择 Items 属性，然后单击省略号按钮（...），如图 C# 6.2 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_189_0.png)

图 C# 6.2

将出现“项集合编辑器”对话框，如图 C# 6.3 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_189_1.png)

图 C# 6.3

在“项集合编辑器”对话框中，可以选择要添加到 toolStrip1 控件的工具条项（按钮、文本框、标签、组合框、下拉按钮或拆分按钮）。还可以使用“项集合编辑器”对话框设置工具条项的属性。

13 单击“选择项并添加到下面的列表”标签下方下拉列表的下箭头，然后选择所需的工具条项，如图 C# 6.4 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_190_0.png)

图 C# 6.4

在图 C# 6.4 中，可以看到我们已选择一个按钮作为工具条项。

14 单击“项集合编辑器”对话框中的“添加”按钮，将所选工具条项添加到 toolStrip1 控件。所选工具条项将添加到“成员”标签下方的列表中，如图 C# 6.5 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_190_1.png)

图 C# 6.5

添加工具条项后，可以在“项集合编辑器”对话框的右窗格中设置其属性。

15 重复步骤 13-14，使用“项集合编辑器”对话框向 toolStrip1 控件添加更多工具条项。表 6.7 列出了添加到 toolStrip1 控件的工具条项及其修改后的属性值：

### 表 6.7：toolStrip1 的工具条项属性的修改值

| 工具条项 | 属性 | 值 |
|---|---|---|
| toolStripButton1 | Text | 新建文件 |
| toolStripButton2 | Text | 打开文件 |
| toolStripButton2 | DisplayStyle | ImageAndText |
| toolStripLabel1 | Text | ToolStrip 演示 |
| toolStripDropDownButton1 | Text | 字号 |
| toolStripDropDownButton1 | DisplayStyle | ImageAndText |
| toolStripDropDownButton1 | DropDownItems | 添加五个菜单项，并将其 Text 属性设置为以下值 |
| toolStripMenuItem1 | Text | 12 |
| toolStripMenuItem2 | Text | 14 |
| toolStripMenuItem3 | Text | 16 |
| toolStripMenuItem4 | Text | 18 |
| toolStripMenuItem5 | Text | 20 |
| toolStripTextBox1 | Text | 输入文本 |
| toolStripSplitButton1 | Text | 编辑 |
| toolStripSplitButton1 | DisplayStyle | ImageAndText |
| toolStripSplitButton1 | DropDownItems | 添加三个菜单项，并将其 Text 属性设置为以下值 |
| toolStripMenuItem6 | Text | 剪切 |
| toolStripMenuItem7 | Text | 复制 |
| toolStripMenuItem8 | Text | 粘贴 |
| toolStripComboBox1 | Text | 字体 |
| toolStripComboBox1 | Items | Arial<br>Times New Roman<br>Courier New<br>Optima<br>Book Antiqua<br>Lucida Console |

所有工具条项都会添加到“成员”列表中（图 C# 6.6）。

16 单击“项集合编辑器”对话框中的“确定”按钮将其关闭，如图 C# 6.6 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_192_0.png)

图 C# 6.6

现在，toolStrip1 控件会出现在设计器中，如图 C# 6.7 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_192_1.png)

图 C# 6.7

17 双击 toolStrip1 控件，并在代码隐藏文件（Form1.cs 文件）中其 ItemClicked 事件内添加清单 6.1 中给出的突出显示代码：

### 清单 6.1：显示要在 toolStrip1_ItemClicked 事件中添加的代码

```
private void toolStrip1_ItemClicked(object sender, ToolStripItemClickedEventArgs e)
{
    MessageBox.Show("You clicked " + e.ClickedItem.Name);
}
```

在清单 6.1 中，e.ClickedItem.Name 属性检索用户单击的工具条项的名称。

18 按 F5 键运行 ToolStripDemo 应用程序。输出将出现，如图 C# 6.8 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_192_2.png)

图 C# 6.8

19 单击工具栏上的任意按钮、下拉按钮、拆分按钮或标签，将出现一个消息框，显示所单击工具条项的名称，如图 C# 6.9 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_193_0.png)

图 C# 6.9

在图 C# 6.9 中，当在工具栏上单击“字号”项时，会出现一个消息框，显示“You clicked toolStripDropDownButton1”。

## 使用 MenuStrip 控件

在使用 Visual Studio 2010 IDE 时，你一定多次使用过菜单栏及其各种菜单。你还可以为自己的 Windows 窗体应用程序设计菜单栏，以便分别对用户可以执行的操作和可以选择的选项进行逻辑分组。可以使用 MenuStrip 控件向 Windows 窗体应用程序添加菜单栏。

MenuStrip 控件充当 Windows 窗体上单个菜单栏的容器。菜单栏包含若干菜单，这些菜单具有经过逻辑分组的菜单项。分组在菜单栏下的菜单项表示用户可选择的选项。菜单项还可以有子菜单，子菜单是包含另一组选项的另一个菜单。

MenuStrip 控件是 MenuStrip 类的实例，该类存在于 System.Windows.Forms 命名空间中。

表 6.8 列出了 MenuStrip 类值得注意的属性：

### 表 6.8：MenuStrip 类值得注意的属性

| 属性 | 描述 |
|---|---|
| CanOverflow | 获取或设置一个值，该值指示 MenuStrip 控件是否支持溢出功能。 |
| GripStyle | 获取或设置 MenuStrip 控件手柄的可见性。GripStyle 属性用于重新定位 MenuStrip 控件。例如，如果将 MenuStrip 控件的 GripStyle 属性设置为 Hidden，则用户无法重新定位 MenuStrip 控件。 |
| ShowItemToolTips | 获取或设置一个值，该值指示是否为 MenuStrip 控件显示工具提示 |
| Stretch | 获取或设置一个值，该值指示 MenuStrip 控件是否在其容器中从头到尾拉伸 |

表 6.9 列出了 MenuStrip 类值得注意的事件：

### 表 6.9：MenuStrip 类值得注意的事件

| 事件 | 描述 |
|---|---|
| MenuActivate | 当用户使用鼠标或键盘从菜单栏访问或打开菜单时发生 |
| MenuDeactivate | 当 MenuStrip 控件停用时发生 |

请注意，MenuStrip 控件只是菜单的容器。菜单和菜单项主要由 ToolStripMenuItem 对象表示，这些对象是 ToolStripMenuItem 类的实例。此类允许你对菜单项和子菜单执行各种操作，例如将菜单项添加到菜单和子菜单、添加菜单分隔符（用于分隔两个或多个菜单的水平线）、为菜单和菜单项指定快捷键，以及显示复选标记。

### 表 6.10：ToolStripMenuItem 类值得注意的属性

| 属性 | 描述 |
|---|---|
| Checked | 获取或设置一个值，该值指示 ToolStripMenuItem 对象是否已选中 |
| CheckOnClick | 获取或设置一个值，该值指定单击时 ToolStripMenuItem 对象是否自动显示为选中或未选中 |
| CheckState | 获取或设置一个值，该值指示 ToolStripMenuItem 对象处于选中、未选中还是不确定状态 |
| Enabled | 获取或设置一个值，该值指示菜单中的子菜单项是否启用 |
| ShortcutKeys | 获取或设置与 ToolStripMenuItem 对象关联的快捷键 |
| ShowShortcutKeys | 获取或设置一个值，该值指示是否在 ToolStripMenuItem 对象旁边显示与其关联的快捷键 |

### 表 6.11：ToolStripMenuItem 类值得注意的事件

| 事件 | 描述 |
|---|---|
| CheckedChanged | 当 Checked 属性更改时发生 |
| CheckStateChanged | 当 CheckState 属性更改时发生 |

要创建子菜单，可以向现有的 ToolStripMenuItem 对象添加多个 ToolStripMenuItem 对象。

> **提示**
> 
> *如果你打算将程序发布给公众使用，则应遵循 Windows 中的各种菜单约定。这些菜单约定如下：*
> 
> - 如果菜单项会打开对话框，则应在其名称后添加省略号（...）（例如“打印...”）。
> - 许多标准快捷键已在使用，例如 CTRL+S 用于保存、CTRL+X 用于剪切、CTRL+V 用于粘贴、CTRL+C 用于复制。因此，不要为这些功能分配任何不同的快捷键。
> - 菜单栏中有某些菜单不会打开菜单，而是立即执行某种操作。因此，类似的即时操作应在其名称后加感叹号（!）（例如“连接!”）。
> - “文件”菜单应始终是第一个菜单，而“退出”项应是该菜单的最后一项。

现在，让我们创建一个名为 MenuStripDemo 的 Windows 窗体应用程序，其中我们将使用 ToolStripMenuItem 类的一些属性和事件。执行以下步骤创建 MenuStripDemo 应用程序：

- 1. 重复本章“使用 ToolStrip 控件”标题下的步骤 1-4。
- 2. 在“新建项目”对话框的“名称”文本框中输入 MenuStripDemo 作为应用程序名称，并在“位置”组合框中输入要保存应用程序的文件夹路径。在本例中，我们选择了默认位置，即 C:\Users\temp\Documents\Visual Studio 2010\Projects。
- 3. 单击“新建项目”对话框中的“确定”按钮。MenuStripDemo 应用程序即创建完成。

