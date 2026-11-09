
**ComboBox** 控件的功能。表 3.11 列出了 **ComboBox** 类的重要属性：

**表 3.11：ComboBox 类的重要属性**

| **属性** | **描述** |
|---|---|
| DrawMode | 获取或设置一个值，该值指示由代码还是操作系统处理列表元素的绘制 |
| DropDownHeight | 获取或设置一个值，用于指定组合框下拉部分的高度 |
| DropDownStyle | 获取或设置一个值，用于指定组合框的样式 |
| DropDownWidth | 获取或设置一个值，用于指定组合框下拉部分的宽度 |
| DroppedDown | 获取或设置一个值，该值指示是否显示 ComboBox 控件的下拉列表 |
| IntegralHeight | 获取或设置一个值，该值指示 ComboBox 控件是否调整自身大小以完整显示其项 |
| ItemHeight | 获取或设置一个值，用于指定 ComboBox 控件中项的高度 |
| Items | 获取 ComboBox 控件中可用项的集合 |
| MaxDropDownItems | 获取或设置一个值，用于指定 ComboBox 控件下拉列表中可显示的最大项数 |
| MaxLength | 获取或设置一个值，用于指定 ComboBox 控件可编辑文本字段中可输入的最大字符数 |
| SelectedIndex | 获取或设置当前选定项的索引 |
| SelectedItem | 获取或设置当前选定的项 |
| SelectedText | 获取或设置 ComboBox 控件可编辑文本字段中当前选定的文本 |
| Sorted | 获取或设置一个值，该值指示 ComboBox 控件中的项是否按字母升序排序 |

表 3.12 列出了 **ComboBox** 类的重要方法：

**表 3.12：ComboBox 类的重要方法**

| **方法** | **描述** |
|---|---|
| BeginUpdate | 在向控件添加项时通过防止闪烁来保持 ComboBox 控件的性能。在调用 EndUpdate 方法之前，它不会绘制该控件。 |
| EndUpdate | 在绘制被 BeginUpdate 方法暂停后，恢复绘制 ComboBox 控件。 |
| FindString | 查找 ComboBox 控件中第一个以指定字符串开头的项。 |
| FindStringExact | 查找 ComboBox 控件中第一个与指定字符串完全匹配的项。 |
| GetItemHeight | 返回 ComboBox 控件中特定项的高度，以像素为单位。 |
| ResetText | 重置 ComboBox 控件可编辑文本字段中的文本。 |
| Select | 选择 ComboBox 控件可编辑文本字段中的一段文本。 |
| SelectAll | 选择 ComboBox 控件可编辑文本字段中的所有文本。 |

执行以下步骤，在 Windows 窗体应用程序中使用 **ComboBox** 控件：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中*选择* File→New→Project。新建项目对话框打开。
- 3. 从 **New Project** 对话框左窗格的 **已安装的模板** 部分中选择 **Visual Basic→Windows**。
- 4. 在中间窗格中选择 **Windows 窗体应用程序** 模板以创建 Windows 窗体应用程序。
- 5. 在 **名称** 文本框中输入应用程序的名称 **ComboBoxControl**（也可在 CD 上获得），并在 **位置** 组合框中输入应用程序的适当位置。
- 6. 单击 **确定** 按钮关闭 **新建项目** 对话框。**ComboBoxControl** 应用程序已创建（图 VB-3.20）。
- 7. 从 **工具箱** 中将一个 **Label** 控件、一个 **ComboBox** 控件和一个 **TextBox** 控件拖放到 **Form1** 窗体上。
- 8. 使用 **属性** 窗口，将 **Label** 控件和 **ComboBox** 控件的 **Text** 属性分别设置为 *选择你出生的月份：* 和 *[选择]*。设置属性后，窗体如图 VB-3.20 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_133_0.png)

图 VB-3.20

- 9. 在窗体中选择 **ComboBox** 控件，在 **属性** 窗口中选择 **ComboBox** 控件的 **Items** 属性，并单击该属性前面的省略号按钮 (...)。**字符串集合编辑器** 对话框打开，你可以在其中向 **ComboBox** 控件添加项（图 VB-3.22）。
- 10. 在 **在集合中输入字符串（每行一个）** 列表框中输入月份名称（图 VB-3.22）。
- 11. 单击 **确定** 按钮关闭 **字符串集合编辑器** 对话框（图 VB-3.22）。

![](img/9862a98a1a2d3bb14334137965a1ec60_133_1.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_133_2.png)

图 VB-3.21

图 VB-3.22

- 12. *双击*窗体中的 **ComboBox** 控件，并将以下突出显示的一行代码*添加*到 **代码编辑器**：

```vb
Private Sub ComboBox1_SelectedIndexChanged(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles ComboBox1.SelectedIndexChanged
    TextBox1.Text = "You have selected: " & ComboBox1.SelectedItem
End Sub
```

