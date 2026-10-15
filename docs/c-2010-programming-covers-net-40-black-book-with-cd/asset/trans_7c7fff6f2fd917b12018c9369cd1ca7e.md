

**图 8.47：显示具有修改后属性的控件**

- 5. 按 F5 键执行 TabOrder 应用程序。图 8.48 显示了 TabOrder 应用程序的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_328_0.png)

**图 8.48：显示 TabOrder 应用程序的输出**

现在，当你从键盘按下 Tab 键时，其他控件会按照属性窗口中 TabIndex 属性指定的顺序一个一个地高亮显示。你可以在 CD 上找到 TabOrder 应用程序的代码。

## 为控件指定访问字符

访问字符是菜单名称或控件标签中带下划线的字符。让我们执行以下步骤来学习如何为控件指定访问字符：

- 1. 创建一个名为 AccessCharacters 的 Windows 窗体应用程序。
- 2. 向 Form1 添加一个 Button 控件，button1。
- 3. 修改 Form1 的 Text 属性为 Access Characters Form。
- 4. 在 Form1 和 button1 的 Load 和 Click 事件中分别添加以下代码片段：

```
private void Form1_Load(object sender, EventArgs e)
{
    button1.Text = "&Print";
}
private void button1_Click(object sender, EventArgs e)
{
    MessageBox.Show("Alt+p is the shortcut key");
}
```

- 5. 按 F5 键运行并执行应用程序。结果，Form1 出现，如图 8.49 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_329_0.png)

**图 8.49：显示 AccessCharacters 应用程序的输出**

Form1 显示了标题为 Print 的按钮控件，其中 Print 的第一个字符 P 被下划线标出。现在，按下键盘上的 Alt+P 键组合以显示消息框，如图 8.50 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_329_1.png)

**图 8.50：使用访问字符显示消息框**

你也可以单击 Print 按钮来显示消息框，如图 8.50 所示。Alt+P 键组合是指定字符 P 的 Print 按钮的快捷键。以同样的方式，你可以为各种命令创建访问字符。你可以在 CD 上的 AccessCharacters 应用程序中找到为 Button 控件指定访问字符的代码。

## 移动和调整控件大小

在 C# 2010 中，你可以使用 SetBounds 方法来移动窗体和控件。Size 和 Location 属性用于设置窗体和控件的尺寸。这些属性分别由 Size 和 Point 类指定。这些类的对象是通过将值传递给其类构造函数中的 x 和 y 维度来创建的，Size(x_dimension, y_dimension) 和 Point(x_location, y_location)。你在 Size 和 Point 对象中设置的尺寸以像素为单位度量。在 Windows 窗体的坐标系统中，窗体的左上角是原点 (0, 0)，其中正 x 值向下增加，正 y 值向右增加。

让我们执行以下步骤来学习如何移动和调整控件大小：

- 1. 创建一个名为 MoveResizeControls 的 Windows 窗体应用程序。
- 2. 向 Form1 添加一个 Button 控件，button1。
- 3. 修改 Form1 的 Text 属性为 Move and Resize Form。
- 4. 在 button1 的 Click 事件中添加以下代码片段：

```
private void button1_Click(object sender, EventArgs e)
{
    Size = new Size(100, 100);
    Location = new Point(0, 0);
    button1.Size = new Size(100, 50);
    button1.Location = new Point(0, 0);
}
```

- 5. 按 F5 键运行并执行应用程序。结果，Form1 出现，如图 8.51 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_330_0.png)

**图 8.51：显示 MoveResizeControls 应用程序的输出**

现在，如果你单击 button1 按钮，按钮控件和窗体的大小和位置会发生变化，如图 8.52 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_330_1.png)

**图 8.52：显示窗体和按钮控件大小的更改**

你可以在 CD 上找到 MoveResizeControls 应用程序的源代码。

## 在运行时添加控件

你可以使用窗体的 Controls 集合的 Add 方法在应用程序运行时添加控件。

让我们创建一个名为 AddControl 的应用程序来学习如何在运行时添加控件。

执行以下步骤以在运行时添加控件：

- 1. 创建一个 Windows 窗体应用程序，AddControl。
- 2. 向 Form1 添加一个 Button 控件，button1。
- 3. 将 Form1 的 Text 属性设置为 Add Control Form，button1 设置为 Click Me to Add a Control，如图 8.53 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_330_2.png)

**图 8.53：设置控件的属性**

- 4. 在 button1 的 Click 事件中添加以下代码片段：

