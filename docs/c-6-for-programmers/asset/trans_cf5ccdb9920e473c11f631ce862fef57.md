

// calculate amount after each year and append to output
for (int yearCounter = 1; yearCounter <= year; ++yearCounter)
{
    decimal amount = principal *
        ((decimal) Math.Pow((1 + rate / 100), yearCounter));
    output += $"{yearCounter}\t{amount:C}\r\n";
}

displayTextBox.Text = output; // display result
}
}

![](img/3f5ef6be1748bb746e5f71a483bba4d0_465_0.png)

图 14.36 | 演示 NumericUpDown 控件。（第 2 部分，共 2 部分。）

对于名为 yearUpDown 的 NumericUpDown 控件，我们将 Minimum 属性设置为 1，将 Maximum 属性设置为 10。我们将 Increment 属性保留为其默认值 1。这些设置指定用户可以在 1 到 10 的范围内以 1 为增量输入年数。如果我们将 Increment 设置为 0.5，还可以输入诸如 1.5 或 2.5 之类的值。如果不修改 DecimalPlaces 属性（默认为 0），则 1.5 和 2.5 将分别显示为 2 和 3。我们将 NumericUpDown 的 ReadOnly 属性设置为 true，以指示用户无法在控件中键入数字来进行选择。因此，用户必须单击向上和向下箭头来修改控件中的值。默认情况下，ReadOnly 属性设置为 false。此应用的输出显示在带垂直滚动条的多行只读 TextBox 中，因此用户可以滚动查看整个输出。请注意，在 TextBox 中移动到下一行需要使用 \r\n（第 24 和 31 行）。

## 14.11 鼠标事件处理

本节说明如何处理鼠标事件，例如单击和移动，这些事件在用户通过鼠标与控件交互时生成。可以为任何派生自 System.Windows.Forms.Control 类的控件处理鼠标事件。对于大多数鼠标事件，有关事件的信息通过 MouseEventArgs 类的对象传递给事件处理方法，而用于创建鼠标事件处理程序的委托是 MouseEventHandler。这些事件的每个鼠标事件处理方法都需要一个 object 和一个 MouseEventArgs 对象作为参数。

MouseEventArgs 类包含与鼠标事件相关的信息，例如鼠标指针的 x 和 y 坐标、按下的鼠标按钮（Right、Left 或 Middle）以及鼠标单击次数。MouseEventArgs 对象的 x 和 y 坐标相对于生成该事件的控件——即点 (0,0) 表示发生鼠标事件的控件的左上角。图 14.37 描述了几种常见的鼠标事件和事件参数。

鼠标事件和事件参数

### 事件参数类型为 EventArgs 的鼠标事件
| 事件 | 描述 |
|---|---|
| MouseEnter | 鼠标光标进入控件的边界。 |
| MouseHover | 鼠标光标在控件的边界内悬停。 |
| MouseLeave | 鼠标光标离开控件的边界。 |

### 事件参数类型为 MouseEventArgs 的鼠标事件
| 事件 | 描述 |
|---|---|
| MouseDown | 鼠标光标位于控件边界内时按下鼠标按钮。 |
| MouseMove | 鼠标光标在控件边界内移动。 |
| MouseUp | 光标位于控件边界上时释放鼠标按钮。 |
| MouseWheel | 控件具有焦点时移动鼠标滚轮。 |

### MouseEventArgs 类的属性
| 属性 | 描述 |
|---|---|
| Button | 指定按下了哪个鼠标按钮（Left、Right、Middle 或 None）。 |
| Clicks | 鼠标按钮被单击的次数。 |
| X | 事件在控件内发生位置的 x 坐标。 |
| Y | 事件在控件内发生位置的 y 坐标。 |

图 14.37 | 鼠标事件和事件参数。

图 14.38 使用鼠标事件在 Form 上绘制。每当用户拖动鼠标（即按住鼠标按钮的同时移动鼠标）时，Form 上会在拖动操作期间每个鼠标事件发生的位置出现小圆圈。

```csharp
// Fig. 14.38: PainterForm.cs
// Using the mouse to draw on a Form.
using System;
using System.Drawing;
using System.Windows.Forms;

namespace Painter
{
    // creates a Form that's a drawing surface
    public partial class PainterForm : Form
    {
        bool ShouldPaint { get; set; } = false; // whether to paint
```

图 14.38 | 使用鼠标在 Form 上绘制。（第 1 部分，共 2 部分。）

