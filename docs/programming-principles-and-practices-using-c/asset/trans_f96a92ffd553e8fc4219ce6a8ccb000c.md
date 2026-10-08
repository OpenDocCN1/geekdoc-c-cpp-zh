
## 5. 人口图表

坐标轴在**Point(xoffset,ymax-yoffset)**处相交，该点表示**(1960,0)**。请注意刻度是如何放置以反映数据的。在 $y$ 轴上，我们有十个刻度，每个刻度代表人口的10%。在 $x$ 轴上，每个刻度代表十年，并且刻度的确切数量是根据**base_year**和**end_year**计算得出的，因此如果我们改变该范围，坐标轴会自动重新计算。这是避免在代码中使用“魔法常量”的一个好处。$x$ 轴上的标签违反了该规则：它只是反复调整标签字符串直到数字位于刻度下方的正确位置的结果。为了做得更好，我们需要查看一组用于各个“刻度”的独立标签。

请注意标签字符串的奇怪格式。我们使用了两个相邻的字符串字面量：

```cpp
"year 1960 1970 1980 1990" "2000 2010 2020 2030 2040"
```

相邻的字符串字面量会被编译器连接，因此这等价于

```cpp
"year 1960 1970 1980 1990 2000 2010 2020 2030 2040"
```

对于布局较长的字符串字面量以使代码更具可读性，这是一个有用的“技巧”。

**current_year** 是一条垂直线，用于将硬数据与预测数据分隔开。请注意**xs**和**ys**是如何被用来放置和缩放这条线，使其恰到好处。

给定坐标轴，我们可以继续进行数据处理。我们定义三个**Open_polylines** 并在读取循环中填充它们：

```cpp
Open_polyline children;
Open_polyline adults;
Open_polyline aged;
```

```cpp
for (Distribution d; ifs>>d; ) {
  if (d.year<base_year||end_year<d.year) error("year out of range");
  if (d.young+d.middle+d.old != 100)
      error("percentages don’t add up");
  const int x = xs(d.year);
  children.add(Point(x,ys(d.young)));
  adults.add(Point(x,ys(d.middle)));
  aged.add(Point(x,ys(d.old)));
}
```

使用**xs**和**ys**使得数据的缩放和放置变得微不足道。“小型类”，例如 *Scale*，对于简化符号和避免不必要的重复——从而提高可读性和增加正确性的可能性——可能极其重要。

为了使图表更具可读性，我们为每条线添加标签并应用颜色：

```cpp
Text children_label {Point{20,children.point(0).y},"age 0-14"};
children.set_color(Color::red);
children_label.set_color(Color::red);

Text adults_label {Point{20,adults.point(0).y},"age 15-64"};
adults.set_color(Color::blue);
adults_label.set_color(Color::blue);

Text aged_label {Point{20,aged.point(0).y},"age 65+"};
aged.set_color(Color::dark_green);
aged_label.set_color(Color::dark_green);
```

最后，我们需要将各种*Shapes* 附加到*Window*上并启动 GUI 系统（§14.2.3）：

```cpp
win.attach(children);
win.attach(adults);
win.attach(aged);

win.attach(children_label);
win.attach(adults_label);
win.attach(aged_label);

win.attach(x);
win.attach(y);
win.attach(current_year);

gui_main();
```

所有代码都可以放在 *main()* 内部，但我们更喜欢将辅助类 *Scale* 和 *Distribution* 放在外部，并与 *Distribution* 的输入运算符放在一起。

如果你忘记了我们在制作什么，这里再次展示输出：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_578_0.png)

### 练习

**函数绘图练习：**

1. 创建一个空的 600x600 **Window**，标签为“Function graphs”。
2. 注意，你需要根据课程网站上关于“FLTK 安装”的备注中指定的属性创建一个项目。
3. 你需要将 **Graph.cpp** 和 **Window.cpp** 移动到项目中。
4. 添加一条 *x* 轴和一条 *y* 轴，长度均为 400，标签为“1 = = 20 pixels”，每 20 像素一个刻度。坐标轴应在 (300,300) 处相交。
5. 将两条坐标轴都设置为红色。

在以下内容中，为每个要绘制的函数使用单独的 **Shape**：

1. 在范围 $[-10,11]$ 内，使用 400 个点且无缩放（在窗口中），在 $(300,300)$ 处对应 $(0,0)$ 的位置绘制函数 `double one(double x) { return 1; }`。
2. 将其改为使用 *x* 缩放 20 和 *y* 缩放 20。
3. 从现在开始，对所有图表使用该范围、缩放等。
4. 向窗口中添加 `double slope(double x) { return x/2; }`。
5. 使用位于其左下端点正上方的点的 **Text** "/x/2/" 来标记斜率。
6. 向窗口中添加 `double square(double x) { return x*x; }`。
7. 向窗口添加一个余弦函数（不要编写新的函数）。
8. 将余弦函数设置为蓝色。
9. 编写一个函数 `sloping_cos()`，将余弦函数加到 `slope()` 上（如上定义），并将其添加到窗口。

