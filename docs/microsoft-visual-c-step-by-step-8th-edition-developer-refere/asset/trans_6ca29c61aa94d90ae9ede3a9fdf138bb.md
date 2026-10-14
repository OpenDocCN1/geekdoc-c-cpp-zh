

```
void IDraw.SetLocation(int xCoord, int yCoord)
{
    this.locX = xCoord;
    this.locY = yCoord;
}
```

此代码将通过参数传入的值存储在 Square 对象中的 locX 和 locY 字段中。

9. 用此处以粗体显示的语句替换 IDraw.Draw 方法中生成的代码：

Click here to view code image

```
void IDraw.Draw(Canvas canvas)
{
    if (this.rect != null)
    {
        canvas.Children.Remove(this.rect);
    }
    else
    {
        this.rect = new Rectangle();
    }

    this.rect.Height = this.sideLength;
    this.rect.Width = this.sideLength;
    Canvas.SetTop(this.rect, this.locY);
    Canvas.SetLeft(this.rect, this.locX);
    canvas.Children.Add(this.rect);
}
```

此方法通过在画布上绘制 Rectangle 形状来渲染 Square 对象。 （正方形只是一个所有四条边长度相同的矩形。）如果 Rectangle 已被绘制过（可能在不同的位置且颜色不同），则将其从画布中移除。 Rectangle 的高度和宽度通过使用 sideLength 字段的值来设置。 Rectangle 在画布上的位置通过使用 Canvas 类的静态 SetTop 和 SetLeft 方法来设置，然后将 Rectangle 添加到画布中。 （这会导致它被显示。）

10. 将 IColor 接口中的 SetColor 方法添加到 Square 类中，如此处所示：

Click here to view code image

```
void IColor.SetColor(Color color)
{
    if (this.rect != null)
    {
        SolidColorBrush brush = new SolidColorBrush(color);
        this.rect.Fill = brush;
    }
}
```

此方法检查 Square 对象是否已实际显示。 （如果尚未渲染，rect 字段将为 null。）代码使用 SolidColorBrush 对象将 rect 字段的 Fill 属性设置为指定颜色。 （SolidColorBrush 类的工作细节超出了本次讨论的范围。）

11. 在 Project 菜单上，单击 Add Class。 在 Add New Item – Drawing 对话框中，在 Name 框中键入 Circle.cs，然后单击 Add。

Visual Studio 创建 Circle.cs 文件并在 Code and Text Editor 窗口中显示它。

12. 在 Circle.cs 文件顶部，将以下 using 指令添加到列表中：

Click here to view code image

```
using Windows.UI;
using Windows.UI.Xaml.Media;
using Windows.UI.Xaml.Shapes;
using Windows.UI.Xaml.Controls;
```

13. 修改 Circle 类的定义，使其实现 IDraw 和 IColor 接口，如此处以粗体所示：

```
class Circle : IDraw, IColor
{
}
```

14. 将以下以粗体显示的私有变量添加到 Circle 类：

Click here to view code image

```
class Circle : IDraw, IColor
{
    private int diameter;
    private int locX = 0, locY = 0;
    private Ellipse circle = null;
}
```

这些变量将保存 Circle 对象在画布上的位置和大小。 Ellipse 类提供了您将用于绘制圆的功能。

15. 将此处以粗体显示的构造函数添加到 Circle 类：

Click here to view code image

```
class Circle : IDraw, IColor
{
    ...
    public Circle(int diameter)
    {
        this.diameter = diameter;
    }
```

此构造函数初始化 diameter 字段。

## 16. 向 Circle 类添加以下 SetLocation 方法：

Click here to view code image

```
void IDraw.SetLocation(int xCoord, int yCoord)
{
    this.locX = xCoord;
    this.locY = yCoord;
}
```

此方法实现了 IDraw 接口的一部分，其代码与 Square 类中的代码相同。

## 17. 向 Circle 类添加此处显示的 Draw 方法：

Click here to view code image

```
void IDraw.Draw(Canvas canvas)
{
    if (this.circle != null)
    {
        canvas.Children.Remove(this.circle);
    }
    else
    {
        this.circle = new Ellipse();
    }

    this.circle.Height = this.diameter;
    this.circle.Width = this.diameter;
    Canvas.SetTop(this.circle, this.locY);
    Canvas.SetLeft(this.circle, this.locX);
    canvas.Children.Add(this.circle);
}
```