在前面的代码片段中，ComboBox1.SelectedIndexChanged 是一个事件处理程序，用于处理 ComboBox 控件 ComboBox1 的 SelectedIndexChanged 事件。这意味着，当在运行时于 ComboBox1 中选择一个新项时，将执行 ComboBox1_SelectedIndexChanged 事件处理程序中编写的代码。前面代码片段中突出显示的一行代码使用一条消息设置 TextBox1 的 Text 属性，该消息指示已选择的项。

- 13. 按键盘上的 F5 键运行应用程序。输出出现（图 VB-3.23）。
- 14. 从组合框中选择一个项。在我们的示例中，我们选择了 February（图 VB-3.24）。
  文本框中会显示一条指示所选项的消息（图 VB-3.24）。

![](img/9862a98a1a2d3bb14334137965a1ec60_134_0.png)

了解 ComboBox 控件后，现在让我们了解 ListBox 控件。

## 使用 ListBox 控件

ListBox 控件用于显示项的列表，用户可从中选择一个或多个项。它类似于 ComboBox 控件；但是，与 ComboBox 控件不同，你可以从 ListBox 控件中选择多个项，并且不能在运行时为 ListBox 控件手动键入项。ListBox 控件中的每一项都通过其在列表中的位置（称为索引）来识别。ListBox 类包含在 System.Windows.Forms 命名空间中，提供 ListBox 控件的功能。表 3.13 列出了 ListBox 类的重要属性：

**表 3.13：ListBox 类的重要属性**

| **属性** | **描述** |
|---|---|
| ColumnWidth | 获取或设置多列列表框中列的宽度，以像素为单位 |
| DrawMode | 获取或设置列表框的绘制模式 |
| HorizontalScrollbar | 获取或设置一个值，指定是否在列表框中显示水平滚动条 |
| IntegralHeight | 获取或设置一个值，指示列表框是否应调整大小以避免显示部分项 |
| ItemHeight | 获取或设置列表框中项的高度，以像素为单位 |
| Items | 获取列表框中可用项的集合 |
| MultiColumn | 获取或设置一个值，指定列表框是否支持多列 |
| ScrollAlwaysVisible | 获取或设置一个值，指定垂直滚动条是否始终可见 |
| SelectedIndex | 获取或设置列表框中当前选定项的索引 |
| SelectedIndices | 获取一个集合，该集合包含列表框中所有选定项的索引 |
| SelectedItem | 获取或设置列表框中的选定项 |
| SelectedItems | 获取一个集合，该集合包含列表框的选定项 |
| SelectionMode | 获取选择项时使用的模式 |
| Sorted | 获取或设置一个值，指示列表框中的项是否按字母顺序排序 |

SelectionMode 属性允许你指定一次可以从列表框中选多少个项。可以使用此属性允许在列表框中进行多重选择。SelectionMode 属性可以设置为以下任意值：

- **None：** 表示无法从列表框中选择任何项
- **One：** 表示只能从列表框中选择一个项
- **MultiSimple：** 表示可以从列表框中选择多个项
- **MultiExtended：** 表示可以从列表框中选择多个项，并且用户可以使用 SHIFT、CTRL 和方向键进行选择

表 3.14 列出了 ListBox 类的重要方法：

**表 3.14：ListBox 类的重要方法**

| **方法** | **描述** |
|---|---|
| BeginUpdate | 在向控件添加项时通过防止闪烁来保持 ListBox 控件的性能。在调用 EndUpdate 方法之前，它不会绘制该控件。 |
| ClearSelected | 清除列表框中所有项的选择。 |
| EndUpdate | 在绘制被 BeginUpdate 方法暂停后，恢复绘制 ListBox 控件。 |
| FindString | 查找 ListBox 控件中第一个以指定字符串开头的项。 |
| FindStringExact | 查找 ListBox 控件中第一个与指定字符串完全匹配的项。 |
| GetItemHeight | 返回 ListBox 控件中特定项的高度，以像素为单位。 |
| GetSelected | 如果指定项已选定，则返回布尔值。 |
| SetSelected | 选择或清除列表框中指定的项。 |

执行以下步骤，在 Windows 窗体应用程序中使用 ListBox 控件：

- 1. *启动* **Visual Studio 2010**。
- 2. 从菜单栏中*选择* **文件→新建→项目**。新建项目对话框打开。
- 3. 从新建项目对话框左窗格的已安装的模板部分中*选择* **Visual Basic→Windows**。
- 4. 在中间窗格中*选择* **Windows 窗体应用程序** 模板以创建 Windows 窗体应用程序。
- 5. 在名称文本框中*输入*应用程序的名称 **ListBoxControl**（也可在 CD 上获得），并在位置组合框中输入应用程序的适当位置。
- 6. *单击* **确定** 按钮关闭新建项目对话框。ListBoxControl 应用程序已创建（图 VB-3.25）。
- 7. 从工具箱中将一个 Label 控件、一个 ListBox 控件和一个 TextBox 控件*拖放*到 Form1 窗体上。
- 8. 使用 **属性** 窗口将 Label 控件的 Text 属性*设置*为 **选择颜色：**。设置属性后，窗体如图 VB-3.25 所示：
