

```
Closed_polyline cpl = {
{100,100}, {150,200}, {250,250}, {300,200}
};
```

结果（自然）与§13.6中的结果相同，只是那条最终的闭合线除外：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_489_0.png)

**Closed_polyline**的定义如下：

```
struct Closed_polyline : Open_polyline {
using Open_polyline::Open_polyline; // closed sequence of lines

void draw_lines() const; // use Open_polyline's
}; // constructors (§A.16)
```

```
void Closed_polyline::draw_lines() const
{
Open_polyline::draw_lines(); // first draw the “open polyline part”

// then draw closing line:
if (2<number_of_points() && color().visibility())
fl_line(point(number_of_points()-1).x,
point(number_of_points()-1).y,
point(0).x,
point(0).y);
}
```

**using** 声明（§A.16）表明 **Closed_polyline** 具有与 **Open_polyline** 相同的构造函数。**Closed_polyline** 需要自己的 `draw_lines()` 来绘制连接最后一个点与第一个点的闭合线。

我们只需要处理 **Closed_polyline** 与 **Open_polyline** 所提供的不同之处这一小细节。这一点非常重要，有时被称为“差异编程”。我们只需要编程实现我们的派生类（在此为 **Closed_polyline**）与基类（在此为 **Open_polyline**）所呈现的差异部分。

那么，我们如何绘制那条闭合线呢？我们使用 FLTK 的绘制直线函数 `fl_line()`。它接受四个代表两个点的 **int**。因此，这里再次使用了底层的图形库。然而请注意，正如其他所有情况一样，对 FLTK 的提及仅保留在我们类的实现中，而不是暴露给用户。用户代码无需提及 `fl_line()`，也无需了解那些点以整数对形式隐式出现的接口。如果我们愿意，可以用另一个 GUI 库替换 FLTK，而对我们用户的代码影响甚微。

## 13.8 多边形

**Polygon**（多边形）与 **Closed_polyline** 非常相似。唯一的区别在于，对于 **Polygon**，我们不允许线段相交。例如，上面的 **Closed_polyline** 是一个多边形，但我们可以添加另一个点：

```
cpl.add(Point{100,250});
```

结果如下：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_490_0.png)

根据经典定义，这个 **Closed_polyline** 不是多边形。我们如何定义 **Polygon**，以便在不违反几何规则的前提下，正确捕捉到它与 **Closed_polyline** 的关系？上述介绍中包含了强烈的提示。**Polygon** 是一个线段不相交的 **Closed_polyline**。或者，我们可以强调形状是由点构建的方式，并说明 **Polygon** 是一个 **Closed_polyline**，其中我们不能添加一个定义相交线段的 **Point**。

基于该思想，我们这样定义 **Polygon**：

```cpp
struct Polygon : Closed_polyline {    // closed sequence of nonintersecting
                                       // lines
    using Closed_polyline::Closed_polyline; // use Closed_polyline's
                        // constructors
    void add(Point p);
    void draw_lines() const;
};

void Polygon::add(Point p)
{
    // check that the new line doesn't intersect existing lines (code not shown)
    Closed_polyline::add(p);
}
```

在这里，我们继承了 **Closed_polyline** 的 **draw_lines()** 定义，从而节省了大量工作并避免了代码重复。不幸的是，我们必须检查每次 **add()**。这产生了一个低效的（*N* 平方阶）算法 – 定义一个包含 *N* 个点的 **Polygon** 需要调用 *N*( *N*-1)/2 次 **intersect()**。实际上，我们假设 **Polygon** 类将用于点数较少的多边形。例如，创建一个包含 24 个 **Points** 的 **Polygon** 涉及 24*(24–1)/2 = 276 次 **intersect()** 调用。这可能是可以接受的，但如果我们要一个包含 2000 个点的面多边形，那将耗费大约 2,000,000 次调用，我们可能会寻找更好的算法，这可能需要修改接口。

使用初始化列表构造函数，我们可以像这样创建一个多边形：

```cpp
Polygon poly = {
    {100,100}, {150,200}, {250,250}, {300,200}
};
```

显然，这创建了一个与我们原始 **Closed_polyline** 完全相同（精确到最后一个像素）的 **Polygon**：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_492_0.png)

