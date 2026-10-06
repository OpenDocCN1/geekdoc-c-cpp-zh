

# 处理鼠标和键盘事件

如果用户按下鼠标但在释放鼠标按钮之前将焦点切换到另一个控件或应用程序，则可能会发生 MouseDown 事件而没有相应的 Mouseup 事件。

| MouseEventArgs 属性 | 描述 |
| --- | --- |
| Button | 指定触发事件的鼠标按钮；值可以是 Left（左键）、Right（右键）、Middle（中键）或 none（无） |
| Clicks | 指定鼠标点击次数 |
| X | 事件在生成事件的控件上发生的 x 坐标 |
| Y | 事件在生成事件的控件上发生的 y 坐标 |

**表 13-3** MouseEventArgs 类的属性

MouseClicked 和 Click 是两个独立的事件。Click 事件接受一个 `EventArgs` 参数，而 MouseClick 接受一个 `MouseEventArgs` 参数。例如，如果你定义了 Click 事件，你将无法获得 `MouseEventArgs` 属性。

13-21 节包含一个 Form（表单），其中有一个名为 `locationLabel` 的 Label（标签），当用户继续点击鼠标时，该标签会发生变化。图显示了 Label 如何响应一系列点击而变化。最初，Label 是空的（即删除了默认的 Text 属性且未替换），在 Form1.cs 文件中了以下代码：

```cs
private void MouseClick(object sender, MouseEventArgs e)
{
    locationLabel.Text += "\nclicked at " + e.X + ", " + e.Y;
}
```

每当在 Form 上点击鼠标时，Label 都会追加新行，其中包含“Clicked at”以及点击在 Form 上发生的 x 和 y 坐标位置。图 13-21 显示了用户在点击了 Form 的左上、右上、右下和左下区域区域后的 Form 状态。

# 第 13 节 处理事件

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_654_0.png)

**图 13-21** 响应点击的表单

当程序人员从 IDE 中的事件列表中为 Form1 选择 `MouseClick()` 事件时，Designer.cs 文件中会生成以下代码。此代码实例化了 `MouseClick` 委托。

```cs
this.MouseClick += new System.Windows.Forms.EventHandler(this.Form1_MouseClicked);
```

# 处理键盘事件

键盘事件，也称为键事件（key events），在用户按下和释放键盘键时发生。与鼠标事件类似，每个键盘事件处理方法都必须有两个参数。根据事件的不同，用于创建事件处理程序的委托可能是 `EventHandler`，第二个参数的类型是 `KeyEventArgs`。

| 键盘事件 | 描述 | 事件参数 |
| --- | --- | --- |
| KeyDown | 在按下按键时发生 | KeyEventArgs |
| KeyUp | 在释放按键时发生 | KeyEventArgs |
| KeyPress | 在按下按键时发生 | KeyEventArgs |

**表 13-4** 键盘事件

表 13-5 描述了 `KeyEventArgs` 属性，表 13-6 描述了 KeyPress。一个重要的区别是 `KeyEventArgs` 对象包含了关于按下的修饰键（modifier keys）的数据。例如，如果你需要在应用程序中区分用户按了 Alt+A，你必须使用使用 `KeyEventArgs` 参数的键盘事件。

| 属性 | 描述 |
| --- | --- |
| Alt | 表示是否按下了 Alt 键 |
| Control | 表示是否按下了 Control (Ctrl) 键 |
| Shift | 表示是否按下了 Shift 键 |
| KeyCode | 返回按键的代码 |
| KeyData | 返回带有任何修饰键的键码 |
| KeyValue | 返回按键的数值表示（这被称为虚拟键） |

**表 13-5** KeyEventArgs 类的的一些属性

| 属性 | 描述 |
| --- | --- |
| KeyChar | 返回按键的 ASCII 字符 |

**表 13-6** KeyPress 类的的一个属性

