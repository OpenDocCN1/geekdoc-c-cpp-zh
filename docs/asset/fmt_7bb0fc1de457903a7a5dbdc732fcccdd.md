
# 虚函数调用

# 虚函数表

## 练习

1. 定义两个类 `Smiley`（笑脸）和 `Frowny`（哭脸），它们都派生自类 `Circle`（圆），并且都有两只眼睛和一个嘴巴。接下来，从 `Smiley` 和 `Frowny` 派生类，分别为它们添加一顶合适的帽子。

2. 尝试复制一个 `Shape`（形状）。会发生什么？

3. 定义一个抽象类，并尝试定义该类型的一个对象。会发生什么？

4. 定义一个类 `Immutable_Circle`（不可变圆），它与 `Circle` 类似，但无法移动。

5. 定义一个 `Striped_rectangle`（条纹矩形），不使用填充，而是通过在矩形内部绘制水平线条来“填充”矩形（例如，每隔一行绘制一条这样的线）。你可能需要调整线宽和行距，以获得喜欢的图案。

6. 使用 `Striped_rectangle` 的技术定义一个 `Striped_circle`（条纹圆）。

7. 使用 `Striped_rectangle` 的技术定义一个 `Striped_closed_polyline`（条纹闭合折线）（这需要一定的算法创造力）。

8. 定义一个类 `Octagon`（正八边形）。编写一个测试，测试其所有函数（由你定义或从 `Shape` 继承而来的函数）。

9. 定义一个 `Group`（组），它是 `Shape` 的容器，并对 `Group` 中的各个成员应用合适的操作。提示：`Vector_ref`。使用一个

10. 定义一个类 **`Pseudo_window`**（伪窗口），在不付出巨大努力的前提下，尽可能使其看起来像一个 **`Window`**（窗口）。它应该有圆角、标签和控制图标。你可能添加一些虚假的“内容”，例如一张图片。它实际上不需要做任何事。让它出现在一个 **`Simple_window`** 中是可以接受的（甚至推荐这样做）。

11. 定义一个 **`Binary_tree`**（二叉树）类，派生自 **`Shape`**。将层级数作为参数（**`levels===0`** 表示没有节点，**`levels===1`** 表示一个节点，**`levels===2`** 表示一个顶层节点和两个子节点，**`levels===3`** 表示一个顶层节点，每个节点有两个子节点，以此类推）。让节点由一个小圆表示。用线连接节点（这是惯例）。附注：在计算机科学中，树是从顶层节点向下生长的（有趣地，但合乎逻辑；通常称为根）。

12. 修改 **`Binary_tree`** 以使用虚函数绘制其节点。然后，从 **`Binary_tree`** 派生一个新类，重写该虚函数，以使用不同的节点表示（例如，三角形）。

13. 修改 **`Binary_tree`** 以接受一个参数（或多个参数），指示使用哪种线来连接节点（例如，指向下方的箭头或指向红色的向上箭头）。注意本练习和上一个练习如何以两种替代方式使类层次结构更加灵活和有用。

14. 为 **`Binary_tree`** 添加一个操作，向节点添加文本。你可能需要修改 **`Binary_tree`** 的设计才能优雅地实现这一点。选择一种识别节点的方式；例如，你可以给出一个字符串 `"lrllr"` 来导航二叉树，依次向左、向右、向左、向右、向右移动（根节点匹配初始的 **`l`** 和初始的 **`r`**）。

15. 大多数类层次结构与图形无关。定义一个类 **`Iterator`**，其中有一个纯虚函数 **`next()`**，返回 **`double*`**（参见第 17 章）。现在从 **`Iterator`** 派生 **`Vector_iterator`** 和 **`List_iterator`**，使得 **`Vector_iterator`** 的 **`next()`** 产生指向 **`vector<double>`** 下一个元素的指针，而 **`List_iterator`** 对 **`list<double>`** 做同样的事。你用 **`vector<double>`** 初始化 **`Vector_iterator`**，并且第一次调用 **`next()`** 会返回指向其第一个元素的指针（如果有）。如果没有下一个元素，则返回 0。通过使用该函数 **`void print(Iterator&)`** 来打印 **`vector<double>`** 和 **`list<double>`** 的元素来测试这一点。

