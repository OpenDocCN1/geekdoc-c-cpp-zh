
我们将`area`和`circumference`函数的声明放在类`Circle`的声明内部。它们被标记为`public`，因为我们希望它们对库的用户可用。这些声明看起来像普通的函数声明。请注意，它们根本不接收任何参数。

在我们尝试实现这些函数之前，让我们作为测试驱动开发者为它们编写测试。这将使我们能够演示如何在对象上调用函数。

```text
static void testAreaOfCircle() {
   Circle c;
   c.radius = 4;
   ASSERT_APPROX_EQUAL( c.area(), 16*PI, 0.01 );
}

static void testCircumferenceOfCircle() {
   Circle c;
   c.radius = 2;
   ASSERT_APPROX_EQUAL(c.circumference(),4*PI,0.01);
}
```

如上例所示，你使用点号来调用对象上的函数。例如，`c.area()`计算圆`c`的面积。

我们在特定的圆`c`上调用`area`函数，因此函数`area`应返回该特定圆`c`的面积。这就是你不需要向成员函数`area`传递半径的原因。

既然我们知道函数将如何被使用，让我们看看如何为这些函数提供定义。与C++函数通常的做法一样，我们在`.cpp`文件中编写定义。

```text
double Circle::area() {
   return PI*radius*radius;
}
```

```text
double Circle::circumference() {
   return 2*Pi*radius;
}
```

关于这些函数定义，有几点需要注意。

- (i) 当你定义类的成员函数时，必须始终在定义中指定类名。语法是：`CLASS_NAME::FUNCTION_NAME`。如果你忘记这样做，你会得到链接器错误，提示你忘记定义该函数。必须指定类名的原因是许多类可能具有同名的函数。例如，我们可能有一个类`Square`，它也有一个`area`函数。这就是你需要说明实际正在实现的是哪个类的方法的原因。

- (ii) `Circle`类的成员函数能够访问成员变量`radius`和全局变量`PI`。

### 8.3.1 在成员函数上使用 const

正如我们在第7.2节引入`const`关键字时提到的，如果你要使用`const`，必须在整个代码中一致地使用它。如果你决定使用`const`，那么如果一个成员函数不改变对象，你应该将其标记为`const`。你通过在声明和定义的末尾写`const`来实现这一点。

```cpp
class Circle {
public:
    double radius;
    double area() const;
    double circumference() const;
};

/**
 *  计算圆的面积
 */
double Circle::area() const {
    return PI*radius*radius;
}
```

在这个示例中，我们注意到测量圆的面积不会以任何方式改变圆。这就是我们在`area`函数的声明中添加了`const`的原因。

我们也在定义中添加了它，因为函数声明和定义中`const`和`&`的使用必须完全匹配。如果它们不完全匹配，你会得到链接器错误。尝试实验一下，看看如果你没有匹配的`const`语句会发生什么实际错误，这是值得的。

当你将一个指向`const Circle`的引用作为参数传递给函数时，编译器会坚持该函数不得修改该圆。这意味着你无法调用圆上的任何函数，除了那些标记为`const`的函数。这就是为什么，如果你打算使用`const`，你必须在每个不改变对象的函数上使用它。

## 8.4 一个金融示例

为了看到引入类所带来的好处，让我们通过一个涉及金融数学的更复杂的示例来进行讲解。首先我们定义一个名为`BlackScholesModel`的类。

```cpp
class BlackScholesModel {
public:
	double stockPrice;
	double volatility;
	double riskFreeRate;
	double date;
};
```

这个类中成员变量的选择是精心考量的。这个类只包含与模型相关的变量，而不包含与金融合约相关的变量。我们将在稍后的不同类中指定不同的期权合约。

我们将在后续章节中为这个类添加功能。例如，我们将添加函数来执行如模拟期权价格等操作。

