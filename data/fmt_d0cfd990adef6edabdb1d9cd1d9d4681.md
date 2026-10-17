
# 第 13 章 处理事件

## 处理控件事件

| KeyPress | 当控件获得焦点时按下按键时发生；事件在 KeyDown 之后发生 |

**表 13-1** 一些控件类的公共实例事件（续）

| 事件 | 说明 |
| --- | --- |
| Key | 当控件获得焦点时释放按键时发生 |
| Leave | 当离开控件时发生 |
| LocationChanged | 当 `Location` 属性值发生变化时发生 |
| LostFocus | 当控件失去焦点时发生 |
| MouseDown | 当鼠标指针悬停在控件上并按下鼠标键时发生 |
| MouseEnter | 当鼠标指针进入控件时发生 |
| MouseHover | 当鼠标指针悬停在控件上时发生 |
| MouseLeave | 当鼠标指针离开控件时发生 |
| MouseMove | 当鼠标指针在控件上移动时发生 |
| MouseUp | 当鼠标指针悬停在控件上并释放鼠标键时发生 |
| MouseWheel | 当控件获得焦点时滚动鼠标轮时发生 |
| Move | 当控件被移动时发生 |
| Resize | 当控件被调整大小时发生 |
| TextChanged | 当 `Text` 属性值发生变化时发生 |
| VisibleChanged | 当 `Visible` 属性值发生变化时发生 |

**表 13-1** 一些类的公共实例事件

你已经使用 IDE 创建了事件处理方法。例如，当你在 IDE 中双击控件时，你已经创建了默认事件。你为 `Button` 创建了 `Click()` 方法，为 `LinkLabel` 创建了 `LinkChanged()` 方法。一个 `Form` 可以包含任意数量的控件，这些控件可能关联有事件。此外，单个控件可以触发任意数量的事件。例如，除了创建 `Button` 的默认事件外，你可能希望在用户鼠标悬停在上时定义各种动作。表 13-1 仅列出了控件提供的许多事件中的少数几个；任何控件理论上都可以触发许多事件。

假设你想创建一个项目，该项目在鼠标悬停在 `Button` 上与点击按钮时具有不同的动作集。图 13-19 显示了在 IDE 中启动的项目。已经执行了以下操作：

- `Form` 调整大小为 225, 150。
- 将一个 `Button` 拖到 `Form` 上，将其 `Text` 设置为 "Click me"。
- 为 `Form` 添加了一个 `Label`，其 `Text` 设置为 "Hello"，并增大了字体。

![](img/b0a31988f44670d0728c4f372d8dab77_659_0.png)

图 13-19 IDE 中启动的 ButtonTwoEvents 项目

当你在 IDE 中双击 `Form` 上的 `Button` 时，你会生成一个 `Click` 方法的外壳，可以在其中输入命令来更改 `Label` 的文本和颜色，如下：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    label1.Text = "Button was clicked";
    label1.BackColor = Color.CornflowerBlue;
}
```

`CornflowerBlue` 是 C# 的预定义颜色之一。完整列表见表 12 中的表 12-5。

当在设计器 `Form` 上选中 `Button` 时，你可以点击右侧属性窗口中的事件（Events）图标。

当你在 IDE 中双击 `Form` 上的 `Button` 时，你会生成一个 `Click` 方法的外壳，可以在其中输入命令来更改 `Label` 的文本和颜色，如下：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    label1.Text = "Button was clicked";
    label1.BackColor = Color.CornflowerBlue;
}
```

`CornflowerBlue` 是 C# 的预定义颜色之一。完整列表见表 12 中的表 12-5。当在设计 `Form` 上选中 `Button` 时，你可以点击右侧属性窗口中的事件图标。

当你滚动属性窗口中的事件时，你可以看到各种选择。这个图标看起来像一个闪电。图 20 显示了属性窗口。

![](img/b0a31988f44670d0728c4f372d8dab77_660_0.png)

图 13-20 显示事件属性窗口

你可以在此方法中输入任何你语句。例如，你可能会编写：

```csharp
private void button1_MouseEnter(object sender, EventArgs e)
{
  label1.Text = "Go ahead";
  button1.BackColor = Color.Red;
}
```

当你运行带有这两个方法的程序时，会发生两个事件：

- 当鼠标进入按钮时（即鼠标悬停在按钮上时），`Label` 的文本更改为 "Go ahead"，按钮变为红色，如图 13-21 左侧所示。
- 在按钮被点击后，`Label` 的文本再次更改为 "Button was clicked"，`Label` 变为蓝色，如图 13-21 右侧所示。

![](img/b0a31988f44670d0728c4f372d8dab77_660_1.png)

图 13-21 鼠标进入按钮和点击按钮后的 ButtonEvents 程序

如果你执行 Windows Form 设计器生成的代码，你会发现以下两个语句：

```csharp
this.button1.Click += new System.EventHandler(this.button1_Click);
this.button1.MouseEnter += new System.EventHandler(this.button1_MouseEnter);
```