16. 定义一个类 **`Controller`**（控制器），包含四个虚函数 **`on()`**、**`off()`**、**`set_level(int)`** 和 **`show()`**。从 **`Controller`** 派生至少两个类。其中一个应该是一个简单的测试类，其中 **`show()`** 打印该类是否设置为开或关以及当前级别。第二个派生类应该以某种方式控制 **`Shape`** 的线颜色；“级别”的具体含义由你决定。尝试找到第三个用这样的 **`Controller`** 类控制的“事物”。

17. C++ 标准库中定义的异常，例如 **`exception`**、**`runtime_error`** 和 **`out_of_range`** （\S 5.6.3），被组织成一个类层次结构（具有一个有用的虚函数 `what()`），返回一个字符串，该字符串据称解释了出了什么问题。在你的信息来源中搜索 C++ 标准异常类层次结构，并绘制其类层次结构图。

# 后记

软件的理想目标不是构建一个做所有事情的大型程序。理想的目标是构建许多紧密反映我们概念并能协同工作的类，使我们能够以优雅的方式构建应用程序，付出相对较少的努力（相对于任务的复杂性），具备足够的性能，并确信产生的结果是正确的。这样的程序在可理解性和可维护性方面，优于那些仅仅为了尽快完成特定任务而匆忙拼凑的代码。类、封装（由 **`private`** 和 **`protected`** 支持）、继承（由类派生支持）以及运行时多态（由虚函数支持）是我们用于构建系统结构的最强大工具之一。

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_551_0.png)

# 15 绘制函数和数据图

> “最好是最好的敌人。”
>
> —伏尔泰

如果你从事任何实证领域，你需要绘制数据图。如果你从事任何使用数学来建模现象的领域，你需要绘制函数图。本章讨论此类图形的基本机制。照例，我们展示这些机制的使用，并讨论其设计。关键示例是绘制单参数函数和显示从文件读取的值。

## 15.1 简介

## 15.2 绘制简单函数

## 15.3 函数

### 15.3.1 默认参数

### 15.3.2 更多示例

### 15.3.3 Lambda 表达式

## 15.4 坐标轴

## 15.5 近似

## 15.6 绘制数据图

### 15.6.1 读取文件

### 15.6.2 通用布局

### 15.6.3 数据缩放

### 15.6.4 构建图形

## 15.1 简介

与如果你以此为职业时使用的专业软件系统相比，这里介绍的功能很原始。我们的主要目的不是输出的优雅，而是理解如何生成此类图形输出以及使用的编程技术。你会发现在这里介绍的设计技术、编程技术和基本数学工具比介绍的图形功能具有更长期的价值。因此，请不要匆匆略过代码片段——它们包含的兴趣点远不止于它们计算和绘制的形状。

## 15.2 绘制简单函数

让我们开始。让我们看看我们可以绘制的示例以及绘制它们所需的代码。特别是，看看使用的图形接口类。首先，这是一条抛物线、一条水平线和一条斜线：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_552_0.png)

实际上，由于本章的主题是绘制函数图像，那条水平线不仅仅是一条水平线；它是我们对函数进行绘图得到的结果：

```cpp
double one(double) { return 1; }
```

这是我们所能想到的最简单的函数：它是一个只有一个参数的函数，对于每个参数都返回`1`。由于我们不需要该参数来计算结果，因此我们无需为其命名。对于作为参数传递给`one()`的每个`x`，我们得到`y`值`1`；也就是说，该直线由(`x,y`)==(`x`,`1`)定义，对所有`x`成立。