例如，假设你想创建一个带有 Label 的 Form，并双击 Key 事件以生成一个名为 `Form1_KeyUp()` 的方法。假设你如如图 13-22 所示，将语句插入到 Form1.cs 文件的方法中。当用户运行程序并按下键盘键时，Label 将被填充有关该按键的信息。图 13-23 显示了该程序的三次执行结果。在第一次执行期间，用户输入了 a 而没有按下 Shift 键。

```cs
private void Form1_KeyUp(object sender, KeyEventArgs e)
{
    label1.Text += " Code " + e.KeyCode;
    label1.Text += "\n" + e.Alt;
    label1.Text += "\n" + e.Shift;
    label1.Text += "\n" + e.Control;
    label1.Text += "\nKey Data " + e.KeyData;
    label1.Text += "\nKey Value " + e.KeyValue;
}
```

**图 13-22** 程序中的 Form1_KeyUp()

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_656_0.png)

图 13-23 KeyDemo 程序的三次执行

在图 13-23 的第二次执行中，用户按住 Shift，按下 a，然后释放 Shift 键。这导致了两个独立的事件。第一个事件具有 `KeyCode` a 且 Shift 为 true，第二个事件也是如此。注意，在输入 a 后生成的值是相同的，但在输入 Shift 后的值是不同的。

在图 13-23 的第三次执行中，用户按下了 a，其代码为 D。

当你查看 KeyDemo 程序的 Form1.Designer.cs 时，你会看到定义委托的自动创建的事件语句：

```cs
this.KeyUp += new System.Windows.Forms.EventHandler(this.Form1_KeyUp);
```

> 两个真相和一个谎言：
1. 用于创建鼠标事件处理程序的委托是 `MouseEventHandler`。
2. 键盘事件（也称为键事件）在用户按下和释放键盘键时发生。
3. 与鼠标事件不同，每个键盘事件处理方法都必须无参数。

# 管理多个控件

当 Form 包含多个控件时，你通常希望其中一个拥有焦点。你可能还希望为同一个共享结果设置多个操作。例如，你可能希望无论用户点击按钮还是按下 Enter 键，都发生相同的操作，或者你可能希望多个按钮在被点击时产生相同的事件。

# 定义焦点

当用户在 Form 上遇到多个 GUI 控件时，通常有一个控件拥有焦点。例如，当按钮拥有焦点时，用户期望点击按钮或按下 Enter 键将引发一个事件。

`TabStop` 是控件的一个布尔属性，用于标识控件是否作为 Tab 键序列中的停止点（即焦点接收的地方）。按钮的默认值为 true，但 Label 的默认值为 false，因为 Label 并不被认为是制表键序列的一部分。`TabIndex` 是一个数值属性，指示当用户按下 Tab 键时控件接收焦点的顺序。程序人员通常使用较小的 Tab 值，从 0 开始。当控件的 `TabStop` 为 true 且该控件具有 Form 控件中最小的 `TabIndex` 时，它在 Form 初始化时接收焦点。

> 将两个或多个控件的 `TabIndex` 值设置为 0 不会导致错误。然而，只有一个控件会接收焦点。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_657_0.png)

图 13-24 显示了一个包含三个按钮和一个 Label 的 Form。每个按钮都关联了如下 Click 事件：

```cs
private void Button1_Click(object sender, EventArgs args)
{
    Label.Text = "Button1 selected";
}
```

在图 13-24 所示的程序中，每个按钮都按升序分配了 `TabIndex` 值。当应用程序启动时，第一个按钮（标记为 I）拥有焦点。无论用户点击该按钮还是按下 Enter，消息都会如左侧所示显示。在图的下一部分，用户按 Tab 键并按了 button2，它拥有焦点，Label 的 Text 属性发生了变化。或者，用户也可以点击 button2 来获得相同的结果。用户可以通过像往常一样点击或按下 Tab 直到所需的按钮拥有焦点然后按下 Enter 来选择其他任何按钮。

