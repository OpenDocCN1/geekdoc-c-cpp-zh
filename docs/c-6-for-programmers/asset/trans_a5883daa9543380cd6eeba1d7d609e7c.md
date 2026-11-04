
### 键盘事件和事件参数

**具有 KeyEventArgs 类型事件参数的键事件**

- **KeyDown**：在最初按下某个键时生成。
- **KeyUp**：在释放某个键时生成。

**具有 KeyPressEventArgs 类型事件参数的键事件**

- **KeyPress**：在按下某个键时生成。在 KeyDown 之后、KeyUp 之前引发。

**KeyPressEventArgs 类的属性**

- **KeyChar**：返回所按键的 ASCII 字符。

**KeyEventArgs 类的属性**

- **Alt**：指示是否按下了 Alt 键。
- **Control**：指示是否按下了 Ctrl 键。
- **Shift**：指示是否按下了 Shift 键。
- **KeyCode**：以 Keys 枚举中的值形式返回该键的键代码。这不包括修饰键信息。它用于测试特定键。
- **KeyData**：返回键的键代码与修饰键信息组合而成的 Keys 值。此属性包含有关所按键的所有信息。
- **KeyValue**：以 int 形式返回键代码，而不是作为 Keys 枚举中的值。此属性用于获取所按键的数值表示。该 int 值称为 Windows 虚拟键代码。
- **Modifiers**：返回一个 Keys 值，指示任何按下的修饰键（Alt、Ctrl 和 Shift）。此属性仅用于确定修饰键信息。

**图 14.39** | 键盘事件和事件参数。

图 14.40 演示了如何使用键事件处理程序显示用户按下的键。该程序是一个包含两个 Label 的 Form，其中一个 Label 显示按下的键，另一个显示修饰键信息。

```csharp
1 // Fig. 14.40: KeyDemo.cs
2 // Displaying information about the key the user pressed.
3 using System;
4 using System.Windows.Forms;
5
6 namespace KeyDemo
7 {
8     // Form to display key information when key is pressed
9     public partial class KeyDemo : Form
10     {
11         // default constructor
12         public KeyDemo()
13         {
14             InitializeComponent();
15         }
```

**图 14.40** | 显示用户所按键的信息。（第 1 部分，共 2 部分。）

