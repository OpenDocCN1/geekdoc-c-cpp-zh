
绘制和填充形状。DrawEllipse 和 FillEllipse 方法用于创建自定义按钮。例如，FillEllipse 绘制并填充按钮，而当 HasOutline 为 True 时，DrawEllipse 绘制按钮的轮廓。

绘制方法使用 Pen 对象来绘制表示形状的边界。形状表示为由边界矩形包围的区域。FillEllipse 与 DrawEllipse 工作方式几乎相同；然而，与 Pen 不同，你必须向 FillEllipse 传递一个 Brush，因为填充方法会绘制区域内部。

存在两种类型的填充和绘制方法。一个版本接受定义矩形区域的整数参数，另一个版本接受表示矩形区域的浮点数。形状绘制方法提供浮点版本的好处在于，你可以执行返回浮点数的数学运算，而无需将这些数字截断为整数。

调用的具体绘制或填充方法取决于参数的类型。这里多态性有所帮助。每个绘制和填充方法都有多个重载版本，编译器会根据参数类型决定调用哪个具体方法。

除了通过指定四个点来定义矩形区域外，你还可以用一对 Point 结构或一个 Rectangle 结构来表示矩形区域。如果使用点或矩形，则当底层值为整数时应使用 Point 或 Rectangle，而当底层值为浮点值时应使用 PointF 和 RectangleF。关于 Point 和 Rectangle 结构用法的一些示例可以在 RoundButton.cs 文件中找到。

## 将变换应用于图形对象

GDI+ 使用世界、页面和设备坐标。当你调用 Graphics 方法时，你表达的位置处于世界坐标空间中。GDI+ 通过两次变换将世界坐标参数转换，先从世界坐标到页面坐标，然后到设备坐标。GDI+ 在后台处理这些变换。作为软件工程师，我们的优势在于可以更改原点，将 PageUnit 从默认的像素更改为其他度量单位，并执行诸如缩放图片之类的任务。

这些功能被用来创建增强的可视化效果，即当客户端点击 RoundButton 项时按钮位置发生变化。如果按钮在客户端点击时外观没有哪怕轻微的变化，那么这种错觉就会丧失。RoundButton 类中的随附段落会在绘制按钮图形之前将缩放的 Matrix 变换应用于 Graphics 对象，从而产生按钮在客户端点击时略微移动的错觉。

当客户端点击 RoundButton 控件的一个实例时，OnMouseDown 方法会被触发。从列表中我们可以确定基类的 OnMouseDown 方法被调用。这将使客户端能够捕获该事件；也就是说，我们没有干扰默认行为。此时，down 字段被设为 True，并且控件被使无效。调用 Invalidate 方法会强制进行重绘。现在，重载的 OnPaint 方法被调用。再次，我们执行 base.OnPaint 行为，然后执行自定义行为。

自定义 Paint 行为绘制按钮，随后绘制图形。如果 down 为 True——在我们的情况下是这样——则会调用 DrawDownGraphic 方法。（这就是变换发挥作用的地方。）DrawDownGraphic 创建一个 Matrix 对象。Matrix.Scale 被调用以缩放 Matrix 对象，并且该 Matrix 对象被应用于 graphics.Transform 属性。最终产品是一个图形，看起来像按钮被按下时略微移动了。

当你理解了其机制，你会发现它们非常清晰。创造力在于找到正确的画笔、色调和阴影的组合，使错觉尽可能真实。你应该通过运行 VideoKiosk.sln 测试应用程序自行判断按钮看起来有多真实。

创造力越好，应用程序就越出色。

## 利用 GraphicsPath 对象创建形状表单

GraphicsPath 类定义在 System.Drawing.Drawing2D 命名空间中。GraphicsPath 对象用于表示一系列连接的线条和曲线。你听说过形状化的 Windows 窗体。事实上，GraphicsPath 对象就是创建形状化 Windows 窗体的方式。

GraphicsPath 对象允许你通过向 GraphicsPath 对象添加线条和曲线，然后使用该对象定义窗体的剪切区域来创建形状窗体。PlayControl 具有圆角边缘，显示出平滑的形状。PlayControl 中的随附摘录显示了通过圆角化角落来微妙地塑造 PlayControl 的代码。

## 线性渐变画笔

Brushes 用于填充形状内部。有几种类型的画笔，包括 HatchBrush、LinearGradientBrush、PathGradientBrush、SolidBrush 和 TextureBrush。当你用它们填充图形形状时，这些画笔类型会产生特定类型的效果。当你需要一个画笔时，可以创建一个这些画笔类型之一的实例，或使用包含预定义纯色画笔的 Brushes 类。

如果这本书以彩色印刷，从图 3-1 你可以看到自定义圆形按钮正在使用 LinearGradientBrush 来增强 3D 效果。LinearGradientBrush 是一种画笔，其阴影在画笔绘制的空间上从起始颜色渐变到结束颜色。你可能已经注意到这种做法经常用于启动画面或旧式安装程序中。

LinearGradientBrush 有多个重载的构造函数。Listing 3-3 中第 45 到 50 行使用的版本接受两个点和两种颜色。点表示渐变的开始和结束点，颜色表示渐变的起始和结束颜色。在示例中，通过使用白色起始颜色和较暗的结束颜色，我们获得了光线照射在按钮上的外观，从而增强了 3D 外观。

你可以确定大量用于细化渐变效果的属性。Blend 属性是一个类，描述在渐变沿线位置使用开始和结束颜色的百分比。GammaCorrection 属性是一个布尔值，显示是否对渐变应用伽马校正。InterpolationColors 属性使你能够确定一个 ColorBlend，支持显示多色线性渐变。LinearColors 属性是一个包含渐变开始和结束颜色的数组。Transform 属性定义一个 Matrix，使你能够平移、缩放、旋转或倾斜渐变。最后，Rectangle 属性定义渐变画笔的开始和结束点。

LinearGradientBrush 用于绘制 RoundButtons 的内部。用于创建渐变的色调取决于 down 字段的值。向上按钮较浅，向下按钮较暗。

Listing 3-6 显示了 LinearGradientBrush 的 RotateTransform 和 SetTriangularShape 方法。你应该运行代码以查看完美的增强可视化效果。在高对比度下几乎无法真实再现它。

### 特征化 Tracker 控件

就我们的目的而言，将 Tracker 实现为自定义控件是合理的。Tracker 在图 3-1 中显示为 PlayControl 顶部的小滑块。Tracker 的行为与你很可能已经熟悉的 ProgressBar 控件类似。

与 ProgressBar 类似，Tracker 使用图形来显示相对进度。Tracker 使客户端能够指定最小值、最大值和位置值。如果位置更接近最小值，则图形进度指针更接近控件的左侧；如果位置更接近最大值，则进度指针向控件的右侧移动。

实现 Tracker 控件将使你能够更详细地研究 GDI+。Tracker 的完整源代码列表定义在 VideoKiosk.sln 的 Controls.dll 项目中的 Tracker.cs 中。Least
