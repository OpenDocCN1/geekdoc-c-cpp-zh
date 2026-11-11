
点、网格和图像。这些各种实体的详细信息在本书网站上给出。

### 4.4 动画

正如你在第 2 章看到的，WPF 包含用于创建动画的工具。你几乎可以对任何类型的值——`double`、`Point` 等——进行动画处理，然后使用这个变化的值来使显示发生变化。你可以在 XAML 代码或 C# 中定义动画。对于 XAML，有许多预定义动画，你可以将它们组合起来制作相当复杂的运动。在 C# 代码中，你可以使用这些预定义动画，也可以使用任意复杂的程序创建自己的动画。例如，你可以编写一个程序来计算弹跳球随时间变化的位置，然后使用这个变化的位置来控制显示中某个形状（如圆盘）的位置。用 XAML 编写模拟程序并不现实，因此用 C# 编写这样的程序更自然。

在我们的示例中，只有一个动画，但它展示了关键思想（见代码清单 4.8）。在代码中，我们构造了一条线段，其一个端点位于一个名为 `p1` 的 `Dot` 上。在这段代码中，我们通过指定起点和终点位置、动画应持续多长时间（它从时间 0 开始，即程序运行时开始，并持续五秒），以及它应自动反向并永远重复，来对一个点进行动画处理。（顺便说一句，这个相对简单的动画是可以用 XAML 轻松描述的一个例子。）结果是一个随时间在两个指定位置之间来回移动的点。注意，这个点实际上并没有显示在 `GraphPaper` 上；它只是一个值不断变化的 `Point`。但是，`p1.BeginAnimation(Dot.PositionProperty, animaPoint1)` 这一行表示，名为 `p1` 的 `Dot` 的 `PositionProperty` 应由 `animaPoint1` 进行动画处理；这会使该 `Dot` 在显示中来回移动。再次，WPF 的依赖机制在做繁重的工作：它检测 `animaPoint1` 的每一次变化，并确保 `p1` 的 `PositionProperty` 也随之改变；这个属性决定了 `Dot` 在画布上的位置，因此我们能看到运动。

*代码清单 4.8：对 Point 进行动画处理的代码。*

```csharp
1   PointAnimation animaPoint1 = new PointAnimation(
2       new Point(-20, -20),
3       new Point(-40, 20),
4       new Duration(new TimeSpan(0, 0, 5)));
5   animaPoint1.AutoReverse = true;
6   animaPoint1.RepeatBehavior = RepeatBehavior.Forever;
7   p1.BeginAnimation(Dot.PositionProperty, animaPoint1);
```

![](img/f464cd0043eb5336aa0543fe20a0561b_144_0.png)

我们一直在相当自由地使用 `Point`，给它们的 x 和 y 坐标赋值。严格遵循面向对象编程信条可能会要求我们将这些坐标视为要隐藏的实例变量，并且只能通过访问器/修改器（或 get/set）方法访问它们。事实上，`Point` 更像 Pascal 记录或 C 结构体，而不是典型的 C++ 或 Java 对象。在模糊记录（相关值的集合）与对象之间的区别时，C# 允许这种用法，这可以对效率产生巨大影响，而对可调试性的影响相对较小。

### 4.5 交互

我们已经讨论了测试平台（以及一般而言的 WPF）中如何处理按钮单击和滑块值更改：会调用 `Click` 或 `ValueChanged` 方法。

键盘交互略有不同。在主 `Window` 中任何位置发生的按键都分两个阶段处理：首先，其中一些被识别为命令（例如“Alt-X”表示“退出程序”）；其次，那些未被识别为命令的按键由名为 `KeyDownHandler` 的方法处理，该方法对所有按键作出响应：要么忽略它们（对于按在 Control 或 Shift 等修饰键上的情况），要么显示一个小对话框，指示按下了哪个键。当你编写更复杂的程序时，你可能希望将这部分代码添加到其中，以便在按下某些键时执行特定操作。

最后，选择菜单项时执行的操作在 `InitializeCommands` 方法中定义。对于许多命令（如 `ApplicationCommands.Close`，表示应用程序应关闭窗口），已经有预定义的处理方式以及与命令关联的预定义按键。对于这些命令，只需编写类似 `CommandBindings.Add(new CommandBinding(ApplicationCommands.Close, CloseApp));` 的内容，其中 `CloseApp` 是一个小过程，它会弹出一个对话框，以确认用户确实想要关闭应用程序。对于其他命令，必须调用稍微更复杂的机制。由于我们不期望你添加任何新命令，因此是否研究这样做的机制由你决定。

