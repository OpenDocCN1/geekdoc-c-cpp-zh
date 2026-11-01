

## C# 编程初学者指南

![](img/41d82527c4e41cdb7e56259564306ddc_87_0.png)

图 5.39. 程序初始状态

![](img/41d82527c4e41cdb7e56259564306ddc_87_1.png)

图 5.40. 已填充的 ListBox

- 10. 现在我们可以通过单击选中 ListBox 中的某个项。然后，我们可以点击“删除选中项”（Remove Selected）按钮来移除选中的项，如图 5.41 所示。该项将被移除，如图 5.42 所示。请注意，如果同一项在 ListBox 中出现多次并被选中删除，该项将从上到下逐个移除。

- 11. 最后，当用户点击“显示项目计数”（Show item count）按钮时，将出现一个消息框显示项目数量，如图 5.43 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_88_0.png)

图 5.41. 从 ListBox 中选中一个项

![](img/41d82527c4e41cdb7e56259564306ddc_88_1.png)

图 5.42. 选中的项已从 ListBox 中移除

![](img/41d82527c4e41cdb7e56259564306ddc_88_2.png)

图 5.43. 消息框中显示项目计数

![](img/41d82527c4e41cdb7e56259564306ddc_90_0.png)

图 5.46. 添加新列

- 5. 再添加两列，并将其 Name 属性分别设置为 **Surname** 和 **Age**。

- 6. 由于 ListView 处于 **大图标**（LargeIcon）视图，这些列还不会显示。我们需要将该属性切换到 **详细信息**（Details），如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_90_1.png)

图 5.47. 设置 View 属性

现在这些列将可见。但是，它们仍未正确对齐。我们可以拖动列以使其在 ListView 控件中适当适应，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_91_0.png)

图 5.48. 调整列的宽度

此操作后，列将适合内部显示，如图 5.49 所示。

此外，通过将 GridLines 属性设置为 True，可以使 ListView 控件的网格线可见，如图 5.50 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_91_1.png)

图 5.49. 列适应 ListView 内部

![](img/41d82527c4e41cdb7e56259564306ddc_92_0.png)

图 5.50. 显示网格线

- 7. 向 ListView 添加项不像分配属性那样简单。相反，我们需要创建一个对象来保存要传递给 ListView 的数据。以下代码片段创建了一个 ListViewItem 对象，用于临时保存我们要写入 ListView 的数据：

```csharp
ListViewItem listvi = new ListViewItem("John");
listvi.SubItems.Add("Cardie");
listvi.SubItems.Add("35");
```

代码 5.12

然后，我们将 listvi 项的内容添加到 ListView 控件，如下所示：

```csharp
listView1.Items.Add(listvi);
```

代码 5.13

这些代码行不会自动执行，我们需要将它们插入到事件方法中。我们可以将它们写在窗体 Form1 的 Load 方法中，这样这些代码行将在窗体加载时（即程序开始运行时）执行。为此，请双击

- 8. 为了指定 MaskedTextBox 的输入格式，我们应该设置掩码。为此，单击 MaskedTextBox 顶部的箭头并选择“设置掩码”（Set Mask），如图 5.54 和 5.55 所示：

![](img/41d82527c4e41cdb7e56259564306ddc_95_0.png)

图 5.54. 打开 MaskedTextBox 菜单

![](img/41d82527c4e41cdb7e56259564306ddc_95_1.png)

图 5.55. 为 MaskedTextBox 设置掩码

在“设置掩码”菜单中，我们可以在各种规范中进行选择。对于本例，我们将选择“电话号码”（Phone number）掩码，如图 5.56 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_97_0.png)

图 5.57. 程序初始视图

我们只能在 MaskedTextBox 中输入电话号码。当我们点击“添加”（Add）按钮时，电话号码将被添加到 ListBox 中，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_97_1.png)

图 5.58. 添加两个电话号码后的程序

### 5.11. MonthCalendar

该控件以月格式显示日历，以便用户从中选择日期。MonthCalendar 与 DateTimePicker 类似。它们的区别在于，MonthCalendar 的日历视图始终打开以选择日期，而用户需要单击 DateTimePicker 才能打开视图选择日期。

MonthCalendar 的属性如下：

