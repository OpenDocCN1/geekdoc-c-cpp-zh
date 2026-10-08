

这会产生三个不同大小的圆，它们的圆心在一条水平线上对齐：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_503_0.png)

**Circle** 实现的主要特殊性在于，存储的点不是圆心，而是包围该圆的正方形的左上角。我们本可以存储其中任何一个，但选择了 FLTK 用于其优化圆绘制例程的那个。这样，**Circle** 提供了另一个示例，说明类如何用于呈现一个概念的不同（且据称更好）的视图，与其实现相比：

```cpp
Circle::Circle(Point p, int rr)      // 中心和半径
      :r(rr)
{
    add(Point{p.x-r,p.y-r});          // 存储左上角
}

Point Circle::center() const
{
    return {point(0).x+r, point(0).y+r};
}

void Circle::draw_lines() const
{
    if (color().visibility())
        fl_arc(point(0).x,point(0).y,r,r,r+r,0,360);
}
```

注意使用 `fl_arc()` 来绘制圆。前两个参数指定左上角，接下来两个参数指定包围圆的矩形的宽度和高度，最后两个参数指定要绘制的起始和结束角度。通过走完整的 360 度来绘制一个圆，但我们也可以使用 `fl_arc()` 来绘制圆的一部分（以及椭圆的一部分）；请参见练习 1。

### 13.13 椭圆

椭圆与 **Circle** 类似，但它是用长轴和短轴定义的，而不是用半径；也就是说，要定义一个椭圆，我们给出圆心的坐标，从圆心到 *x* 轴上一点的距离，以及从圆心到 *y* 轴上一点的距离：

```cpp
struct Ellipse : Shape {
    Ellipse(Point p, int w, int h);    // 圆心，到圆心的最大和最小距离

    void draw_lines() const;

    Point center() const;
    Point focus1() const;
    Point focus2() const;

    void set_major(int ww)
    {
        set_point(0,Point(center().x-ww,center().y-h});    // 保持
                                                           // 圆心不变

        w = ww;
    }
    int major() const { return w; }

    void set_minor(int hh)
    {
        set_point(0,Point(center().x-w,center().y-hh});    // 保持
                                                           // 圆心不变

        h = hh;
    }
    int minor() const { return h; }

private:
    int w;
    int h;
};
```

我们可以像这样使用 **Ellipse**：

```cpp
Ellipse e1 {Point(200,200),50,50};
Ellipse e2 {Point(200,200),100,50};
Ellipse e3 {Point(200,200),100,150};
```

这给了我们三个具有共同圆心但不同大小轴线的椭圆：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_505_0.png)

请注意，当 **Ellipse** 的 **major()**==**minor()** 时，它看起来就像一个圆。

椭圆的另一种常见视图指定了两个焦点以及从某点到焦点的距离之和。给定一个 **Ellipse**，我们可以计算出一个焦点。例如：

```cpp
Point focus1() const
{
    if (h<=w)     // 焦点在 x 轴上：
        return {center().x+int(sqrt(double(w*w-h*h))),center().y};
    else          // 焦点在 y 轴上：
        return {center().x,center().y+int(sqrt(double(h*h-w*w)))};
}
```

为什么 **Circle** 不是 **Ellipse**？从几何上讲，每个圆都是椭圆，但并非每个椭圆都是圆。特别是，圆是两个焦点相等的椭圆。想象一下，如果我们定义 **Circle** 为 **Ellipse** 会怎样。我们可以这样做，但代价是其表示需要额外的值（圆由一个点和一个半径定义；椭圆需要圆心和一对轴线）。我们不喜欢不必要的空间开销，但我们的 **Circle** 不是 **Ellipse** 的主要原因是，如果不以某种方式禁用 `set_major()` 和 `set_minor()`，我们就无法这样定义它。毕竟，如果我们可以使用 `set_major()` 来获得 `major() != minor()`，那么它就不再是一个圆（正如数学家所认定的那样）——至少在那之后它就不再是一个圆了。我们不能有一个对象在某些时候（即当 `major() == minor()` 时）是一种类型（**Circle**），在另一些时候（即当 `major() != minor()` 时）是另一种类型（**Ellipse**）。我们可以拥有一个有时看起来像圆的对象（即 **Ellipse**）。另一方面，**Circle** 永远不会变形为具有两个不等轴的椭圆。