### 4.6 测试平台的一个应用

现在让我们回到本章开头讨论过的切角示例。为了创建一个演示这一点的应用程序，我们需要移除 `Window1.cs` 中的大部分代码，并从用户创建的一个简单多边形开始。我们将描述交互序列，然后编写代码。

`GraphPaper` 一开始是空的；有两个按钮，分别标记为“Clear”和“Subdivide”。当用户在绘图纸上单击时，会出现一个多边形 P1，其顶点位于单击位置（单击两次后，该多边形由两条相同的线段组成；单击三次后，是一个三角形；依此类推）。当用户单击 Subdivide 按钮时，会出现第一个多边形的细分版本 P2；随后单击 Subdivide 会用 P2 替换 P1，并用 P2 的细分版本替换 P2，依此类推，因此多边形及其细分版本始终都会显示。单击 Clear 按钮会清空绘图纸。一旦用户细分了多边形，我们就禁用对绘图纸的进一步单击；你可能希望此类单击向细分后的多边形添加新点，但不清楚新点应添加到细分后多边形的何处，因此我们干脆避开这个问题。

记住这一描述，让我们编写代码。⁷ 我们需要一个 isSubdivided 标志（初始为 `false`）来告诉我们用户是否已细分多边形。Clear 按钮应重置该标志，并清空绘图纸。如果多边形中还没有点，Subdivide 应不起作用。

我们从测试平台代码的副本开始，并修改 XAML 以移除滑块并更改按钮上的文本：

7. 整个程序可在本书网站上下载。

```xml
<StackPanel DockPanel.Dock="Left"
    Orientation="Vertical" Background="#ECE9D8">
    <TextBlock Margin="3" Text="Controls"/>
    <Button Margin="3,5" HorizontalAlignment="Left"
    Click="b1Click">Subdivide</Button>
    <Button Margin="3,5" HorizontalAlignment="Left"
    Click="b2Click">Clear</Button>
</StackPanel>
```

现在我们修改 Window1.xaml.cs 中的 C# 代码。首先将两个多边形都初始化为空：

```csharp
public partial class Window1 : Window
{
    Polygon myPolygon = new Polygon();
    Polygon mySubdivPolygon = new Polygon();
    bool isSubdivided = false;
    GraphPaper gp = null;
    [...]
    public Window1()
    {
        [...]
        initPoly(myPolygon, Brushes.Black);
        initPoly(mySubdivPolygon, Brushes.Firebrick);
        gp.Children.Add(myPolygon);
        gp.Children.Add(mySubdivPolygon);

        ready = true; // Now we're ready to have sliders
                      // and buttons influence the display.
    }
```

多边形初始化过程还将多边形设置为具有不同的颜色和标准线宽，并确保当两条边以锐角相交时，它们会被截断，如图 4.4 底部所示，而不是像中间所示那样将连接处延伸成长斜接。

![](img/f464cd0043eb5336aa0543fe20a0561b_146_0.png)

图 4.4：当我们加粗顶部的顶点连接处时，必须对其进行斜接，如中间所示。在底部，斜接受到限制。

```csharp
private void initPoly(Polygon p, SolidColorBrush b)
{
    p.Stroke = b;
    p.StrokeThickness = 0.5; // 0.5 mm thick line
    p.StrokeMiterLimit = 1;  // no long pointy bits at vertices
    p.Fill = null;
}
```

处理对 Clear 按钮的单击很简单：我们只需从每个多边形中移除所有点，并将 isSubdivided 标志重新设置为 false：

```csharp
// Clear button
public void b2Click(object sender, RoutedEventArgs e)
{
    myPolygon.Points.Clear();
    mySubdivPolygon.Points.Clear();
    isSubdivided = false;

    e.Handled = true; // don't propagate click further
}
```

Subdivide 按钮更复杂。首先，如果多边形已经细分，我们希望用细分后多边形的点替换 myPolygon 的点。然后，我们可以细分 myPolygon，并将结果放入 mySubdivPolygon。