```csharp
// default constructor
public PainterForm()
{
    InitializeComponent();
}

// should paint when mouse button is pressed down
private void PainterForm_MouseDown(object sender, MouseEventArgs e)
{
    // indicate that user is dragging the mouse
    ShouldPaint = true;
}

// stop painting when mouse button is released
private void PainterForm_MouseUp(object sender, MouseEventArgs e)
{
    // indicate that user released the mouse button
    ShouldPaint = false;
}

// draw circle whenever mouse moves with its button held down
private void PainterForm_MouseMove(object sender, MouseEventArgs e)
{
    if (ShouldPaint) // check if mouse button is being pressed
    {
        // draw a circle where the mouse pointer is present
        using (Graphics graphics = CreateGraphics())
        {
            graphics.FillEllipse(
                new SolidBrush(Color.BlueViolet), e.X, e.Y, 4, 4);
        }
    }
}
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_467_0.png)

图 14.38 | 使用鼠标在 Form 上绘制。（第 2 部分，共 2 部分。）

在第 12 行，程序声明了属性 ShouldPaint，它决定是否在 Form 上绘制。我们希望程序仅在鼠标按钮被按下（即按住）时绘制。因此，当用户单击或按住鼠标按钮时，系统会生成 MouseDown 事件，事件处理程序（第 21–25 行）将 ShouldPaint 设置为 true。当用户释放鼠标按钮时，系统会生成 MouseUp 事件，PainterForm_MouseUp 事件处理程序（第 28–32 行）将 ShouldPaint 设置为 false，程序停止绘制。与 MouseMove 事件在用户移动鼠标时连续发生不同，系统仅在鼠标按钮首次按下时生成 MouseDown 事件，并且仅在鼠标按钮释放时生成 MouseUp 事件。每当鼠标在控件上移动时，该控件的 MouseMove 事件就会发生。在 PainterForm_MouseMove 事件处理程序（第 35–46 行）内部，程序仅在 ShouldPaint 为 true（即按下了鼠标按钮）时绘制。在 using 语句中，第 40 行调用继承的 Form 方法 CreateGraphics 来创建一个 Graphics 对象，该对象允许程序在 Form 上绘制。Graphics 类提供了绘制各种形状的方法。例如，第 42–43 行使用方法 FillEllipse 绘制一个圆。在这种情况下，方法 FillEllipse 的第一个参数是 SolidBrush 类的对象，它指定填充形状的纯色。颜色作为参数提供给 SolidBrush 类的构造函数。Color 类型包含许多预定义的颜色常量——我们选择了 Color.BlueViolet。FillEllipse 在一个边界矩形中绘制椭圆，该矩形由其左上角的 x 和 y 坐标、宽度和高度指定——即该方法的最后四个参数。x 和 y 坐标表示鼠标事件的位置，可以从鼠标事件参数（e.x 和 e.y）中获取。要绘制一个圆，我们将边界矩形的宽度和高度设置为相等——在此示例中，两者均为 4 像素。Graphics、SolidBrush 和 Color 都属于 System.Drawing 命名空间。回想第 13 章，using 语句会自动对在关键字 using 后的括号中创建的对象调用 Dispose。这一点很重要，因为 Graphics 对象是一种有限资源。对 Graphics 对象调用 Dispose 可确保其资源返回系统以供重用。

## 14.12 键盘事件处理

键盘事件在按下和释放键盘按键时发生。可以为任何继承自 System.Windows.Forms.Control 的控件处理此类事件。有三个键盘事件——KeyPress、KeyUp 和 KeyDown。当用户按下字符键或空格键或退格键时，会发生 KeyPress 事件。特定按键可以通过事件处理程序的 KeyPressEventArgs 参数的 KeyChar 属性来确定。KeyPress 事件不指示按键事件发生时是否按下了修饰键（例如 Shift、Alt 和 Ctrl）。如果此信息很重要，可以使用 KeyUp 或 KeyDown 事件。这些事件各自的 KeyEventArgs 参数包含有关修饰键的信息。图 14.39 列出了重要的键盘事件信息。若干属性返回 Keys 枚举中的值，该枚举提供用于指定键盘上各种按键的常量。与 FontStyle 枚举（第 14.7 节）类似，Keys 枚举用一组位表示，因此该枚举的常量可以与按位运算符组合，以指示同时按下的多个按键。