确保 **Polygon** 真正代表一个多边形结果出奇地复杂。我们在 **Polygon::add()** 中省略的相交检查，可以说是在整个图形库中最复杂的。如果你对繁琐的几何坐标操作感兴趣，请查看代码。

问题在于 **Polygon** 的不变量“这些点表示一个多边形”只有在所有点都定义完成后才能验证；也就是说，我们没有——尽管强烈建议——在其构造函数中建立 **Polygon** 的不变量。我们考虑过移除 **add()** 并强制要求通过至少包含三个点的初始化列表完全指定 **Polygon**，但这会使程序中生成点序列的用例变得复杂。

## 13.9 矩形

屏幕上最常见的形状是矩形。原因部分是文化上的（我们的大部分门、窗、图片、墙壁、书架、书页等也是矩形的），部分也是技术上的（将坐标保持在矩形空间内比任何其他形状的空间都简单）。无论如何，矩形如此常见，以至于 GUI 系统直接支持它们，而不是仅仅将它们视为恰好有四个角和直角的普通多边形。

```cpp
struct Rectangle : Shape {
    Rectangle(Point xy, int ww, int hh);
    Rectangle(Point x, Point y);
    void draw_lines() const;

    int height() const { return h; }
    int width() const { return w; }
private:
    int h;    // height
    int w;    // width
};
```

我们可以通过两个点（左上角和右下角）或一个点（左上角）以及宽度和高度来指定一个矩形。构造函数可以这样定义：

```cpp
Rectangle::Rectangle(Point xy, int ww, int hh)
    : w{ww}, h{hh}
{
    if (h<=0 || w<=0)
        error("Bad rectangle: non-positive side");
    add(xy);
}

Rectangle::Rectangle(Point x, Point y)
    : w{y.x-x.x}, h{y.y-x.y}
{
    if (h<=0 || w<=0)
        error("Bad rectangle: first point is not top left");
    add(x);
}
```

每个构造函数都适当地初始化成员 **h** 和 **w**（使用成员初始化语法；参见 §9.4.4），并将左上角点存储在 **Rectangle** 的基类 **Shape** 中（使用 **add()**）。此外，它还执行一个简单的合理性检查：我们确实不想要宽度或高度为负的 **Rectangles**。

某些图形/GUI 系统将矩形视为特殊对象的原因之一是，确定哪些像素位于矩形内部的算法比多边形和圆形等其他形状要简单得多——因此也快得多。因此，“填充颜色”的概念——即矩形内部区域的颜色——在矩形中比在其他形状中更常用。我们可以在构造函数中设置填充颜色，或者通过 set_fill_color() 操作（由 Shape 提供的与其他颜色相关服务一起提供）：

```
Rectangle rect00 {Point({150,100},200,100};
Rectangle rect11 {Point({50,50},Point({250,150}};
Rectangle rect12 {Point({50,150},Point({250,250}}; // just below rect11
Rectangle rect21 {Point({250,50},200,100}; // just to the right of rect11
Rectangle rect22 {Point({250,150},200,100}; // just below rect21

rect00.set_fill_color(Color::yellow};
rect11.set_fill_color(Color::blue};
rect12.set_fill_color(Color::red};
rect21.set_fill_color(Color::green};
```

这产生了

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_494_0.png)

当没有填充颜色时，矩形是透明的；这就是你如何看到黄色 `rect00` 的角落。

我们可以移动窗口中的形状（§14.2.3）。例如：

```cpp
rect11.move({400, 0});        // to the right of rect21
rect11.set_fill_color(Color::white);
win12.set_label("rectangles 2");
```

这产生了

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_495_0.png)

注意只有部分白色 `rect11` 位于窗口内。不适合的部分被“裁剪”了；也就是说，它不会在屏幕上的任何地方显示。

还要注意形状是如何一个叠在另一个上面的。这就像你把纸放在桌子上一样。你放的第一张纸会在最下面。我们的 `Window`（§E.3）提供了一种重新排列形状的简单方法。你可以告诉窗口将某个形状放在顶部（使用 `Window::put_on_top()`）。例如：

```cpp
win12.put_on_top(rect00);
win12.set_label("rectangles 3");
```

