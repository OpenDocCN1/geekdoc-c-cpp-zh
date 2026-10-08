

同样，我们将 **set_point()** 设为 *protected*（受保护的）。通常，只有派生类才知道点的含义，以及在不违反不变量的情况下是否允许修改它。例如，如果我们定义了一个由六个点组成的 **Regular_hexagon**（正六边形）类，仅改变其中一个点就会使图形“不再是正六边形”。另一方面，如果我们改变矩形的一个点，结果仍然是一个矩形。事实上，在我们的示例类代码中，我们并没有发现需要使用 **set_point()**，因此提供 **set_point()** 只是为了确保我们可以读取和设置 **Shape**（图形）的每一个属性这一规则成立。例如，如果我们想要一个 **Mutable_rectangle**（可变矩形），我们可以从 **Rectangle**（矩形）派生它，并提供修改点的操作。

我们将 **Points**（点）的 vector，即 **points**，设为 *private*（私有的），以保护它免受不希望的修改。为了使其有用，我们还需要提供访问它的接口：

```cpp
void Shape::set_point(int i, Point p)  // 未使用；目前不必要
{
   points[i]= p;
}

Point Shape::point(int i) const
{
   return points[i];
}

int Shape::number_of_points() const
{
   return points.size();
}
```

在派生类的成员函数中，这些函数是这样使用的：

```cpp
void Lines::draw_lines() const
// 绘制连接成对点的线
{
   for (int i=1; i<number_of_points(); i+=2)
      fl_line(point(i-1).x,point(i-1).y,point(i).x,point(i).y);
}
```

你可能会担心所有这些琐碎的访问函数。它们难道不是低效的吗？它们会让程序变慢吗？它们会增加生成代码的大小吗？

不，编译器会将它们全部编译掉（“内联”）。调用 **number_of_points()** 所占用的内存字节数和执行的指令数，与直接调用 **points.size()** 完全相同。

这些访问控制的考虑和决策非常重要。我们可以提供一个接近极简版的 **Shape**：

```cpp
struct Shape {    // 接近极简的定义 — 过于简单 — 未使用
    Shape();
    Shape(initializer_list<Point>);
    void draw() const;            // 处理颜色并调用 draw_lines
    virtual void draw_lines() const;   // 绘制相应的线条
    virtual void move(int dx, int dy);    // 移动形状 +=dx 和 +=dy
    virtual ~Shape();

    vector<Point> points;      // 并非所有形状都使用
    Color lcolor;
    Line_style ls;
    Color fcolor;
};
```

我们通过那额外的 12 个成员函数和两行访问说明（**private:** 和 **protected:**）增加了什么价值？基本的回答是，保护表示确保它不会以类设计者未预料到的方式发生变化，从而让我们能够更轻松地编写更好的类。这就是关于“不变量”（§9.4.3）的论点。在这里，当我们定义从 **Shape** 派生的类时，我们将指出此类优势。一个简单的例子是，早期版本的 **Shape** 使用了

```cpp
Fl_Color lcolor;
int line_style;
```

结果发现这限制太多（**int** 类型的线型不能优雅地支持线宽，并且 **Fl_Color** 无法适应 **invisible**（不可见）），并导致了一些混乱的代码。如果这两个变量是 **public**（公共的）并在用户代码中使用过，我们只能在破坏该代码的代价下改进我们的接口库（因为代码中提到了 **lcolor** 和 **line_style** 的名称）。

此外，访问函数通常提供了记法上的便利。例如，**s.add(p)** 比 **s.points.push_back(p)** 更容易阅读和编写。

### 14.2.3 绘制形状

我们现在已经描述了类 **Shape** 几乎全部内容，除了其真正核心部分：

```cpp
void draw() const;          // 处理颜色并调用 draw_lines
virtual void draw_lines() const; // 绘制相应的线条
```

**Shape** 最基本的任务是绘制形状。我们可以移除 **Shape** 的其他所有功能，或者让它不拥有自己的数据，而不会造成重大的概念损害（参见 §14.4），但绘制是 **Shape** 的本职工作。它使用 FLTK 和操作系统的底层机制来实现，但从用户的角度来看，它只提供两个函数：

