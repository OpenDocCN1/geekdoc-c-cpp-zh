
| `yellowRadioButton` | `RadioButton` | Text: Yellow Checked: False |
| `redRadioButton` | `RadioButton` | Text: Red Checked: False |
| `whiteRadioButton` | `RadioButton` | Text: White Checked: False |
| `normalRadioButton` | `RadioButton` | Text: Back to Normal Checked: True |
| `exitButton` | `Button` |  |

### 步骤 3
...你将创建一个允许用户使用 `RadioButton` 控制选择颜色的应用程序。当用户选择颜色时，表单的背景颜色将立即变为该颜色。图 4-29 显示了应用程序的表单，并带有所有控件的名称。教程 4-5 将引导你完成这一过程。

注意，我们有三个独立的 `if` 语句。第 3 行的 `if` 语句确定 `pepperoniCheckBox` 控制是否被选中。如果是，第 5 行显示消息 `You selected Pepperoni.`。第 8 行的 `if` 语句确定 `cheeseCheckBox` 控制是否被选中。如果是，第 10 行显示消息 `You selected Cheese.`。第 13 行的 `if` 语句确定 `anchoviesCheckBox` 控制是否被选中。如果是，第 15 行显示消息 `You selected Anchovies.`。

# CheckedChanged 事件

每当 `RadioButton` 或 `CheckBox` 的 `Checked` 属性发生变化时，该控件就会触发一个 `CheckedChanged` 事件。如果你想在用户选择（或取消选择）`RadioButton` 或 `CheckBox` 控制时立即执行某些操作，可以为该控件创建一个 `CheckedChanged` 事件处理器，并在该事件处理器中编写所需的代码。

要为 `RadioButton` 或 `CheckBox` 创建 `CheckedChanged` 事件处理器，只需在设计器中双击该控件即可。代码编辑器中将创建一个空的 `CheckedChanged` 事件处理器。然后，你就可以在事件处理器内部编写代码了。教程 4-5 将引导你完成这一过程。

# 教程 4-5：创建颜色主题应用程序

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_576_0.png)

在本教程中，你将创建一个允许用户使用 `RadioButton` 控制选择颜色的应用程序。当用户选择颜色时，表单的背景颜色将立即变为该颜色。图 4-29 显示了应用程序的表单，并带有所有控件的名称。

图 4-29 Color Theme 表单

![](img/2e5a40b20b6ba3c5f5ed1f5ae1fb1a28_577_0.png)

### 步骤 1
启动 Visual Studio 并创建一个名为 *Color Theme.* 的新 Windows Forms 项目。

### 步骤 2
如图 4-29 所示设置应用程序表单。注意表单的 `Text` 属性已设置为 *Color Theme*。图中显示了控件的名称。当你将每个控件放置在表单上时，请参考表 4-8 进行相关的属性设置。

#### 表 4-8 控件属性设置

| 控件名称 | 控件类型 | 属性设置 |
| --- | --- | --- |
| `colorGroupBox` | `GroupBox` | Text: Select a Background Color |
| `yellowRadioButton` | `RadioButton` | Text: Yellow Checked: False |
| `redRadioButton` | `RadioButton` | Text: Red Checked: False |
| `whiteRadioButton` | `RadioButton` | Text: White Checked: False |
| `normalRadioButton` | `RadioButton` | Text: Back to Normal Checked: True |
| `exitButton` | `Button` |  |