这些 `EventHandler` 语句与图 13-17 中的 `Student` 类中的语句。`Click` 和 `MouseEnter` 委托已设置为为适当处理此应用程序的事件。你可以使用 IDE 从属性列表中选择它们并编写你想要的动作语句来创建这些事件。IDE 通过正确输入所需的语句为你节省了时间。然而，通过手动创建一个包含事件的 GUI 程序，你更深入地理解了事件处理的工作原理。这种知识有助于你调试问题，并在必要时帮助你创建自己的事件和处理器。

## 处理鼠标和键盘事件

用户通过多种方式与 GUI 应用程序交互。最常见的策略无疑是使用鼠标或在键盘上打字。鼠标和键盘事件的相似之处在于，每个鼠标或按键事件处理方法都必须有两个参数：一个表示发送者的对象和一个包含事件信息的对象。

### 处理鼠标事件

鼠标事件包括用户使用鼠标时采取的所有操作，包括点击、指向和拖动。可以通过继承自 `EventArgs` 的 `MouseEventArgs` 类对象处理任何控件的鼠标事件。用于创建鼠标事件处理程序的委托是 `MouseEventHandler`。根据事件的不同，事件处理方法第二个参数的类型是 `EventArgs` 或 `MouseEventArgs`。表 13-2 描述了若干常见的鼠标事件，表 13-3 列出了 `MouseEventArgs` 类的一些属性。

| 鼠标事件 | 说明 | 事件参数类型 |
| --- | --- | --- |
| MouseClick | 用户在控件边界内点击鼠标时发生 | MouseEventArgs |
| MouseDoubleClick | 用户在控件边界内双击鼠标时发生 |  |
| MouseEnter | 鼠标光标进入控件边界时发生 | EventArgs |
| MouseLeave | 鼠标光标离开控件边界时发生 | EventArgs |
| MouseDown | 鼠标在控件边界内按下鼠标键时发生 | MouseEventArgs |
| MouseHover | 鼠标光标在控件边界内时发生 | MouseEventArgs |
| MouseMove | 鼠标在控件边界内移动时发生 | MouseEventArgs |
| MouseUp | 鼠标在控件边界内释放鼠标键时发生 | MouseEventArgs |

表 13-2 常见鼠标事件

如果用户按下鼠标，但在释放鼠标键之前将焦点切换到另一个控件或应用程序，则可能会发生 `MouseDown` 事件而没有发生相应的 `MouseUp` 事件。

| MouseEventArgs 属性 | 说明 |
|---|---|
| Button | 指定触发事件的哪个鼠标键；值可以是 Left、Right、Middle 或 none |
| Clicks | 指定鼠标被点击的次数 |
| X | 事件在生成事件的控件上发生的 x 坐标 |
| Y | 事件在生成事件的控件上发生的 y 坐标 |

表 13-3 MouseEventArgs 类的属性

`MouseClicked` 和 `Click` 是两个独立的事件。`Click` 事件接受一个 `EventArgs` 参数，但 `MouseClick` 接受一个 `MouseEventArgs` 参数。例如，如果你定义了一个 `Click` 事件，你就没有 `MouseEventArgs` 类的属性。

图 13-22 的每个部分包含一个名为 `clickLocationLabel` 的 Form，当用户继续点击它时，该标签会发生变化。该图显示了 Label 如何响应用户的一系列点击。起初，Label 是空的（即默认的 `Text` 属性已被删除且未被替换），但在 `Form.cs` 文件中添加了以下代码：

```csharp
private void Form1_MouseClicked(object sender, MouseEventArgs e)
{
    clickLocationLabel.Text += "\nClicked at " + e.X + ", " + e.Y;
}
```

每当在 Form 上点击鼠标时，Label 都会追加一个新行，其中包含“Clicked at ”以及在 Form 上发生点击的 x 和 y 坐标位置。

![](img/b0a31988f44670d0728c4f372d8dab77_664_0.png)

图 13-22 响应点击的 Form

当程序员从 IDE 中的事件列表中为 `Form1` 选择 `MouseClick()` 事件时，在 `Designer.cs` 文件中会生成以下代码。此代码实例化了 `MouseClick` 委托。

```csharp
this.MouseClick += new System.Windows.Forms.MouseEventHandler(this.Form1_MouseClicked);
```

### 处理键盘事件

键盘事件（也称为按键事件）发生在用户按下和释放键盘按键时。与鼠标事件的工作方式类似，每个键盘事件处理方法都必须有两个参数。根据事件的不同，用于创建键盘事件处理程序的委托是 `KeyEvent` 或 `KeyEventHandler`，第二个参数的类型是 `KeyEvent` 或 `KeyEventArgs`。

| 键盘事件 | 说明 | 事件参数类型 |
| --- | --- | --- |
| KeyDown | 按键首次被按下时发生 | KeyEventArgs |
| KeyUp | 按键被释放时发生 | KeyEventArgs |
| KeyPress | 按键被按下时发生 | KeyEventArgs |

表 13-4 键盘事件

表 13-5 描述了 `KeyEventArgs` 属性，表 13-6 描述了 `KeyEventArgs` 属性。一个重要的区别是 `KeyEventArgs` 对象包含了关于与另一个按键一起按下的辅助键或修饰键的信息。例如，如果你需要在应用程序中区分用户按下 A 和 Alt+A，那么你必须使用使用 `KeyEventArgs` 类型参数的键盘事件。

