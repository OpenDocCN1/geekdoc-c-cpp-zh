
在我们离开绘制简单对象的主题之前，本节以一个简单示例作为结尾，演示了使用画刷可以实现的视觉效果类型。该示例名为 ScrollMoreShapes，本质上是 ScrollShapes 的修订版本。除了矩形和椭圆之外，你还要添加一条粗线，并用各种自定义画刷填充形状。你已经学习了绘制原理，因此代码不言自明。首先，由于使用了新的画刷，你需要指明正在使用 System.Drawing.Drawing2D 命名空间：

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Drawing.Drawing2D;
using System.Text;
using System.Windows.Forms;
```

接下来是 Form1 类中的一些额外字段，其中包含要绘制形状的位置详细信息，以及你将使用的各种画笔和画刷：

```
private Rectangle rectangleBounds = new Rectangle(new Point(0,0),
    new Size(200,200));
private Rectangle ellipseBounds = new Rectangle(new Point(50,200),
    new Size(200,150));
private readonly Pen bluePen = new Pen(Color.Blue, 3);
private readonly Pen redPen = new Pen(Color.Red, 2);
private readonly Brush solidAzureBrush = Brushes.Azure;
private readonly Brush solidYellowBrush = new SolidBrush(Color.Yellow);
private static readonly Brush brickBrush = new
    HatchBrush(HatchStyle.DiagonalBrick, Color.DarkGoldenrod, Color.Cyan);