- `draw()` 应用样式和颜色，然后调用 `draw_lines()`。
- `draw_lines()` 在屏幕上放置像素。

`draw()` 函数没有使用任何新技术。它只是调用 FLTK 函数将颜色和样式设置为 **Shape** 中指定的值，调用 `draw_lines()` 进行实际的屏幕绘制，然后尝试将颜色和样式恢复为调用前的状态：

```cpp
void Shape::draw() const
{
    Fl_Color oldc = fl_color();
    // 没有好的可移植方法来获取当前样式
    fl_color(lcolor.as_int());          // 设置颜色
    fl_line_style(ls.style(),ls.width()); // 设置样式
    draw_lines();
    fl_color(oldc);                     // 重置颜色（恢复为之前）
    fl_line_style(0);                  // 将线样式重置为默认值
}
```

不幸的是，FLTK 没有提供获取当前样式的方法，因此样式只是被设置为默认值。这是为了简单性和可移植性而有时不得不接受的妥协。我们认为不值得尝试在我们的接口库中实现该功能。

请注意，**Shape::draw()** 不处理填充颜色或线条的可见性。这些由各个 `draw_lines()` 函数处理，因为它们更清楚如何解释这些属性。原则上，所有颜色和样式处理都可以委托给各个 `draw_lines()` 函数，但那会非常重复。

现在考虑我们可能如何处理 `draw_lines()`。如果你仔细想想，你会发现对于一个 **Shape** 函数来说，为每种形状绘制所需的一切是很困难的。要做到这一点，要求每种形状的最后一个像素以某种方式存储在 **Shape** 对象中。如果我们保留 `vector<Point>` 模型，我们就得存储大量的点。更糟糕的是，“屏幕”（即图形硬件）已经做到了这一点——而且做得更好。

为了避免这种额外的工作和额外的存储，**Shape** 采取了另一种方法：它让每个 **Shape**（即每个从 **Shape** 派生的类）有机会定义如何绘制它。一个 **Text**（文本）、**Rectangle**（矩形）或 **Circle**（圆形）类可能有一种巧妙的方法来绘制自己。事实上，大多数此类类都这样做了。毕竟，此类类“知道”自己应该表示什么。例如，**Circle**（圆）是由一个点和一个半径定义的，而不是由许多线段定义的。在需要时从点和半径生成 **Circle** 所需的位并不真的那么困难或昂贵。因此，**Circle** 定义了自己的 `draw_lines()`，我们希望在调用 **Shape’s** `draw_lines()` 时调用它。这就是 `draw_lines()` 声明中 `virtual` 的含义：

```cpp
struct Shape {
    // ...
    virtual void draw_lines() const; // 让每个派生类如果愿意可以定义自己的 draw_lines()
    // ...
};

struct Circle : Shape {
    // ...
    void draw_lines() const; // “重写” Shape::draw_lines()
    // ...
};
```

因此，如果 **Shape** 是一个 **Circle**，**Shape’s** `draw_lines()` 必须以某种方式调用 **Circle’s** 其中一个函数；如果 **Shape** 是一个 **Rectangle**，则调用 **Rectangle’s** 其中一个函数。`draw_lines()` 声明中的 `virtual` 一词确保了这一点：如果从 **Shape** 派生的类定义了自己的 `draw_lines()`（类型与 **Shape’s** `draw_lines()` 相同），那么将调用该类的 `draw_lines()` 而不是 **Shape’s** `draw_lines()`。第 13 章展示了如何为 **Text**、**Circle**、**Closed_polyline**（闭合折线）等实现这一点。在派生类中定义函数，以便可以通过基类提供的接口使用，被称为 *overriding*（重写）。

请注意，尽管 `draw_lines()` 在 **Shape** 中起着核心作用，但它被设为 *protected*（受保护的）；它不是给“普通用户”调用的——那是 `draw()` 的作用——而仅仅是作为由 `draw()` 和从 **Shape** 派生的类使用的“实现细节”。

这完成了我们在 §12.2 中描述的显示模型。驱动屏幕的系统了解 `Window`。`Window` 了解 **Shape** 并且可以调用 **Shape’s**