请注意，我们将日期指定为`double`。我们将以自公元0年以来的年份来衡量日期。因此，2014年1月1日将表示为2014.0。在实际代码中你不会这样做，但我们不想在闰年以及九月有多少天这类问题上浪费精力。当你开始对真实的期权合约进行定价时，你需要更加小心。那时你会希望使用包含适当日期类的库。

我们现在定义一个单独的类用于期权合约。我们将创建一个类`CallOption`，它包含行权价和到期日，但不包含任何关于当前市场数据的信息。这种设计背后的理念是，我们可以使用相同的`BlackScholesModel`来对`CallOption`或`PutOption`进行定价。请注意，`CallOption`不会随着市场数据的变化而变化。这反映了现实情况：看涨期权*合约*不受市场变化的影响，尽管其价格可能会波动。

```cpp
class CallOption {
public:
	double strike;
	double maturity;

	double payoff( double stockAtMaturity ) const;
```

## 8.4.1 我们获得了什么？

这些好处与引入 `CartesianPoint` 和 `PolarPoint` 类时获得的好处类似，但现在它们显得更加显著。

- 编程更简单。如果我们有一个接受 5 个 `double` 参数的单个函数 `blackScholesPrice`，几乎不可能记住参数的正确顺序。

- 调试更简单。如果你有一个接受 5 个 `double` 参数的函数，几乎不可能发现有人是否不小心将参数的顺序搞错了。

- 一致性。如果我们使用相同的 `BlackScholesModel` 类对看跌期权、亚式期权、障碍期权等进行定价，我们将拥有一个更容易使用的库。

在后续章节中，我们将应用更高级的面向对象技术，这将带来更显著的优势。

## 8.5 关于编写类的建议

在编写类时，关于类的名称以及将其定义在哪个文件中等事务，你有许多选择。拥有一些约定是好的。在本书中，我们选择遵循以下指南。

1. 只要可能，不要把类声明放在头文件中，而应放在 `cpp` 文件中。这源于一个普遍原则，即你应该尽可能隐藏信息。

2. 如果你决定将类放在头文件中，每个头文件只定义一个类。

3. 将该类的命名与头文件相同。

4. 给类使用名词作为名称：例如 `CartesianPoint` 或 `BlackScholesModel`。

5. 类名的首字母使用大写。

文件 `BlackScholesModel.h` 和 `CallOption.h` 展示了这些约定。

文件 `geometry.h` 违反了这些约定，但这仅仅是因为我们要避免用许多与金融数学无关的文件来杂乱项目。如果我们真的在编写一个几何库，为了可读性，我们会将所有点类放入各自的头文件中。

需要考虑的第二个问题是 `const` 关键字。在本章中，我们尝试一致地使用 `const` 关键字。然而，`const` 关键字是 C++ 中的可选特性。你可以选择使用它，如果希望编译器保证你永远不会在不小心的情况下修改对象，但即使你完全不用 `const`，你的代码也能工作。

这意味着你可以为你的项目做出一个软件架构决策：是使用 `const` 还是不使用？这是一个针对整个项目的决策，因为事实证明，如果你想使用 `const` 关键字，你真的需要在所有地方使用它。这是因为如果某人传递给你一个 `const` 引用，你只能将其传递给本身声明为接受 `const` 引用的函数。

在实践中，这意味着你无法选择是否使用 `const`。你需要询问你的老板是否希望使用它。

即使你自己不喜欢 `const` 关键字，如果你正在编写一个库，如果库用户希望使用 `const` 关键字，你就需要使用该关键字。

在本书中，我们将使用 `const`，以便你可以理解所提出的问题，但你可能更愿意在自己的代码中避免使用它。

## 8.6 封装

现在让我们尝试更详细地理解 `public` 关键字。为此，让我们编写一个面向对象版本的饼图代码。我们从一个名为 `PieChart` 的类声明开始。