```
private void button1_Click(object sender, EventArgs e)
{
    TextBox NewTextBox = new TextBox();
    NewTextBox.Name = "MyTextBox";
    NewTextBox.Size = new Size(120, 20);
    NewTextBox.Location = new Point(100, 100);
    NewTextBox.Text = "Hello world of Coding";
    Controls.Add(NewTextBox);
}
```

- 5. 按 F5 键运行并执行应用程序。结果，Form1 出现，如图 8.54 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_331_0.png)

**图 8.54：显示 AddControl 应用程序的输出**

现在，当你单击 Click Me to Add a Control 按钮时，一个文本框会被添加到 Add Control Form 窗体中，如图 8.55 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_331_1.png)

**图 8.55：在运行时向窗体添加新控件**

你可以在 CD 上的 AddControl 应用程序中找到在运行时添加控件的代码。

## 处理 Windows 窗体和控件的常见事件

如你所知，C# 2010 是一种事件驱动语言。事件是调用函数或可能导致另一个事件发生的操作，该事件执行代码中指定的操作。单击按钮和在文本框中输入一些文本是事件的例子。你可以通过处理事件来控制应用程序的流程。主要有两种类型的事件：鼠标事件（通过鼠标提供输入而生成的事件）和键盘事件（通过键盘提供输入而生成的事件）。在本节中，你将学习如何处理这两种类型的事件。

### 处理鼠标事件

你可以使用以下鼠标事件来处理鼠标事件：

- MouseDown — 当鼠标指针位于控件上方且按下鼠标按钮时发生
- MouseEnter — 当鼠标指针进入控件时发生
- MouseHover — 当鼠标指针在控件上方来回移动时发生
- MouseLeave — 当鼠标指针离开控件时发生
- MouseMove — 当鼠标指针在控件上方移动时发生
- MouseUp — 当鼠标指针位于控件上方且释放鼠标按钮时发生
- MouseWheel — 当控件获得焦点时鼠标滚轮移动时发生

MouseEventArgs 对象的以下属性用于处理鼠标事件：

- Buttons — 指示按下的是哪个鼠标按钮。
- Clicks — 指示鼠标按钮被按下和释放的次数。
- Delta — 指示鼠标滚轮旋转的刻度数。刻度是鼠标滚轮旋转一个档位。
- X — 指示鼠标单击的 x 坐标。
- Y — 指示鼠标单击的 y 坐标。

Buttons 属性由 MouseButtons 枚举的值设置，如下所示：

- Left — 指示按下左鼠标按钮
- Middle — 指示按下中鼠标按钮
- None — 指示没有按下鼠标按钮
- Right — 指示按下右鼠标按钮
- XButton1 — 指示按下第一个 XButton
- XButton2 — 指示按下第二个 XButton

### 处理键盘事件

在 C# 中，以下事件可用于处理键盘事件：

- KeyDown — 当控件获得焦点时按下键时发生
- KeyPress — 当控件获得焦点时按下键时发生
- KeyUp — 当控件获得焦点时释放键时发生

为了处理 KeyDown 和 KeyUp 事件，事件处理程序接受类型为 KeyEventArgs 的参数。KeyEventArgs 类型包含以下属性：

- Alt — 持有指示 ALT 键是否被按下的值。
- Control — 持有指示 CTRL 键是否被按下的值。
- Handled — 持有或设置指示事件是否被处理的值。
- KeyCode — 持有 KeyDown 或 KeyUp 事件的键盘代码。
- KeyData — 持有 KeyDown 或 KeyUp 事件的键盘数据。
- KeyValue — 持有 KeyDown 或 KeyUp 事件的键盘值。
- Modifiers — 持有 KeyDown 或 KeyUp 事件的修饰符标志。这指示按下了哪些修饰键（Ctrl、Shift 和/或 Alt）。
- Shift — 持有指示 Shift 键是否被按下的值。

为了处理 KeyPress 事件，事件处理程序接受类型为 KeyPressEventArgs 的参数，其中包含以下属性：

- Handled — 获取或设置指示 KeyPress 事件是否被处理的值
- KeyChar — 持有按下的键对应的字符

让我们执行以下步骤来展示如何处理事件：

- 1. 创建一个名为 MouseandKeyboardEvents 的 Windows 窗体应用程序。
- 2. 向 Form1 添加两个 Label、两个 TextBox 和一个 Button 控件。
- 3. 将 Form1 的 Text 属性设置为 Add Numbers Form。
- 4. 修改添加的控件的属性，如表 8.10 所给：

| Control | Property | Value |
|---|---|---|
| label1 | Text | Enter first number |
| label2 | Text | Enter second number |
| button1 | Text | Add |