| 属性 | 说明 |
| --- | --- |
| Alt | 表示是否按下 Alt 键 |
| Control | 表示是否按下 Control (Ctrl) 键 |
| Shift | 表示是否按下 Shift 键 |
| KeyCode | 返回按键的代码 |
| KeyData | 返回按键码以及任何修饰符 |
| KeyValue | 返回按键的数字表示法（此数字称为 Windows 虚拟键码） |

**表 13-5** `KeyEventArgs` 类的一些属性

| 属性 | 说明 |
| --- | --- |
| KeyChar | 返回按键的 ASCII 字符 |

**表 13-6** `KeyPress` 的一个属性

例如，假设你创建一个带有 Label 的 Form，如图 13-22 所示。从 Form 的属性窗口中，双击 `KeyUp` 事件以生成一个名为 `Form1_KeyUp()` 的方法壳。随后你将语句插入 `Form1.cs`，如图 13-23 所示。当用户运行程序并释放键盘键时，Label 将填充有关按键的信息。

```csharp
private void Form1_KeyUp(object sender, KeyEventArgs e)
{
    label11.Text += " Key Code " + e.KeyCode;
    label11.Text += "\nAlt " + e.Alt;
    label11.Text += "\nShift " + e.Shift;
    label11.Text += "\nControl " + e.Control;
    label11.Text += "\nKeyData " + e.KeyData;
    label11.Text += "\nKeyValue " + e.KeyValue + "\n\n";
}
```

图 13-23 KeyUp() 方法

![](img/b0a31988f44670d0728c4f372d8dab77_666_0.png)

图 13-24 KeyDemo 程序的三次执行

在图 13-24 的第二次执行中，用户按住 Shift、*a*，然后释放了 Shift 键。这导致了两次 `KeyUp`。第一个带有 Shift 的 *KeyCode A*，第二个是 *KeyCode Shift*。注意输入 *a* 和 *A* 后生成的键值是相同的，但输入 Shift 后的值不同。

在图 13-24 的第三次执行中，用户按了数字 *1*，其代码为 D1。当你查看 KeyDemo 程序的 `Form1.Designer.cs` 文件时，你会看到以下生成的语句，它定义了组合委托：

```csharp
this.KeyUp += new System.Windows.Forms.KeyUpEventHandler(this.Form1_KeyUp);
```

## 二真一假

+ 1. 用于创建鼠标事件的委托是 `MouseEventHandler`。
2. 键盘事件（也称为按键事件）发生在用户按下和释放键盘按键时。
3. 与鼠标事件不同，每个键盘事件处理方法都必须无参数。

错误的陈述是 #3。与鼠标事件一样，每个键盘事件处理都是无的。

## 管理多个控件

当表单（Forms）包含多个控件时，你通常希望其中一个控件拥有焦点。你可能还希望多个操作具有单一的共同结果。例如，你可能希望在用户点击按钮或按下 Enter 键时发生相同的操作，或者你可能希望多个按钮在被点击时产生同一个事件。

### 定义焦点

当用户遇到表单上的 GUI 控件时，通常有一个控件具有焦点。例如，当按钮具有焦点时，用户期望点击该按钮或按下 Enter 键将触发一个事件。

`TabStop` 是控件的一个布尔属性，用于标识该控件是否将作为 Tab 键序列中的一个停靠点。按钮的 `TabStop` 默认值为 `true`，但标签（Label）的默认值为 `false`，因为标签通常被认为不是制表序列的一部分。`TabIndex` 是一个数值属性，表示当用户按下 Tab 键时，控件接收焦点的顺序。程序员通常使用使用较小的数字作为 `TabIndex` 的值，并从 0 开始。当一个控件的 `TabStop` 值为 `true` 且该控件具有表单所有控件中最低的 `TabIndex` 时，它会在表单初始化时获得焦点。

> 将两个或多个控件的 `TabIndex` 值设为 0 不会导致错误。然而，只有一个控件会接收焦点。

![](img/b0a31988f44670d0728c4f372d8dab77_667_0.png)

图 13-25 显示了一个包含三个按钮和一个标签的表单。每个按钮都关联了如下所示的 `Click()` 事件：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    buttonInfoLabel.Text = "Button 1 selected";
}
```

每个按钮都按升序顺序分配了 `TabIndex` 值。当应用程序启动时，第一个按钮（标记为 J）拥有焦点。当用户点击该按钮或按下 Enter 时，消息如图 13-25 左侧所示出现。在图的下部分，用户按了 Tab 和 Enter 选择了 button2，因此它拥有焦点，标签的属性也发生了变化。或者，用户也可以点击 button2 来达到相同的结果。用户可以通过像常一样点击其他任何一个按钮，或者一直按 Tab 直到所需的按钮获得焦点然后按下 Enter 来选择它们。

![](img/b0a31988f44670d0728c4f372d8dab77_668_0.png)

图 13-25 FocusDemo 程序的执行

### 使用单个处理程序处理多个事件