此方法也是 IDraw 接口的一部分。 它与 Square 类中的 Draw 方法类似，只是它通过在画布上绘制 Ellipse 形状来渲染 Circle 对象。 （圆是宽度和高度相同的椭圆。）

## 18. 向 Circle 类添加以下 SetColor 方法：

Click here to view code image

```
void IColor.SetColor(Color color)
{
    if (this.circle != null)
    {
        SolidColorBrush brush = new SolidColorBrush(color);
        this.circle.Fill = brush;
    }
}
```

此方法属于 IColor 接口。 如前所述，此方法与 Square 类的方法类似。

您已完成 Square 和 Circle 类的创建。 现在您可以使用表单来测试它们。

## 测试 Square 和 Circle 类

- 1. 在 Design View 窗口中显示 DrawingPad.xaml 文件。
- 2. 在表单上，单击大阴影区域。
- 表单的阴影区域是 Canvas 对象，此操作将焦点设置到此对象。
- 3. 在 Properties 窗口中，单击 Event Handlers 按钮。 （该按钮的图标看起来像一道闪电。）
- 4. 在事件列表中，找到 Tapped 事件，然后在 Tapped 文本框中双击。
- Visual Studio 为 DrawingPad 类创建名为 drawingCanvas_Tapped 的方法，并在 Code and Text Editor 窗口中显示它。
- 这是一个在用户用手指轻敲画布或在画布上单击鼠标左键时运行的事件处理程序。 您可以在第 20 章“解耦应用程序逻辑和处理事件”中了解更多关于事件处理程序的信息。
- 5. 在 DrawingPad.xaml.cs 文件顶部，将以下 using 指令添加到列表中：
- using Windows.UI;
- Windows.UI 命名空间包含 Colors 类的定义，您将在绘制形状时设置形状的颜色时使用它。
- 6. 将以下以粗体显示的代码添加到 drawingCanvas_Tapped 方法中：

Click here to view code image

```
private void drawingCanvas_Tapped(object sender,
TappedRoutedEventArgs e)
{
    Point mouseLocation = e.GetPosition(this.drawingCanvas);
    Square mySquare = new Square(100);

    if (mySquare is IDraw)
    {
        IDraw drawSquare = mySquare;
        drawSquare.SetLocation((int)mouseLocation.X,
(int)mouseLocation.Y);
        drawSquare.Draw(drawingCanvas);
    }
}
```

此方法中的 *TappedRoutedEventArgs* 参数提供了有关鼠标位置的有用信息。 特别是，*GetPosition* 方法返回一个 *Point* 结构，其中包含鼠标的 x 和 y 坐标。 您添加的代码创建了一个新的 *Square* 对象。 然后它检查以验证此对象是否实现了 *IDraw* 接口（这是良好的做法，有助于确保如果您尝试通过它未实现的接口引用对象，您的代码在运行时不会失败）并通过此接口创建对该对象的引用。 请记住，当您显式实现接口时，接口定义的方法只能通过创建对该接口的引用来使用。 （*SetLocation* 和 *Draw* 方法对 *Square* 类是私有的，只能通过 *IDraw* 接口使用。）代码然后将 *Square* 的位置设置为用户手指或鼠标的位置。 请注意，*Point* 结构中的 x 和 y 坐标实际上是 *double* 值，因此此代码将它们转换为 *ints*。 代码然后调用 *Draw* 方法以显示 *Square* 对象。

7. 在 *drawingCanvas_Tapped* 方法末尾，添加以下以粗体显示的代码：

Click here to view code image

```
private void drawingCanvas_Tapped(object sender,
TappedRoutedEventArgs e)
{
    ...
    if (mySquare is IColor)
    {
        IColor colorSquare = mySquare;
        colorSquare.SetColor(Colors.BlueViolet);
    }
}
```

此代码测试 *Square* 类以验证它是否实现了 *IColor* 接口；如果实现了，代码将通过此接口创建对 *Square* 类的引用并调用 *SetColor* 方法将 *Square* 对象的颜色设置为 *Colors.BlueViolet*。

## Important

您必须在调用 *SetColor* 之前调用 *Draw*，因为 *SetColor* 方法仅在 *Square* 已被渲染时才设置 *Square* 的颜色。 如果您在 *Draw* 之前调用 *SetColor*，颜色将不会被设置且 *Square* 对象不会出现。

8. 返回 Design View 窗口中的 DrawingPad.xaml 文件，然后单击 *Canvas* 对象。