**类定义练习：**

1. 定义一个 `struct Person`，包含一个 `string` 名称和一个 `int` 年龄。
2. 定义一个类型为 `Person` 的变量，用 "Goofy" 和 63 进行初始化，并将其写入屏幕（`cout`）。
3. 为 `Person` 定义输入（`>>`）和输出（`<<`）运算符；从键盘（`cin`）读取一个 `Person` 并将其输出到屏幕（`cout`）。
4. 为 `Person` 提供初始化 `name` 和 `age` 的构造函数。
5. 将 `Person` 的表示设为私有，并提供 `const` 成员函数 `name()` 和 `age()` 来读取姓名和年龄。
6. 修改 `>>` 和 `<<` 以适配重新定义的 `Person`。
7. 修改构造函数以检查 `age` 在 [0;150) 范围内，且 `name` 不包含任何 `;: '" \ [ ] & ^ % $ # @ !` 字符。在发生错误时使用 `error()`。进行测试。
8. 从输入（`cin`）读取一系列 `Persons` 到 `vector<Person>`；将它们再次输出到屏幕（`cout`）。使用正确和错误的输入进行测试。
9. 更改 `Person` 的表示，将 `name` 改为 `first_name` 和 `second_name`。未提供名字和姓氏视为错误。确保同时修复 `>>` 和 `<<`。进行测试。

### 复习

1. 什么是单参数函数？
2. 何时使用（连续）线来表示数据？何时使用（离散）点？
3. 哪个函数（数学公式）定义了斜率？
4. 什么是抛物线？
5. 如何制作 x 轴？如何制作 y 轴？
6. 什么是默认参数，何时使用它？
7. 如何将函数相加？
8. 如何为绘制的函数上色和添加标签？
9. 当我们说一个级数近似于一个函数时，意味着什么？
10. 为什么在编写绘制图表的代码之前，要草图布局图表？
11. 如何缩放图表以便输入适合？
12. 如何在没有试错的情况下缩放输入？
13. 为什么要格式化输入，而不是让文件仅包含“数字”？
14. 如何规划图表的总体布局？如何在代码中反映该布局？

### 术语

- 近似
- 默认参数
- 函数
- lambda
- 缩放
- 屏幕布局

### 习题

1. 这里有另一种定义阶乘函数的方式：
   ```cpp
   int fac(int n) { return n>1 ? n*fac(n-1) : 1; } // factorial n!
   ```
   它将通过首先决定由于**4>1**，**fac(4)** 必须是**4\*fac(3)**，这显然是**4\*3\*fac(2)**，进而又是**4\*3\*2\*fac(1)**，即**4\*3\*2\*1**来执行 **fac(4)**。尝试理解它是如何工作的。调用自身的函数被称为*递归*。§15.5 中的替代实现被称为*迭代*，因为它遍历数值（使用 **while**）。通过计算 $0, 1, 2, 3, 4$ 直到包括 20 的阶乘，验证递归的 **fac()** 是否有效，并给出与迭代 **fac()** 相同的结果。你更喜欢哪种 **fac()** 的实现，为什么？
2. 定义一个类 **Fct**，它仅类似于 **Function**，但它存储其构造函数参数。为 **Fct** 提供“重置”操作，以便你可以重复使用它，针对不同范围、不同函数等。
3. 修改上一个练习中的 **Fct**，使其接受一个额外参数来控制精度或其他方面。为该参数类型使用模板参数以增加灵活性。
4. 在单个图表上绘制正弦（**sin()**）、余弦（**cos()**）、它们的和（**sin(x)+cos(x)**）以及它们平方的和（**sin(x)\*sin(x)+cos(x)\*cos(x)**）。请提供坐标轴和标签。
5. “动画化”（如 §15.5 中所述）级数 **1−1/3+1/5−1/7+1/9−1/11+ …**。它被称为莱布尼茨级数，收敛于 pi/4。
6. 设计和实现一个条形图类。其基本数据是一个包含 $\mathcal{N}$ 个值的 **vector<double>**，每个值应由一个表示该值的矩形“条”表示，其高度代表数值。
7. 完善条形图类，允许为图表本身及其单独条形添加标签。允许使用颜色。
8. 这里有一组以厘米为单位的身高以及该身高组的人数（四舍五入到最近的 5cm）：(170,7), (175,9), (180,23), (185,17), (190,6), (195,1)。你会如何绘制该数据