与所有初级的数学论证一样，这有点琐碎和吹毛求疵，因此让我们来看一个稍微复杂一点的函数：

```cpp
double slope(double x) { return x/2; }
```

这是生成那条倾斜直线的函数。对于每个`x`，我们得到`y`值`x/2`。换句话说，(`x,y`)==(`x`,`x/2`)。两条直线相交的点是(`2`,`1`)。

现在我们可以尝试一些更有趣的内容，即似乎经常在这本书中重新出现的平方函数：

```cpp
double square(double x) { return x*x; }
```

如果你记得中学几何（即使你不记得），这定义了一个抛物线，其最低点位于(`0,0`)，并且关于*y*轴对称。换句话说，(`x,y`)==(`x`,`x`²)。因此，抛物线与倾斜直线相切的最低点是(`0,0`)。

以下是绘制这三个函数的代码：

```cpp
constexpr int xmax = 600;    // 窗口大小
constexpr int ymax = 400;

constexpr int x_orig = xmax/2;    // (0,0) 的位置是窗口中心
constexpr int y_orig = ymax/2;
constexpr Point orig {x_orig, y_orig};

constexpr int r_min = -10;        // 范围 [-10:11]
constexpr int r_max = 11;

constexpr int n_points = 400;     // 范围内使用的点数

constexpr int x_scale = 30;       // 缩放因子
constexpr int y_scale = 30;

Simple_window win {Point{100,100}, xmax, ymax, "函数绘图"};

Function s {one, r_min, r_max, orig, n_points, x_scale, y_scale};
Function s2 {slope, r_min, r_max, orig, n_points, x_scale, y_scale};
Function s3 {square, r_min, r_max, orig, n_points, x_scale, y_scale};

win.attach(s);
win.attach(s2);
win.attach(s3);
win.wait_for_button();
```

首先，我们定义了一堆常量，以便不必在代码中到处散布“魔法常量”。然后，我们创建一个窗口，定义函数，将它们附加到窗口上，最后将控制权交给图形系统以完成实际的绘图。

除了三个`Function`的定义 s, s2 和 s3 之外，这一切都是重复和“样板代码”：

```cpp
Function s {one, r_min, r_max, orig, n_points, x_scale, y_scale};
Function s2 {slope, r_min, r_max, orig, n_points, x_scale, y_scale};
Function s3 {square, r_min, r_max, orig, n_points, x_scale, y_scale};
```

每个`Function`指定了其第一个参数（一个接受一个`double`参数并返回`double`的函数）如何在窗口中绘制。第二个和第三个参数给出`x`的范围（即要绘制图像的函数的参数）。第四个参数（此处为`orig`）告诉`Function`原点(0,0)应位于窗口内的哪个位置。

如果你觉得这么多参数令人困惑，我们也这么认为。我们的理想是尽可能少地提供参数，因为很多参数会让人困惑并提供出错的機會。然而，这里我们需要它们。稍后（§15.3）我们将解释最后三个参数。但是，首先，让我们给我们的图形加上标签：

![image](img/e0ceba017429f80f5cf63e81a1e7ef4f_554_0.png)

我们总是试图使我们的图形自我解释。人们并不总是阅读周围的文本，而好的图表会被移动，使得周围的文本“丢失”。我们作为图片本身一部分放入的任何内容都最有可能被注意到，并且——如果合理的话——最有可能帮助读者理解我们正在展示什么。在这里，我们只是在每个图形上放了一个标签。“标记”的代码是三个`Text`对象（参见§13.11）：

```cpp
Text ts {Point{100, y_orig-40}, "one"};
Text ts2 {Point{100, y_orig + y_orig/2 - 20}, "x/2"};
Text ts3 {Point{x_orig-100, 20}, "x*x"};
win.set_label("函数绘图：标记函数");
win.wait_for_button();
```

在本章的后续内容中，我们将省略将图形附加到窗口、标记窗口以及等待用户点击“Next”的重复代码。

