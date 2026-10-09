

8.6.4. 编写一个普通的函数 `perimeter`，它接受三个 `const` 引用的 CartesianPoints 作为参数，并计算由此产生的三角形的周长。`perimeter` 函数应调用 `distanceTo`。使用 3, 4, 5 三角形测试你的 `perimeter` 函数。

如果你从 `distanceTo` 的定义中移除任一个 `const` 关键字，但在 `perimeter` 的定义中保留它们，会发生什么？请解释为什么“如果你在任何地方使用 `const` 关键字，你就必须在所有地方使用它”。

## 8.7 构造函数

如果在 C++ 中创建一个 `double` 类型的变量但自己未设置其值，C++ 不会保证该变量会被赋予什么值。在实践中，计算机只会获取一些空闲内存，并使用其中碰巧存在的任何值。

例如，下面的程序是有效的 C++，但不可能提前预知它会打印什么内容。

```cpp
int main() {
	double d;
	cout << "What is the value of d?\n";
	cout << d;
	return 0;
}
```

由于我们一直注意警告信息，这尚未成为一个问题，尽管这是技术上有效的 C++ 代码，但它肯定会触发编译器警告。

由于类似的原因，以下代码也会导致编译器警告。

```cpp
class Point {
public:
	double x;
	double y;
};

int main() {
    Point p;
    cout << "What is the value of x?\n";
    cout << p.x;
    return 0;
}
```

如果所有 double 值和所有 int 值默认都为 0，C++ 将更易于使用。我们无法修改 C++ 以使事情更容易，但我们可以通过为类提供构造函数来使我们的类更易于使用。构造函数执行对象的初始化，使其处于合理状态。

我们已经使用过构造函数。例如，要构建一个长度为 100 且初始化为零的向量，我们知道应该编写：

```cpp
vector<double> v(100,0.0);
```

类似地，要构建一个包含 Some text 字符的字符串，我们知道应编写：

```cpp
string s("Some text");
```

大多数类更进一步，拥有一个默认构造函数，将对象初始化为合理的默认状态。例如，要创建一个空向量，只需简单地编写：

```cpp
vector<double> v;
```

默认构造函数会被自动调用。类似地，要创建一个空字符串，人们会编写：

```cpp
string s;
```

当你编写一个类时，几乎总是应该给它一个默认构造函数，以便人们能够正确使用它。你可能还想提供更专业化的构造函数来将对象初始化为特定状态。

### 8.7.1 编写默认构造函数

让我们编写一个名为 Point 的类，它旨在完全像我们的 CartesianPoint 示例那样工作，但现在拥有一个构造函数。

```cpp
class Point {
public:
    Point(); // 声明默认构造函数
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

在类声明中，我们在第 3 行有声明 `Point();`。这声明了构造函数。

构造函数声明看起来像函数声明，除了：

- (i) 没有返回类型；
- (ii) 使用类名代替函数名。

类似地，构造函数定义看起来像函数定义，具有相同的差异。在上面的示例中，构造函数定义从第 8 行开始。

在我们的示例中，构造函数看起来像一个不接收参数的函数。正如我们将看到的，构造函数可以接收参数。默认构造函数只是一个不接收参数的构造函数。

你可以将构造函数视为一个函数，它在任何人被允许查看对象之前自动被调用。从技术上讲，它实际上不是一个函数，因为它*只能*在对象被初始化时调用，并且它没有返回值。

在构造函数定义内部，你应该将所有 `int`、`double` 等字段设置为合理的默认值。更一般地说，在任何人看到对象之前，你应确保对象处于一致状态，并执行达成此目的所需的任何处理。

### 8.7.2 另一种更优越的语法

这里是我们可以编写 `Point` 构造函数的另一种方式：

```cpp
class Point {
public:
    Point(); // 声明默认构造函数
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

在 Point 构造函数的定义中，你可以看到一系列语句：

```cpp
x(0.0),
y(0.0)
```

这被称为初始化列表。这调用了 x 和 y 的构造函数以初始化数据。这与我们之前使用 `=` 语句初始化变量的代码略有不同。

带有初始化列表的构造函数的一般语法是：

```cpp
CLASS_NAME::CLASS_NAME( PARAMETER_LIST ) :
    INITIALISATION_LIST {
      ... NORMAL CODE ...
}
```

注意初始化列表前面的冒号。

经验丰富的 C++ 程序员更喜欢使用初始化列表，因为它稍微快一点。这是因为调用默认构造函数然后执行赋值会比第一次就使用正确的值更慢。

此外，一旦你熟悉了这种语法，它的可读性更好，因为很明显没有任何复杂的地方。所有正在发生的事情只是数据被初始化。这意味着你可以猜测，如果花括号之间有一些代码，它会相对有趣。

## 8.8 带参数的构造函数

编写接收参数的构造函数很直接。以下是如何在 CallOption 类中添加一个接收 *strike* 和 *maturity* 作为参数的构造函数的方法。

```cpp
class CallOption {
public:
    double strike;  
    double maturity;  
    CallOption(); // 默认构造函数
    CallOption(double strike, double maturity); // 替代
};

// 默认构造函数实现
CallOption::CallOption() :  
   strike(0.0),
   maturity(0.0) {
}

// 替代构造函数实现
CallOption::CallOption(
      double s,
      double m ) :  
   strike(s),
   maturity(m) {  
}
```

要创建一个 strike 为 100 且 maturity 为 2.0 的期权，人们随后会编写

```cpp
CallOption myOption( 100, 2.0 );
```

这似乎是一个非常方便的系统，但这可能不是一个很好的设计。原因在于，通过引入类，我们消除了调用函数时记住参数顺序的问题。通过拥有一个具有多个参数的构造函数，我们重新引入了这个问题！

这并不意味着带参数的构造函数总是坏的，只是你不应该过度使用它们。当然，能够构建给定大小和默认值的向量是构造函数的良好用途。

带参数构造函数有一个奇怪的技巧，你应该尝试记住。考虑类 string。它有一个接收原始文本数据的构造函数：

```cpp
string s("Some raw text");
```

C++ 使用这个构造函数自动将原始文本数据转换为字符串，而你无需考虑。例如，代码：

```cpp
plot("myPlot.txt", xVec, yVec );
```

将起作用，尽管 plot 的第一个参数声明为 `const string&` 而不是 `char*`。

一般来说，如果你的类有一个接收单个参数进行构造的构造函数，C++ 将执行类似的自动转换。虽然这对于 string 数据类型非常好，但通常它会导致非常不自然的代码。例如，假设你在 BlackScholesModel 中添加了一个构造函数，其中你只提供股票价格：

