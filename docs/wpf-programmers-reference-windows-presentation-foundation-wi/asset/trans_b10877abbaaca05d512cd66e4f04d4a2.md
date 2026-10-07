

当 `canField` Canvas 控件调整大同时，会执行以下 `SizeChanged` 事件处理器。这发生在控件首次创建时，以及用户通过调整浏览器大小来调整控件时。

```csharp
private DateTime LastUpdate;
private List<Ball> Balls;
private DispatcherTimer Clock;

// 准备好运行。
private void canField_SizeChanged(object sender, SizeChangedEventArgs e)
{
    GetReady();
}

// 删除所有球。如果用户调整了大小，这是必须的。
canField.Children.Clear();

// 创建一些球。
Balls = new List<Ball>();
Random rand = new Random();
Rect bounds = new Rect(0, 0, canField.ActualWidth, canField.ActualHeight);
for (int i = 1; i <= 5; i++)
{
    Balls.Add(new RandomBall(rand, bounds));
}

// 准备计时器。
LastUpdate = DateTime.Now;
Clock = new DispatcherTimer();
Clock.Interval = TimeSpan.FromSeconds(0.1);
Clock.Tick += Tick;
Clock.Start();
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_450_0.png)

## 弹跳球

程序声明了类级变量，用于存储球最后更新的时间，以及一个提供 `Tick` 事件的 DispatcherTimer 对象的引用。

`SizeChanged` 事件处理器简单地调用了 `GetReady()`。该函数会移除 Canvas 中当前的椭圆（Ellipses）。（尝试注释掉这一步以查看有趣的运行。）

接下来，代码使用 `Random` 函数创建了五个 `Ball` 对象，并将它们存储在 `Balls` 列表中。`Ball` 类用于跟踪屏幕上移动的球的尺寸、位置和速度，将在后文中进行描述。

`RandomBall` 函数简单地创建一个新的 `Ball` 并随机初始化其属性。由于它非常直观，此处暂未显示。

`GetReady` 函数通过准备 `Clock` `DispatcherTimer` 来结束。它创建了计时器，设置其 `Interval` 属性使其每秒十分之一触发一次，为它分配了一个新的 `Tick` 事件处理器，并启动它。

# 414 | 第 24 章 SILVERLIGHT

以下代码显示了大约每秒十分之一触发一次的计时器 `Tick` 事件处理器：

```csharp
// 更新球。
private void Clock_Tick(object sender, EventArgs e)
{
    DateTime time_now = DateTime.Now;
    TimeSpan elapsed = time_now.Subtract(LastUpdate);

    foreach (Ball a_ball in Balls)
    {
        a_ball.Update(elapsed);
    }

    LastUpdate = time_now;
}
```

可从 Wrox.com 下载。

以下代码显示了程序的 `Ball` 类：

```csharp
public class Ball
{
    public Shape MyShape { get; set; }
    public Transform Transform { get; set; }
    public double Vx { get; set; }
    public double Vy { get; set; }
    public Rect Bounds { get; set; }

    // 构造函数。
    public Ball(Shape new_shape, Transform initial_transform, double initial_vx, double initial_vy, Rect the_bounds)
    {
        MyShape = new_shape;
        Transform = initial_transform;
        Vx = initial_vx;
        Vy = initial_vy;
        Bounds = the_bounds;
    }

    // 根据流逝的时间更新位置。
    public void Update(TimeSpan elapsed)
    {
        double x = Transform.X + Vx * elapsed.TotalSeconds;
        if ((Vx < 0) && (x < Bounds.Left))
        {
            // 我们撞击了左墙。
            Vx = -Vx;
            x += 2 * (Bounds.Left - x);
        }
        else if ((Vx > 0) && (x + MyShape.Width > Bounds.Right))
        {
            // 我们撞击了右墙。
            Vx = -Vx;
            x -= 2 * (x + MyShape.Width - Bounds.Right);
        }
    }
}
```

可从 Wrox.com 下载。

## 弹跳球

```csharp
double y = Transform.Y + Vy * elapsed.TotalSeconds;
if ((Vy < 0) && (y < Bounds.Top))
{
    // 我们撞击了顶墙。
    Vy = -Vy;
    y *= 2 * (y + Bounds.Top - y);
} else if ((Vy > 0) && (MyShape.Width > Bounds.Bottom))
{
    // 我们撞击了底墙。
    Vy = -Vy;
    y -= 2 * (y + MyShape.Width - Bounds.Bottom);
}
```

```csharp
Transform.X = x;
Transform.Y = y;
```

`MyShape` 属性持有 `Ball` 所代表的 Silverlight Shape（在本例中为椭圆）的引用。`Transform` 属性持有应用到 Shape 上的 `TranslateTransform` 对象引用。要移动它，`Ball` 会更新此属性。

`Vx` 和 `Vy` 属性提供了球速度的 X 和 Y 分量，单位为像素/秒。`Bounds` 属性是一个 `Rect`，决定了球允许区域。

该类中最有趣的代码是它的 `Update` 方法。该函数将球的速度乘以自上次更新以来流逝的时间加到当前位置上。例如，假设球位于 (30, 60) 位置，以每秒 100 像素的速度向右移动，并假设距离上次更新已过去 0.2 秒。在计算出球的新位置后，代码判断它是否撞击了任何边缘。然后代码更新 `Transform` 属性到其位置。

## 更多信息

本章虽然是必须的，但内容较短。其意图是让你略了解 Silverlight 以及 Silverlight 与 WPF 之间的关系。有关更多信息，请参阅关于 Silverlight 的书籍（J. Ambrose, Wrox, 2009）或《Silverlight 4》（Nick Lecreski, Wrox, 2010）。

## 弹跳球

在互联网上有许多地方可以获取信息。以下列表描述了一些你在学习 Silverlight 时可能会发现的链接：

- Silverlight 首页 (msdn.microsoft.com/library/ee65672)：此页面提供了指向特定 Silverlight 版本页面的链接。目前包括 Silverlight 4 Beta 和 Silverlight 3。例如，如果 Silverlight 4 的链接失效了，你应该在这里找到最新的 Silverlight 4 信息。
- Silverlight 4 首页 (mmsdn.microsoft.com/library/cc838158)：指向关于 Silverlight 4 的完整信息。主题包括概述、控件、输入、打印、图形、动画、通信、性能、部署等。
- Silverlight 3 首页 (msdn.microsoft.com/library/cc83815)：与之前的页面类似，但适用于 Silverlight 3。
- 开始构建 Silverlight  (silverlight.net/getstarted)：这是 Silverlight 官方的入门网页。它包含了许多有用链接以及 Silverlight 经理 Tim Heuer 编写的逐步教程，他带你通过一个使用 Twitter 搜索的示例。
- Silverlight 4 Beta — 新功能指南 (timheur.com/blog/archive/2009/11/18/whats-new-in-silverlight-4-complete-guide-new-features.aspx)：Tim Heuer 的一篇长博客文章，描述了 Silverlight 4 的工具、资源和新功能。

