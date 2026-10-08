
## 8.6.1 实现 PieChart

你可以在 PieChart.cpp 中找到 PieChart 类的完整实现。它只是对我们在第 7.6 节中编写的非面向对象代码进行重组。你可以将我们新的 PieChart 类看作是对现有代码的一个面向对象封装，使其更易于使用。

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

- 8.6.1 编写一个类 PutOption，使其行为类似于 CallOption。确保你编写了适当的测试，并遵循文件命名约定。
- 8.6.2 编写一个类 LineChart，使其允许你创建折线图。添加一个设置图表标题的功能。
- 8.6.3 向 CartesianPoint 类添加一个 distanceTo 函数。它应该接受一个参数，即另一个 CartesianPoint，并计算这两个点之间的距离。以下是一个合适的测试函数：

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

你在声明中使用了两次 **const** 关键字，在定义中也使用了两次吗？

- 8.6.4 编写一个普通的函数 **perimeter**，它接受三个 CartesianPoint 的 **const** 引用，并计算所形成的三角形的周长。**perimeter** 函数应该调用 distanceTo。使用 3, 4, 5 三角形测试你的 **perimeter** 函数。

如果你从 distanceTo 的定义中移除 **const** 关键字中的任意一个，但在 **perimeter** 的定义中保留它们，会发生什么？解释为什么“如果你使用 **const** 关键字，就必须到处都使用它”。

## 8.7 构造函数

如果你在 C++ 中创建一个 double 类型的变量但没有设置其值，C++ 并不保证分配什么值。在实践中，计算机只会获取一些空闲内存，并使用那里碰巧存在的任何值。

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

如果所有的 double 值和所有的 int 值默认都为 0，C++ 的使用将会稍微容易一些。我们无法修改 C++ 使事情变得更容易，但我们可以通过为类提供构造函数来使我们的类更易于使用。构造函数执行对象的初始化，使其处于合理状态。

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

让我们编写一个名为 Point 的类，它旨在完全像我们的 CartesianPoint 示例那样工作，但现在拥有了构造函数。

```cpp
class Point {
public:
    Point(); // declare default constructor
    double x;
    double y;
};

Point::Point() {
    x=0.0;
    y=0.0;
}

int main() {
    Point p;
    cout << "What is the value of x?\n";
    cout << p.x;
    return 0;
}
```

在类声明中，我们现在在第 3 行有了声明 Point();。这声明了构造函数。

构造函数声明看起来像函数声明，除了：

- (i) 没有返回类型；
- (ii) 在函数名称的位置，你有类的名称。

同样地，构造函数定义看起来像函数定义，具有相同的差异。在上面的示例中，构造函数定义从第 8 行开始。

在我们的示例中，构造函数看起来像一个不接受参数的函数。正如我们将看到的，构造函数可以接受参数。默认构造函数只是一个不接受参数的构造函数。

你可以将构造函数视为一个在任何人被允许查看对象之前自动调用的函数。从技术上讲，它实际上不是一个函数，因为它*只能*在对象初始化时被调用，并且因为它没有返回值。

在构造函数的定义内部，你应该将所有 int、double 等字段设置为合理的默认值。更一般地说，你应该确保在任何人看到对象之前，对象处于一致的状态，并执行达到此状态所需的任何处理。

## 8.7.2 一种替代且更优的语法

这里是另一种我们可以编写 *Point* 构造函数的方法：

```cpp
class Point {
public:
   Point(); // declare default constructor
   double x;
   double y;
};

Point::Point() :
    x(0.0),
    y(0.0) {
}

int main() {
    Point p;
    cout << "What is the value of x?\n";
    cout << p.x;
    return 0;
}
```

在 Point 构造函数的定义中，你可以看到一个语句列表：

```cpp
x(0.0),
y(0.0)
```

这被称为初始化列表。这调用了 x 和 y 的构造函数以初始化数据。这与我们之前使用 = 语句初始化变量的代码略有不同。

带初始化列表的构造函数的通用语法是：

```cpp
CLASS_NAME::CLASS_NAME( PARAMETER_LIST) :
INITIALISATION_LIST {
... NORMAL CODE ...
}
```

注意初始化列表前的冒号。

经验丰富的 C++ 程序员更喜欢初始化列表，因为它稍微快一点。这是因为调用默认构造函数然后执行赋值操作比第一次就使用正确的值要慢。

此外，一旦你熟悉了这种语法，它更可读，因为很明显没有任何花哨的操作。所做的只是数据正在被初始化。这意味着你可以猜到，如果大括号之间有一些代码，它将相对有趣。

## 8.8 带参数的构造函数

编写接受参数的构造函数很简单。以下是如何向 CallOption 类添加一个接受行权价（strike）和到期日（maturity）作为参数的构造函数。

```cpp
class CallOption {
public:
    double strike;
    double maturity;
    CallOption(); // default constructor
    CallOption(double strike, double maturity);//alternative
};

// default constructor implementation
CallOption::CallOption():
    strike(0.0),
    maturity(0.0){
}

// alternative constructor implementation
CallOption::CallOption(
    double s,
    double m ):
    strike(s),
    maturity(m){
}
```

为了创建一个行权价为 100 且到期日为 2.0 的期权，我们可以这样写

```cpp
CallOption myOption( 100, 2.0 );
```

这似乎是一个非常方便的系统，但这可能不是一个很好的设计。原因是通过引入类，我们消除了在调用函数时记住参数顺序的问题。通过拥有一个带多个参数的构造函数，我们重新引入了这个问题！

这并不意味着带参数的构造函数总是坏的，只是你不应该过度使用它们。当然，能够构造给定大小和默认值的 `vector` *是*构造函数的一个良好用途。

有一个关于带参数构造函数的奇怪技巧你应该试着记住。考虑类 `string`。它有一个接受原始文本数据的构造函数：

```cpp
string s("Some raw text");
```

C++ 使用这个构造函数自动将原始文本数据转换为 `string`，而无需你思考。例如，代码：

```cpp
plot( "myPlot.txt", xVec, yVec );
```

即使 plot 的第一个参数被声明为 `const string&` 而不是 `char*`，它也能正常工作。

一般来说，如果你的类有一个接受单一参数构造函数的类，C++ 将执行类似的自动转换。虽然这对于 `string` 数据类型非常好，但通常会导致非常不自然的代码。

例如，假设你在 `BlackScholesModel` 中添加了构造函数，其中你只提供股票价格：