然而，那张图片仍然不可接受。我们注意到 x/2 在 (0,0) 处与 x*x 相切，并且 one 在 (2,1) 处与 x/2 相交，但这太细微了；我们需要坐标轴来给读者一个毫不含糊的线索，让他们明白发生了什么：

![image](img/e0ceba017429f80f5cf63e81a1e7ef4f_555_0.png)

坐标轴代码是两个 `Axis` 对象（§15.4）：

```cpp
constexpr int xlength = xmax-40; // 使轴比窗口稍小
constexpr int ylength = ymax-40;

Axis x {Axis::Horizontal, Point{20, y_orig},
        xlength, xlength/x_scale, "one notch == 1"};
Axis y {Axis::Vertical, Point{x_orig, ylength+20},
        ylength, ylength/y_scale, "one notch == 1"};
```

使用 `xlength/x_scale` 作为刻度数量可确保一个刻度代表值 1, 2, 3 等。让坐标轴在**(0,0)**处相交是惯例。如果你更喜欢像显示数据那样沿左侧和底部边缘的惯例（参见§15.6），当然可以这样做。区分坐标轴和数据的另一种方法是使用颜色：

```cpp
x.set_color(Color::red);
y.set_color(Color::red);
```

我们得到

![image](img/e0ceba017429f80f5cf63e81a1e7ef4f_556_0.png)

这是可以接受的，尽管出于美学原因，我们可能希望顶部有一些空白空间，以匹配底部和两侧的空白。将 x 轴的标签再向左推一些可能也是个好主意。我们保留了这些瑕疵，以便我们可以提及它们——总是还有更多的美学细节可供我们处理。编程艺术的一部分在于知道何时停止，并将节省的时间用于其他更好的事情（如学习新技术或睡觉）。记住：“完美是好的敌人。”

## 15.3 Function

`Function` 图形接口类的定义如下：

```cpp
struct Function : Shape {
 // 函数参数不被存储
 Function(Fct f, double r1, double r2, Point orig,
          int count = 100, double xscale = 25, double yscale = 25);
};
```

Function 是一种 Shape，其构造函数生成大量线段并将它们存储在其 Shape 部分。这些线段近似函数 f 的值。f 的值在 [r1:r2] 范围内以等间距计算 count 次：

```cpp
Function::Function(Fct f, double r1, double r2, Point xy,
                   int count, double xscale, double yscale)
// 在 xy 处显示 (0,0)，使用 count 个线段绘制 [r1:r2] 范围内 f(x) 的图像
// x 坐标通过 xscale 缩放，y 坐标通过 yscale 缩放
{
    if (r2-r1 <= 0) error("bad graphing range");
    if (count <= 0) error("non-positive graphing count");
    double dist = (r2-r1)/count;
    double r = r1;
    for (int i = 0; i < count; ++i) {
        add(Point{xy.x + int(r*xscale), xy.y - int(f(r)*yscale)});
        r += dist;
    }
}
```

xscale 和 yscale 值分别用于缩放 x 坐标和 y 坐标。我们通常需要对值进行缩放，以使它们适当地适应窗口中的绘图区域。

注意，Function 对象不存储传递给其构造函数的值，因此我们无法稍后询问函数的原点在哪里、以不同的缩放比例重绘它等。它所做的只是存储点（在其 Shape 中）并在屏幕上绘制自己。如果我们想要构造后更改 Function 的灵活性，我们就必须存储我们希望更改的值（参见练习 2）。

我们用来表示函数参数的类型 Fct 是什么？它是标准库类型 std::function 的一个变体，它可以“记住”稍后要调用的函数。Fct 要求其参数是 double，返回类型也是 double。

### 15.3.1 默认参数

请注意 Function 构造函数的参数 xscale 和 yscale 在声明中是如何被赋予初始值的。这样的初始值称为默认参数，如果调用者没有提供值，则使用它们的值。例如：