- **MinDate**：MonthCalendar 将显示的最小日期。
- **MaxDate**：MonthCalendar 将显示的最大日期。
- **BoldedDates**：用于以粗体显示特殊日期。
- **ShowToday**：设置是否在日历底部显示今天的日期。
- **SelectionStart**：保存选定的开始日期。
- **SelectionEnd**：保存选定的结束日期。
- **SelectionRange**：保存选定的开始日期和结束日期之间的天数范围。

### MonthCalendar 示例：在本例中，让我们在 Label 上显示 MonthCalendar 中选定的开始日期与结束日期之间的天数范围。

- 1. 在 Visual Studio 中创建一个新的 C# 项目。
- 2. 在窗体上放置一个 MonthCalendar 和一个 Label，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_98_0.png)

图 5.59. 窗体布局

- 3. 将 Label 的 Name 设置为 **rangeLabel**，并将其 Text 设置为 **SelectionRange:**。
- 4. 将 MonthCalendar 的 Name 设置为 **selectDates**。
- 5. MonthCalendar 的默认事件是 **DateChanged** 事件，当选定的日期发生变化时触发。因此，双击 MonthCalendar 以创建其默认事件处理方法 `selectDates_DateChanged(...)`。

- 6. 添加以下代码行，以在用户选择日历上的日期范围时显示 SelectionRange：`rangeLabel.Text = selectDates.SelectionRange.ToString();`。添加后，默认事件处理方法将如下所示：

```csharp
private void selectDates_DateChanged(object sender,
DateRangeEventArgs e)
{
    rangeLabel.Text = selectDates.SelectionRange.ToString();
}
```

代码 5.17

- 7. 让我们生成并运行项目。默认情况下，MonthCalendar 控件将自动选中今天的日期，Label 将显示其默认文本：

![](img/41d82527c4e41cdb7e56259564306ddc_99_0.png)

图 5.60. 程序初始视图

现在我们可以从日历中选择日期。为此，单击开始日期，按住鼠标按钮，将鼠标指针拖到结束日期。选定的日期将以灰色背景显示，同时 Label 将显示选择范围，如图 5.61 所示。

值得注意的是，默认最大选择范围为 7 天。您可以通过设置 MonthCalendar 控件的 MaxSelectionCount 属性来更改它。

![](img/41d82527c4e41cdb7e56259564306ddc_100_0.png)

图 5.61. 显示所选范围的 Label

### 5.12. NotifyIcon

该控件用于在 Windows 的通知区域中显示图标。通知区域位于任务栏的右侧，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_100_1.png)

图 5.62. 通知区域

NotifyIcon 的重要属性如下：

- **Icon**：NotifyIcon 的 Icon 属性指定在通知区域中使用哪个图标文件（*.ico）作为应用程序图标。
- **ContextMenuStrip**：指定 NotifyIcon 的右键菜单。

> ContextMenuStrip 是一个菜单组件，用于为右键单击指定菜单，如前一章所述。NotifyIcon 控件通常与 ContextMenuStrip 一起使用。

让我们通过一个示例看看如何在 NotifyIcon 中结合使用 ContextMenuStrip：

- 1. 在 Visual Studio 中创建一个新的 C# 项目。
- 2. 在窗体上放置一个 NotifyIcon 和一个 ContextMenuStrip。当您将这些元素拖放到窗体上时，您会看到它们没有出现在窗体上。这是因为这些元素在后台运行，不显示给用户。拖放操作后，您将在窗体设计窗格下方看到这些元素：

![](img/41d82527c4e41cdb7e56259564306ddc_101_0.png)

图 5.63. 窗体的 NotifyIcon 和 ContextMenuStrip 元素

- 3. 单击 contextMenuStrip1 菜单（如图 5.63 所示），然后它将临时出现在窗体上，以便输入右键菜单，如图 5.64 所示。让我们为本例插入一个“退出”（Exit）项，如图 5.65 所示。

- 4. 现在我们将设置“退出”菜单将执行的操作。为此，双击“退出”项，以便在编辑器中创建其事件处理方法 `exitToolStripMenuItem_Click(...)`，如图 5.66 所示。

- 5. 在此事件处理方法中添加代码行 `Application.Exit();`，这将在执行时导致应用程序退出：

```csharp
private void exitToolStripMenuItem_Click(object sender,
EventArgs e)
{
    Application.Exit();
}
```

代码 5.18