```cpp
class PieChart {
public:
    void setTitle( const std::string& title );
    void addEntry( const std::string& label,
                    double value );
    void writeAsHTML( std::ostream& out ) const;
    void writeAsHTML( const std::string& file ) const;
private:
    std::string title;
    std::vector<std::string> labels;
    std::vector<double> values;
};
```

遵循我们的约定，你可以在 `PieChart.h` 中找到这个类。

我们现在将数据变量标记为 `private`。这意味着只有 `PieChart` 的成员函数可以看到这些变量。

唯一修改标题的成员函数是 `setTitle`。唯一修改标签列表和数据点列表的函数是 `addEntry`。以下是它们的定义：

```cpp
void PieChart::setTitle( const std::string& t ) {
    title = t;
}

void PieChart::addEntry( const std::string& label,
                          double value ) {
    labels.push_back( label );
    values.push_back( value );
}
```

有趣的一点是，现在 `labels` 和 `values` 永远不可能包含不同数量的元素。这是因为唯一修改它们的代码是 `addEntry`，而该函数维护了一个保证，即两个向量始终具有相同的长度。我们知道项目中其他地方不可能有任何代码破坏这一保证，因为这些变量是 `private` 的。因为我们使用了 `private` 关键字，我们只需要检查成员函数是否行为良好，就可以确定 `labels` 和 `values` 具有相同数量的元素。

将所有成员变量设为 `private` 被认为是一种良好的编程风格。这样做允许你保证对象始终保持一致的状态。此外，它还允许你将来改变关于实现细节（即数据存储方式）的想法，而不会以任何方式影响你类的用户。

总而言之，`private` 关键字允许你执行比仅仅选择在头文件中放什么更高级的信息隐藏。

不把类放在头文件中比将事物设为 `private` 提供了更多的信息隐藏，所以这应该始终是你的首选。然而，如果你必须将类提供给库的用户，你应该尽量将其所有数据以及尽可能多的成员函数设为 `private`。

我们给 `BlackScholesModel` 和 `CallOption` 公有数据成员仅仅是为了简洁。我们想在解释 `private` 数据之前演示公有的使用。在实践中，通过修改这些类可以改善库。

使用 `private` 关键字隐藏数据的思想通常称为封装。封装这个词实际上指两件事：

- 将相关项目捆绑到一个单一对象中；

- 防止直接操纵对象的内部数据。

封装在现实世界设计中以及面向对象软件设计中都很常见。例如，考虑汽车的设计。

在汽车中，所有灯光控制都放在仪表板上，并且与窗户和座椅的控制明显分离。汽车控制中功能的这种分组对应于软件设计中功能分组到不同的类中。

此外，你可以通过标准功能（左转、右转等）控制汽车，但汽车的内部运作对用户完全隐藏（它们被保留在引擎盖下）。这对应于软件设计原则，即拥有少量提供给用户的公有函数，但将大多数细节保留为 `private`。

由于使用了封装，汽车更容易使用。你可以驾驶汽车而不必是经过训练的机械师，这是一件好事。正如这些设计原则使汽车更容易使用一样，同样的原则使面向对象程序中的对象易于使用。

为了进一步说明这一点，考虑 `vector<double>` 类如何存储其数据的问题，鉴于它不能自己使用 `vector<double>`。你不知道这是如何做到的，而且很合理的是你大概也不太关心。你不需要知道这一点，不必思考这件事让你的生活变得更轻松。

C++ 库的设计者通过使 `vector` 的内部数据变为 `private` 来尝试让你的生活更轻松。你也应该以同样的方式帮助库的用户。

## 8.6.1 实现 PieChart

你可以在 `PieChart.cpp` 中找到 `PieChart` 类的完整实现。它只是对我们在第 7.6 节中编写的非面向对象代码进行重组。你可以将我们新的 `PieChart` 类看作是对现有代码的一个面向对象封装，使其更易于使用。

## 8.6.2 使用 PieChart

面向对象编程的一个核心理念是，人类发现以下代码易于理解：

