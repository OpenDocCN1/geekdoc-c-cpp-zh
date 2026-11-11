
你可以编写在 Web 浏览器中运行的小程序。但是，如果你编写应用程序，通常希望弹出单独的对话框来向用户提供信息或从用户获取信息。

与大多数窗口系统一样，AWT 区分*模态*和*非模态*对话框。在处理完模态对话框之前，用户无法与应用程序的其他窗口交互。当你在继续执行之前需要从用户那里获取信息时，请使用模态对话框。例如，当用户想要读取文件时，可以让一个模态文件对话框弹出。用户必须先指定文件名，程序才能开始读取操作。只有当用户关闭模态对话框后，应用程序才能继续。

非模态对话框允许用户同时在对话框和应用程序的其余部分中输入信息。非模态对话框的一个例子是工具栏。工具栏可以根据需要一直停留在原地，用户可以根据需要与应用程序窗口和工具栏进行交互。

在本节中，我们将从最简单的对话框开始——只包含一条消息的模态对话框。Swing 提供了一个方便的 `JOptionPane` 类，让你无需编写任何特殊的对话框代码即可弹出简单的对话框。接下来，你将看到如何通过实现自己的对话框窗口来编写更复杂的对话框。最后，你将看到如何在应用程序和对话框之间来回传输数据。

我们将通过查看 Swing 的 `JFileChooser` 来结束对对话框的讨论。

## 11.7.1 选项对话框

Swing 提供了一组现成的简单对话框，足以向用户询问单个信息。`JOptionPane` 有四个静态方法来显示这些简单对话框：

- `showMessageDialog` — 显示消息并等待用户点击“确定”
- `showConfirmDialog` — 显示消息并获取确认（如“确定/取消”）
- `showOptionDialog` — 显示消息并从一组选项中获取用户选择
- `showInputDialog` — 显示消息并获取一行用户输入

图 11.30 显示了一个典型的对话框。如你所见，对话框包含以下组件：

- 一个图标
- 一条消息
- 一个或多个选项按钮

![](img/127bccebb2cfadea3f02579edaad63c3_734_0.png)

**图 11.30** 一个选项对话框

输入对话框有一个额外的用户输入组件。它可以是一个文本字段，用户可以在其中键入任意字符串；也可以是一个组合框，用户可以从其中选择一个项目。

这些对话框的确切布局以及标准消息类型图标的选择取决于可插拔的外观。

左侧的图标取决于五种消息类型之一：

```
ERROR_MESSAGE
INFORMATION_MESSAGE
WARNING_MESSAGE
QUESTION_MESSAGE
PLAIN_MESSAGE
```

`PLAIN_MESSAGE` 类型没有图标。每种对话框类型也有一个方法，允许你改为提供自己的图标。

对于每种对话框类型，你都可以指定一条消息。此消息可以是字符串、图标、用户界面组件或任何其他对象。下面是消息对象的显示方式：

| 消息对象类型 | 显示方式 |
|---|---|
| `String` | 绘制该字符串 |
| `Icon` | 显示该图标 |
| `Component` | 显示该组件 |
| `Object[]` | 显示数组中的所有对象，逐个堆叠 |
| 任何其他对象 | 应用 `toString` 并显示结果字符串 |

当然，提供消息字符串是迄今为止最常见的情况。提供 `Component` 则给了你极大的灵活性，因为你可以让 `paintComponent` 方法绘制任何你想要的内容。

底部的按钮取决于对话框类型和*选项类型*。调用 `showMessageDialog` 和 `showInputDialog` 时，你只能得到一组标准按钮（分别为“确定”和“确定/取消”）。调用 `showConfirmDialog` 时，你可以在四种选项类型中选择：

```
DEFAULT_OPTION
YES_NO_OPTION
YES_NO_CANCEL_OPTION
OK_CANCEL_OPTION
```

使用 `showOptionDialog` 可以指定任意一组选项。你为选项提供一个对象数组。每个数组元素的渲染方式如下：

| 选项数组元素类型 | 渲染方式 |
|---|---|
| `String` | 创建一个以该字符串为标签的按钮 |
| `Icon` | 创建一个以该图标为标签的按钮 |
| `Component` | 显示该组件 |
| 任何其他对象 | 应用 `toString` 并创建一个以结果字符串为标签的按钮 |

这些函数的返回值如下：

| 方法 | 返回值 |
|---|---|
| `showMessageDialog` | 无 |
| `showConfirmDialog` | 表示所选选项的整数 |
| `showOptionDialog` | 表示所选选项的整数 |
| `showInputDialog` | 用户提供或选择的字符串 |

`showConfirmDialog` 和 `showOptionDialog` 返回整数，指示用户选择了哪个按钮。对于选项对话框，这就是所选选项的索引；如果用户关闭了对话框而不是选择选项，则为 `CLOSED_OPTION` 值。对于确认对话框，返回值可以是以下之一：