```csharp
// display the character pressed using KeyChar
private void KeyDemo_KeyPress(object sender, KeyPressEventArgs e)
{
    charLabel.Text = $"Key pressed: {e.KeyChar}";
}

// display modifier keys, key code, key data and key value
private void KeyDemo_KeyDown(object sender, KeyEventArgs e)
{
    keyInfoLabel.Text =
        $"Alt: {(e.Alt ? "Yes" : "No")}\n" +
        $"Shift: {(e.Shift ? "Yes" : "No")}\n" +
        $"Ctrl: {(e.Control ? "Yes" : "No")}\n" +
        $"KeyCode: {e.KeyCode}\n" +
        $"KeyData: {e.KeyData}\n" +
        $"KeyValue: {e.KeyValue}";
}

// clear labels when key released
private void KeyDemo_KeyUp(object sender, KeyEventArgs e)
{
    charLabel.Text = "";
    keyInfoLabel.Text = "";
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_470_0.png)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_470_1.png)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_470_2.png)

![](img/3f5ef6be1748bb746e5f71a483bba4d0_470_3.png)

**图 14.40** | 显示用户所按键的信息。（第 2 部分，共 2 部分。）

控件 charLabel 显示所按键的字符值，而 keyInfoLabel 显示与所按键相关的信息。由于 KeyDown 和 KeyPress 事件传递不同的信息，Form（KeyDemo）同时处理这两个事件。

KeyPress 事件处理程序（第 18–21 行）访问 KeyPressEventArgs 对象的 KeyChar 属性。这会以 char 形式返回所按键，然后我们在 charLabel 中显示它（第 20 行）。如果按下的键不是 ASCII 字符，则不会发生 KeyPress 事件，并且 charLabel 不会显示任何文本。ASCII 是字母、数字、标点符号和其他字符的常见编码格式。它不支持功能键（如 F1）或修饰键（Alt、Ctrl 和 Shift）等按键。

KeyDown 事件处理程序（第 24–33 行）显示其 KeyEventArgs 对象中的信息。该处理程序使用 Alt、Shift 和 Control 属性测试 Alt、Shift 和 Ctrl 键，这些属性各自返回一个 bool——如果按下了相应键则为 true，否则为 false。然后，该处理程序显示 KeyCode、KeyData 和 KeyValue 属性。

KeyCode 属性返回一个 Keys 枚举值（第 30 行）。KeyCode 属性返回所按键，但不提供任何关于修饰键的信息。因此，大写和小写的“a”都表示为 A 键。

KeyData 属性（第 31 行）也返回一个 Keys 枚举值，但还包含修饰键数据。因此，如果输入“A”，KeyData 会显示 A 和 Shift 都被按下。最后，KeyValue（第 32 行）返回一个表示所按键的 int。这个 int 就是键代码。键代码在测试非 ASCII 键（如 F12）时很有用。

KeyUp 事件处理程序（第 36–40 行）在释放键时清除两个 Label。从输出中可以看到，非 ASCII 键不会显示在 charLabel 中，因为不会生成 KeyPress 事件。例如，按 F7 键时 charLabel 不显示任何文本，如图 14.40(b) 所示。但是，KeyDown 事件仍会生成，并且 keyInfoLabel 显示有关所按键的信息。通过将所按键的 KeyCode 与 Keys 枚举中的值进行比较，可以使用 Keys 枚举测试特定键。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_471_0.png)

> **软件工程观察 14.2**
> 
> 要使控件在按下特定键（例如 Enter）时做出反应，请处理键事件并测试所按键。要使在 Form 上按下 Enter 键时单击 Button，请设置 Form 的 AcceptButton 属性。

默认情况下，键盘事件由当前具有焦点的控件处理。有时适合让 Form 处理这些事件。这可以通过将 Form 的 KeyPreview 属性设置为 true 来实现，这会使 Form 在键盘事件传递给另一个控件之前先接收它们——例如，即使 Form 内的某个控件（而不是 Form 本身）具有焦点，按键也会引发 Form 的 KeyPress。

### 14.13 小结

本章介绍了几种常见的 GUI 控件。我们详细讨论了事件处理，并展示了如何创建事件处理程序。我们展示了如何使用委托将事件处理程序连接到特定控件的事件。你学习了如何使用控件属性和 Visual Studio 来指定 GUI 的布局。然后我们演示了几个控件，从 Label、Button 和 TextBox 开始。你学习了如何使用 GroupBox 和 Panel 组织其他控件。然后我们演示了 CheckBox 和 RadioButton，它们是允许用户在多个选项中进行选择的状态按钮。我们在 PictureBox 控件中显示图像，使用 ToolTip 组件为 GUI 显示有帮助的文本，并使用 NumericUpDown 控件为用户指定数值输入范围。然后我们演示了如何处理鼠标和键盘事件。下一章将介绍更多 GUI 控件。你将学习如何向 GUI 添加菜单，以及创建显示多个 Form 的 Windows 窗体应用。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_473_0.png)

## 15 使用 Windows 窗体的图形用户界面：第 2 部分

### 目标

本章中，你将：

- 创建菜单、选项卡式窗口和多文档界面（MDI）程序。
- 使用 ListView 和 TreeView 控件显示信息。
- 使用 LinkLabel 控件创建超链接。
- 在 ListBox、CheckedListBox 和 ComboBox 控件中显示信息列表。
- 使用 MonthCalendar 控件输入日期。
- 使用 DateTimePicker 控件输入日期和时间数据。
- 创建自定义控件。
- 使用可视化继承在现有 GUI 基础上构建。

![](img/3f5ef6be1748bb746e5f71a483bba4d0_474_0.png)

### 15.1 简介

这里我们继续介绍 Windows 窗体。我们从菜单开始，菜单向用户呈现按逻辑组织的命令（或选项）。我们展示如何在 Windows 窗体设计器中创建菜单。我们讨论如何使用 MonthCalendar 和 DateTimePicker 控件输入和显示日期与时间。我们还将介绍 LinkLabel，它只需单击鼠标即可超链接到当前计算机上的文件或网页。

我们演示如何通过 ListBox 和 ListView 操作值列表，以及如何在 CheckedListBox 中组合多个复选框。我们还使用 ComboBox 创建下拉列表，并使用 TreeView 控件以层次结构显示数据。你将学习另外两个重要的 GUI 元素——选项卡控件和多文档界面（MDI）窗口。这些组件使你能够创建具有复杂 GUI 的实际程序。你将使用可视化继承在现有 GUI 基础上构建。

Visual Studio 提供了许多 GUI 组件，本章（以及上一章）讨论了其中几个。你还可以设计自定义控件并将其添加到 ToolBox，正如本章最后一个示例所演示的那样。这里介绍的技术为创建更复杂的 GUI 和自定义控件奠定了基础。

### 15.2 菜单

菜单为 Windows 窗体应用提供相关命令组。尽管这些命令取决于程序，但有些命令——例如“打开”和“保存”——在许多应用中都很常见。菜单是 GUI 不可或缺的一部分，因为它们组织命令而不会“弄乱”GUI。

在图 15.1 中，Visual Studio 中一个展开的菜单列出了各种命令（称为菜单项），以及子菜单（菜单中的菜单）。顶级菜单出现在图的左侧部分，而任何子菜单或菜单项显示在右侧。包含某个菜单项的菜单称为该菜单项的父菜单。包含子菜单的菜单项被视为该子菜单的父项。

菜单可以具有 Alt 键快捷方式（也称为访问快捷方式、键盘快捷方式或热键），通过按 Alt 和下划线字母来访问——例如，Alt + F 通常会展开“文件”菜单。菜单项也可以有快捷键（Ctrl、Shift、Alt、F1、F2、字母键等的组合）。某些菜单项显示复选标记，通常表示可以同时选择菜单上的多个选项。