```cpp
static void testPieChartClass() {
    // just checks that the class compiles etc.
    PieChart pieChart;
    pieChart.addEntry("Mushrooms",200);
    pieChart.addEntry("Salami",100);
    pieChart.addEntry("Spinach",150);
    pieChart.setTitle("Pizza Toppings");

    pieChart.writeAsHTML ( "PizzaPie.html" );
}
```

这真正概括了面向对象的一个关键点。面向对象软件应当让我们的库的用户生活更轻松。

### 练习

- 8.6.1 编写一个类 `PutOption`，使其行为类似于 `CallOption`。确保你编写了适当的测试，并遵循文件命名约定。

- 8.6.2 编写一个类 `LineChart`，使其允许你创建折线图。添加一个设置图表标题的功能。

- 8.6.3 向 `CartesianPoint` 类添加一个 `distanceTo` 函数。它应该接受一个参数，即另一个 `CartesianPoint`，并计算这两个点之间的距离。以下是一个合适的测试函数：

```cpp
static void testDistanceTo() {
    CartesianPoint p1;
    p1.x = 1;
    p1.y = 1;
    CartesianPoint p2;
    p2.x = 4;
    p2.y = 5;
    double d = p1.distanceTo( p2 );
    ASSERT_APPROX_EQUAL( d, 5.0, 0.0001);
}
```

你在声明中使用了两次 `const` 关键字，在定义中也使用了两次吗？

- 8.6.4 编写一个普通的函数 `perimeter`，它接受三个 `CartesianPoint` 的 `const` 引用，并计算所形成的三角形的周长。`perimeter` 函数应该调用 `distanceTo`。使用 3, 4, 5 三角形测试你的 `perimeter` 函数。

如果你从 `distanceTo` 的定义中移除 `const` 关键字中的任意一个，但在 `perimeter` 的定义中保留它们，会发生什么？解释为什么“如果你使用 `const` 关键字，就必须到处都使用它”。

## 8.7 构造函数

如果你在 C++ 中创建一个 `double` 类型的变量但没有设置其值，C++ 并不保证分配什么值。在实践中，计算机只会获取一些空闲内存，并使用那里碰巧存在的任何值。

例如，下面的程序是有效的 C++，但无法预先确定它会输出什么。

```cpp
int main() {
  double d;
  cout << "What is the value of d?\n";
  cout << d;
  return 0;
}
```

之前这还不是一个问题，因为我们一直在关注警告信息，尽管这是技术上有效的 C++ 代码，但它肯定会引发编译器警告。

出于类似原因，以下代码也会导致编译器警告。

```cpp
class Point {
public:
  double x;
  double y;
};
```

```cpp
int main() {
    Point p;
    cout << "What is the value of x?\n";
    cout << p.x;
    return 0;
}
```

如果所有的 `double` 值和所有的 `int` 值默认都为 0，C++ 的使用将会稍微容易一些。我们无法修改 C++ 使事情变得更容易，但我们可以通过为类提供构造函数来使我们的类更易于使用。构造函数执行对象的初始化，使其处于合理状态。

我们已经使用过构造函数。例如，为了构造一个长度为 100 且初始化为零的向量，我们知道应该这样写：

```cpp
vector<double> v(100,0.0);
```

同样地，为了构造一个包含文本“Some text”的字符串，我们知道应该这样写：

```cpp
string s("Some text");
```

大多数类更进一步，拥有一个默认构造函数，使对象处于合理的默认状态。例如，为了创建一个空向量，只需写：

```cpp
vector<double> v;
```

默认构造函数会被自动调用。同样地，为了创建一个空字符串，写：

```cpp
string s;
```

当你编写类时，几乎总是应该给它一个默认构造函数，以便人们能够正确使用它。你可能还想提供更具专用性的构造函数，以便将对象初始化为特定状态。

## 8.7.1 编写默认构造函数