当我们设计类时，我们必须小心，不要过于聪明，也不要被我们的“直觉”所欺骗，从而定义出在我们的代码中作为类没有意义的类。相反，我们必须确保我们的类代表某个连贯的概念，而不仅仅是一组数据和函数成员。不思考我们正在表达什么思想/概念，只是随意地把代码堆在一起是“黑客行为”，会导致我们无法解释且他人无法维护的代码。如果你不觉得这是利他主义，请记住“他人”可能是几个月后的你自己。这样的代码也更难调试。

### 13.14 Marked_polyline

我们经常想在图表上“标记”点。显示图表的一种方式是在一条开放折线上，因此我们需要一条在点处带有“标记”的开放折线。**Marked_polyline** 做到了这一点。例如：

```cpp
Marked_polyline mpl{"1234"};
mpl.add(Point(100,100));
mpl.add(Point(150,200));
mpl.add(Point(250,250));
mpl.add(Point(300,200));
```

这会产生

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_507_0.png)

**Marked_polyline** 的定义是

```cpp
struct Marked_polyline : Open_polyline {
    Marked_polyline(const string& m) :mark{m} { if (m=="") mark = "*"; }
    Marked_polyline(const string& m, initializer_list<Point> lst);
    void draw_lines() const;
private:
    string mark;
};
```

通过从 **Open_polyline** 派生，我们“免费”获得了 **Points** 的处理；我们要做的只是处理标记。特别是，**draw_lines()** 变成

```cpp
void Marked_polyline::draw_lines() const
{
    Open_polyline::draw_lines();
    for (int i=0; i<number_of_points(); ++i)
        draw_mark(point(i),mark[i]%mark.size());
}
```

调用 `Open_polyline::draw_lines()` 处理线条，因此我们只需处理“标记”。我们提供标记为字符字符串，并按顺序使用它们：`mark[i]%mark.size()` 通过在创建 `Marked_polyline` 时提供的字符中循环选择下一个要使用的字符。`%` 是取模（余数）运算符。这个 `draw_lines()` 使用了一个辅助函数 `draw_mark()` 来实际在给定点处输出一个字母：

```cpp
void draw_mark(Point xy, char c)
{
    constexpr int dx = 4;
    constexpr int dy = 4;
    string m(1,c);    // 包含单个字符 c 的字符串
    fl_draw(m.c_str(),xy.x-dx,xy.y+dy);
}
```

`dx` 和 `dy` 常量用于将字母居中于该点上方。`string m` 被构造为包含单个字符 `c`。

接受初始化列表的构造函数简单地将该列表转发到 **Open_polyline** 的初始化列表构造函数：

```cpp
Marked_polyline(const string& m, initializer_list<Point> lst)
    :Open_polyline(lst),
    mark{m}
{
    if (m=="") mark = "*";
}
```

对空字符串的测试是必要的，以避免 `draw_lines()` 尝试访问不存在的字符。

给定接受初始化列表的构造函数，我们可以将示例简化为

```cpp
Marked_polyline mpl {"1234",{{100,100}, {150,200}, {250,250}, {300,200}}};
```

### 13.15 Marks

有时，我们想在不连接它们的情况下显示标记。我们为这种情况提供了类 `Marks`。例如，我们可以标记我们在各种示例中使用的四个点，而不将它们用线连接起来：

```cpp
Marks pp {"x",{{100,100}, {150,200}, {250,250}, {300,200}}};
```

这会产生

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_509_0.png)

**Marks** 的一个明显用途是显示代表离散事件的数据，使得绘制连接线是不合适的。例如，一组人的（身高，体重）数据。

**Marks** 只是一个线条**不可见**的 **Marked_polyline**：

```cpp
struct Marks : Marked_polyline {
    Marks(const string& m)
        :Marked_polyline(m)
    {
        set_color(Color{Color::invisible});
    }
    Marks(const string& m, initializer_list<Point> lst)
        : Marked_polyline(m, lst)
    {
        set_color(Color{Color::invisible});
    }
};
```

`::Marked_polyline(m)` 符号用于初始化 **Marks** 对象的 **Marked_polyline** 部分。这种符号是用于初始化成员的语法的变体（§9.4.4）。