```
OK_OPTION
CANCEL_OPTION
YES_OPTION
NO_OPTION
CLOSED_OPTION
```

这一系列选择听起来令人困惑，但实际上很简单。请按照以下步骤操作：

- 1. 选择对话框类型（消息、确认、选项或输入）。
- 2. 选择图标（错误、信息、警告、问题、无或自定义）。
- 3. 选择消息（字符串、图标、自定义组件或它们的堆叠）。
- 4. 对于确认对话框，选择选项类型（默认、是/否、是/否/取消或确定/取消）。
- 5. 对于选项对话框，选择选项（字符串、图标或自定义组件）和默认选项。
- 6. 对于输入对话框，在文本字段和组合框之间进行选择。
- 7. 在 `JOptionPane` API 中找到要调用的适当方法。

例如，假设你想显示图 11.30 中的对话框。该对话框显示一条消息并询问用户确认或取消。因此，它是一个确认对话框。图标是问号图标。消息是一个字符串。选项类型是 `OK_CANCEL_OPTION`。下面是你将进行的调用：

```
int selection = JOptionPane.showConfirmDialog(parent,
    "Message", "Title",
    JOptionPane.OK_CANCEL_OPTION,
    JOptionPane.QUESTION_MESSAGE);
if (selection == JOptionPane.OK_OPTION) ...
```

> **提示：**消息字符串可以包含换行符（`'\n'`）。这样的字符串会以多行显示。

### `javax.swing.JOptionPane` 1.2

- `static void showMessageDialog(Component parent, Object message, String title, int messageType, Icon icon)`
- `static void showMessageDialog(Component parent, Object message, String title, int messageType)`
- `static void showMessageDialog(Component parent, Object message)`
- `static void showInternalMessageDialog(Component parent, Object message, String title, int messageType, Icon icon)`
- `static void showInternalMessageDialog(Component parent, Object message, String title, int messageType)`
- `static void showInternalMessageDialog(Component parent, Object message)`

显示消息对话框或内部消息对话框。（内部对话框完全在其所有者框架内渲染。）父组件可以为 null。要显示在对话框上的消息可以是字符串、图标、组件或它们的数组。`messageType` 参数是 `ERROR_MESSAGE`、`INFORMATION_MESSAGE`、`WARNING_MESSAGE`、`QUESTION_MESSAGE`、`PLAIN_MESSAGE` 之一。

- `static int showConfirmDialog(Component parent, Object message, String title, int optionType, int messageType, Icon icon)`
- `static int showConfirmDialog(Component parent, Object message, String title, int optionType, int messageType)`
- `static int showConfirmDialog(Component parent, Object message, String title, int optionType)`
- `static int showConfirmDialog(Component parent, Object message)`
- `static int showInternalConfirmDialog(Component parent, Object message, String title, int optionType, int messageType, Icon icon)`
- `static int showInternalConfirmDialog(Component parent, Object message, String title, int optionType, int messageType)`
- `static int showInternalConfirmDialog(Component parent, Object message, String title, int optionType)`
- `static int showInternalConfirmDialog(Component parent, Object message)`

显示确认对话框或内部确认对话框。（内部对话框完全在其所有者框架内渲染。）返回用户选择的选项（`OK_OPTION`、`CANCEL_OPTION`、`YES_OPTION`、`NO_OPTION` 之一），如果用户关闭了对话框，则返回 `CLOSED_OPTION`。父组件可以为 null。要显示在对话框上的消息可以是字符串、图标、组件或它们的数组。`messageType` 参数是 `ERROR_MESSAGE`、`INFORMATION_MESSAGE`、`WARNING_MESSAGE`、`QUESTION_MESSAGE`、`PLAIN_MESSAGE` 之一，`optionType` 是 `DEFAULT_OPTION`、`YES_NO_OPTION`、`YES_NO_CANCEL_OPTION`、`OK_CANCEL_OPTION` 之一。

- `static int showOptionDialog(Component parent, Object message, String title, int optionType, int messageType, Icon icon, Object[] options, Object default)`
- `static int showInternalOptionDialog(Component parent, Object message, String title, int optionType, int messageType, Icon icon, Object[] options, Object default)`

显示选项对话框或内部选项对话框。（内部对话框完全在其所有者框架内渲染。）返回用户所选选项的索引；如果用户取消了对话框，则返回 `CLOSED_OPTION`。父组件可以为 null。要显示在对话框上的消息可以是字符串、图标、组件或它们的数组。`messageType` 参数是 `ERROR_MESSAGE`、`INFORMATION_MESSAGE`、`WARNING_MESSAGE`、`QUESTION_MESSAGE`、`PLAIN_MESSAGE` 之一，`optionType` 是 `DEFAULT_OPTION`、`YES_NO_OPTION`、`YES_NO_CANCEL_OPTION`、`OK_CANCEL_OPTION` 之一。`options` 参数是字符串、图标或组件的数组。