private readonly Pen brickWidePen = new Pen(brickBrush, 10);
```

brickBrush 字段被声明为静态，以便你可以使用其值来初始化 brickWidePen 字段。C# 不允许你使用一个实例字段来初始化另一个实例字段，因为它没有定义哪个字段会先被初始化。不过，将该字段声明为静态可以解决此问题。由于只会实例化一个 Form1 类实例，因此字段是静态的还是实例字段无关紧要。

以下是 OnPaint() 重写：

```
protected override void OnPaint( PaintEventArgs e )
{
    base.OnPaint(e);
    Graphics dc = e.Graphics;
    Point scrollOffset = AutoScrollPosition;
    dc.TranslateTransform(scrollOffset.X, scrollOffset.Y);
    if (e.ClipRectangle.Top+scrollOffset.X < 350 ||
        e.ClipRectangle.Left+scrollOffset.Y < 250)
    {
        dc.DrawRectangle(bluePen, rectangleBounds);
        dc.FillRectangle(solidYellowBrush, rectangleBounds);
        dc.DrawEllipse(redPen, ellipseBounds);
        dc.FillEllipse(solidAzureBrush, ellipseBounds);
        dc.DrawLine(brickWidePen, rectangleBounds.Location,
            ellipseBounds.Location+ellipseBounds.Size);
    }
}
```

代码下载 ScrollMoreShapes.sln

与其他示例一样，DisplayPicture 项目是标准的 C# Visual Studio 2010 生成的 Windows 应用程序。你向 Form1 类中添加以下字段：

```
readonly Image piccy;
private readonly Point[] piccyBounds;
```

然后在 Form1() 构造函数中加载文件：

```
public Form1()
{
    InitializeComponent();
    piccy =
        Image.FromFile(@"C:\ProCSharp\GdiPlus\Images\London.jpg");
    AutoScrollMinSize = piccy.Size;
    piccyBounds = new Point[3];
    piccyBounds[0] = new Point(0,0);    // top left
    piccyBounds[1] = new Point(piccy.Width,0);    // top right
    piccyBounds[2] = new Point(0,piccy.Height);    // bottom left
}
```

代码下载 DisplayPicture.sln

注意，图像的像素大小通过其 Size 属性获取，你使用该属性来设置文档区域。你还设置了 piccyBounds 数组，用于标识图像在屏幕上的位置。此处你选择了三个角的坐标来按实际大小和形状绘制图像，但如果你想要调整图像大小、拉伸甚至将其剪切为非矩形平行四边形，只需更改 piccyBounds 数组中的 Point 值即可。

图像在 OnPaint() 重写中显示：

```
protected override void OnPaint(PaintEventArgs e)
{
    base.OnPaint(e);
    Graphics dc = e.Graphics;
    dc.ScaleTransform(1.0f, 1.0f);
    dc.TranslateTransform(AutoScrollPosition.X, AutoScrollPosition.Y);
    dc.DrawImage(piccy, piccyBounds);
}
```

代码下载 DisplayPicture.sln

最后，注意对 IDE 生成的 Form1.Dispose() 方法所做的修改：

```
protected override void Dispose(bool disposing)
{
    piccy.Dispose();
    if (disposing && (components != null))
    {
        components.Dispose();
    }
    base.Dispose(disposing);
}
```

代码下载 DisplayPicture.sln

不再需要图像时尽快将其释放很重要，因为图像在使用时通常会占用大量内存。调用 Image.Dispose() 后，Image 实例不再引用任何实际图像，因此无法再显示（除非加载新图像）。图 48-14 显示了运行此代码的结果。

![](img/d7d2ffa0a76feaab821930e95daace93_1563_0.png)

图 48-14

## 操作图像时的问题

尽管显示图像非常简单，但了解一下幕后发生的事情仍然是值得的。

关于图像，最重要的一点是它们总是矩形的。这不仅仅是为了方便，而是因为底层技术。所有现代显卡都内置了硬件，可以高效地将像素块从内存的一个区域复制到另一个区域，前提是该像素块表示矩形区域。这种硬件加速操作几乎可以作为一个单一操作发生，因此速度极快。事实上，它是现代高性能图形的关键。此操作称为位图块传输（或 BitBlt）。Graphics.DrawImageUnscaled() 内部使用 BitBlt，这就是为什么你可以看到包含多达一百万个像素的巨大图像几乎立即出现。如果计算机必须逐像素将图像复制到屏幕，你会看到图像在长达数秒的时间内逐渐绘制完成。

BitBlt 非常高效，因此几乎所有图像的绘制和操作都使用它们。甚至一些图像编辑也会通过在表示内存区域的 DC 之间使用 BitBlt 来操作图像部分来完成。在 GDI 时代，Windows 32 API 函数 BitBlt() 可以说是图像操作中最重要且使用最广泛的函数，不过在 GDI+ 中，BitBlt 操作在很大程度上被 GDI+ 对象模型隐藏了。

无法对非矩形的图像区域进行 BitBlt，尽管可以轻松模拟类似效果。一种方法是为 BitBlt 的目的将某种颜色标记为透明，这样源图像中该颜色的区域就不会覆盖目标设备中对应像素的现有颜色。还可以指定在 BitBlt 过程中，结果图像的每个像素将由源图像中该像素的颜色与目标设备中该像素的颜色进行某种逻辑运算（例如按位 AND）形成，然后才进行 BitBlt。此类操作受硬件加速支持，可用于产生各种微妙的效果。请注意，Graphics 对象还实现了另一个方法 DrawImage()。它与 DrawImageUnscaled() 类似，但提供了大量重载，允许你指定在绘制过程中使用更复杂的 BitBlt 形式。DrawImage() 还允许你（使用 BitBlt）仅绘制图像的指定部分，或对其进行某些其他操作，例如在绘制时缩放（扩大或缩小其大小）。

## 绘制文本

我们选择在本章较晚的时候介绍显示文本这个非常重要的主题，因为一般来说，在屏幕上绘制文本比绘制简单图形要复杂得多。虽然当你不关心外观时，显示一两行文本极其容易（只需调用一次 Graphics.DrawString() 方法），但如果你要显示包含大量文本的文档，就会很快发现事情变得复杂得多。原因有二：

- 如果你关心外观是否恰到好处，那么你必须了解字体。形状绘制需要画刷和画笔作为辅助对象，而文本绘制过程需要字体作为辅助对象。此外，理解字体并非易事。
- 文本需要在窗口中非常仔细地布局。用户通常期望单词自然连贯，并在之间用清晰的空格对齐。这比你可能想象的要难。首先，你通常无法提前知道一个单词在屏幕上会占据多少空间。这必须计算（使用 Graphics.MeasureString() 方法）。此外，一个单词在屏幕上占据的空间会影响文档中后续每个单词的放置位置。如果你的应用程序需要进行任何换行，那么在决定在哪里放置换行符之前，需要仔细评估单词大小。下次运行 Microsoft Word 时，请仔细观察 Word 在你工作时不断重新定位文本的方式；那里正在进行大量复杂的处理。你所处理的任何 GDI+ 应用程序很可能都不会像 Word 那样复杂。但是，如果你需要显示任何文本，许多相同的考虑因素也适用。

简而言之，高质量的文本处理很难做到完美。然而，假设你知道字体和想要放置的位置，那么将一行文本放到屏幕上实际上非常简单。因此，下一节将提供一个快速示例，展示如何显示一些文本，然后简要回顾字体和字体族的原则，以及一个更真实（且更复杂）的文本处理示例 CapsEditor。

### 简单文本示例

此示例 DisplayText 是你通常的 Windows Forms 工作。这次你重写 OnPaint() 并添加成员字段，如下所示：

```
private readonly Brush blackBrush = Brushes.Black;
private readonly Brush blueBrush = Brushes.Blue;
private readonly Font haettenschweilerFont = new Font("Haettenschweiler", 12);
private readonly Font boldTimesFont = new Font("Times New Roman", 10, FontStyle.Bold);
private readonly Font italicCourierFont = new Font("Courier", 11, FontStyle.Italic | FontStyle.Underline);

protected override void OnPaint(PaintEventArgs e)
{
    base.OnPaint(e);
    Graphics dc = e.Graphics;
    dc.DrawString("This is a groovy string", haettenschweilerFont, blackBrush, new Point(10, 10));
    dc.DrawString("This is a groovy string " + "with some very long text that will never fit in the box", boldTimesFont, blueBrush, new Rectangle(new Point(10, 40), new Size(100, 40)));
    dc.DrawString("This is a groovy string", italicCourierFont, blackBrush, new Point(10, 100));
}
```
