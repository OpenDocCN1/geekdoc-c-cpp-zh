
```cpp
class IsDivisibleBy {
  int divisor;
  public:
    // 构造函数存储参数作为除数
    IsDivisibleBy(int d) { divisor = d; }

    // 检查 x 是否能被 divisor 整除
    bool operator()(int x) {
      return x % divisor == 0;
    }
};
```

给定这样一个类，你可以创建一个函数对象 `IsDivisible(7)` 来测试整数的被整除性。请注意，如果 `d` 和 `x` 是整数，表达式 `IsDivisible(d)(x)` 正在带参数 `x` 调用该函数对象。在最后一个表达式中，`d` 是构造函数参数，而 `x` 是函数对象的参数。

以下代码要求用户输入一个整数，然后从 `vec` 中移除被该整数整除的元素：

```cpp
int d;
cout << "Enter a divisor: ";
cin >> d;
auto rem_start = remove_if(begin(vec), end(vec), IsDivisibleBy(d));
vec.erase(rem_start, end(vec));
```

### 返回 void 的函数对象

对象的对象的类型可以是 `void`。接受单个参数且返回类型为 `void` 的函数称为一元函数。以下是一个可以用于创建一元函数对象的类。该函数对象打印其参数的平方。

```cpp
class PrintSquare {
  public:
    void operator()(int a) { cout << a * a << " "; }
};
```

有时我们想要对数组或向量的每个元素调用一元函数。`<algorithm>` 头文件中声明的 `for_each` 函数正是此用的。它将元素范围的起始和结束位置以及一元函数作为参数，并将函数应用到范围内的每个元素。程序 11-17 演示了使用该函数打印向量中存储数字的平方。

### 程序 11-17

```cpp
// 此程序演示了
// for_each 算法函数的使用。
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

class PrintSquare
{
public:
void operator()(int a) { cout << a * a << " "; }
};

int main() {
    vector<int> vec = {1, 2, 3, 4, 5, 6};

    // 打印数组中每个元素的平方
    for_each(begin(vec), end(vec), PrintSquare());

    cout << endl;
    return 0;
}
```

### 程序输出

1 4 16 25 36

### C++ 库中的函数类

函数对象非常有用，以至于 C++ 库定义了许多可以实例化以创建函数对象的类，你可以在程序中使用它们。使用这些类需要包含 `<functional>` 头文件。表 11-2 列出了那些可以用于比较对象的类，但你可以在网上找到更多信息。

#### 表 11-2 函数对象

| 函数对象 | 说明 |

| :--- | :--- |

| `less<T>` | 如果 `a < b`，则 `less<T>(a, b)` 为真 |

| `less_equal<T>` | 如果 `a <= b`，则 `less_equal(a, b)` 为真 |

| `greater<T>` | 如果 `a > b`，则 `greater<T>(a, b)` 为真 |

| `greater_equal<T>` | 如果 `a >= b`，则 `greater_equal(a, b)` 为真 |

### Lambda 表达式

Lambda 表达式是从一个唯一成员为函数运算符的类创建函数对象的紧凑方式。Lambda 表达式消除了类的声明，使用精简的表示法表达函数运算符。例如，计算两个整数和的 Lambda 表达式是：

```cpp
[](int a, int b) { return a + b; }
```

判断整数是否为偶数的 Lambda 表达式是：

```cpp
[](int a) { return a % 2 == 0; }
```

另一个例子，接受整数输入并产生其平方的 Lambda 表达式如下：

```cpp
[](int a) { cout << a * a << " "; }
```

上面的 Lambda 表达式基本上是函数定义，函数的名称和返回类型被空括号 `[]` 替换。更一般，Lambda 表达式的形式为

```cpp
[capture](parameter list) { function body }
```

捕获类是 Lambda 表达式范围内可以访问的变量列表。这类似于函数列出它访问的所有局部变量。我们使用的 Lambda 不使用捕获列表，因此我们并不考虑这个概念。

Lambda 表达式通过在其后面直接传递参数列表来调用。例如，以下代码片段打印 7，即变量 `x` 和 `y` 的和：

```cpp
int x = 2;
int y = 5;
cout << [](int a, int b){return a + b;}(x, y);
```

以下代码片段以程序 11-18 的方式对数组进行降序。然而，它使用 Lambda 表达式代替了 `sort` 函数的第三参数。

```cpp
double d_values[] = {12.7, 45.9, 6.9};
// 降序数组
sort(begin(d_values), end(d_values),
[](auto a, auto b){return a > b});

// 打印数组
for (auto x : d_values)
{
cout << x << " ";
}
```

由于 Lambda 表达式是函数对象，你可以将 Lambda 赋值给相应类型的变量，并通过变量名调用它。例如，你可以给 Lambda 表达式分配一个名称：

```cpp
auto compare = [](auto a, auto b){return a > b};
```

# 804 第11章 关于类和面向对象编程的更多

这样做可以将代码拆分为更小的部分并使其更具可读性。以下是将上述代码片段重写为引用一个值为 lambda 表达式的变量：

```cpp
double d_values[] = {12.7, 45.9, 6.9 };
// Lambda 表达式
auto compare = [](auto a, auto b) { return a > b };
// 降序排序数组
sort(begin(d_values), end(d_values), compare);
// 打印数组
for (auto x : d_values)
{
    cout << x << " ";
}
```

## 检查点

- 11.31 什么是右值引用？
- 11.32 右值引用的声明如何与左值引用区分开？
- 11.33 移动赋值和拷贝赋值之间的区别是什么？
- 11.34 什么是函数对象？
- 11.35 在类用于创建函数对象之前，必须在类中重载哪个运算符？
- 11.36 什么是 lambda 表达式？

# 类型转换运算符

**概念：** 可以编写特殊的运算符函数将类对象转换为任何其他类型。

正如你已经所看到的，运算符函数允许类工作得更像内置数据类型。运算符函数可以赋予类的另一个功能是自动类型转换。

数据转换在内置数据类型中是在“后台”发生的。例如，程序使用以下变量：

```cpp
int i;
double d;
```

以下语句自动将 `i` 中的值转换为 double 并存储在 `d` 中：

```cpp
d = i;
```

同样，以下语句将 `d` 中的值转换为整数（截断小数部分）并存储在 `i` 中：

```cpp
i = d;
```

# 11.9 类型转换运算符

类对象也可以赋予相同的功能。例如，假设 `distance` 是一个长度对象而 `d` 是 double，如果 `Length` 写得当，以下语句将方便地将 `distance` 以浮点数的形式存储在 `d` 中：

```cpp
d = distance;
```

为了能够使用这样的语句，必须编写一个运算符函数来执行转换。这里有一个将 `Length` 对象转换为 double 的函数：

```cpp
Length::operator double() const
{
    return len_inches / 12 + (len_inches % 12) / 12.0;
}
```

该函数在函数头中计算长度测量的实际等值。例如，4英尺6英寸的测量值将转换为长度 4.5。

> 注意：函数头中没有指定返回类型，因为该类型是从运算符函数的名称推断出来的。此外，由于该函数是成员函数，它在调用对象上操作，不需要其他参数。

程序 11 展示了修改后的 `Length` 类，同时具有 double 和 int 转换运算符。`int` 运算符简单返回 `Length` 对象的英寸数。

# Length2.h 内容

```cpp
#ifndef _LENGTH1_H
#define _LENGTH1_H
#include <iostream>
using namespace std;
class Length {
private:
    int len_inches;
public:
    Length(int feet, int inches)
    {
        setLength(feet, inches);
    }
    Length(int inches) const { return len_inches / 12; }
    int getInches() const { return len_inches % 12; }
    void setLength(int feet, int inches)
    {
        len_inches = 12 * feet + inches;
    }
    // 类型转换运算符
    operator double() const;
    operator int() const { return len_inches; }
    // 重载的流输出运算符
    friend ostream&operator<<(ostream &out, Length a);
};
#endif
```

# 第11章 关于类和面向对象编程的更多

Length2.cpp 内容

#include "Length2.h"

```cpp
// Operator double 将 Length 转换为 double
//********************************
Length::operator double() const
{
    return len_inches / 12 + (len_inches % 12) / 12.0;
}

//************************************************
// 重载的流插入运算符 << 
//************************************************
ostream& operator<<(ostream& out, Length a)
{
    out << a.getFeet() << " feet, " << a.getInches() << ". inches.\";
    return out;
}
```

# 程序 11-19

```cpp
// 此程序演示了 Length 类
// 的类型转换运算符。
#include "Length2.h"

#include <iostream>
#include <string>
using namespace std;

int main()
{
    Length distance(0);
    double feet;
    int inches;
    distance.setLength(4, 6);
    cout << "The Length object is " << distance << " " << endl;

    // 转换并打印
    feet = distance;
    inches = distance;
    cout << "The Length object is " << feet << " " << endl;
    cout << "The Length object is " << inches << " " << endl;
}
```

# 输出

The Length object is 4 feet, 6 inches.

The Length object is 4.5 feet.

The Length object is 6 inches.

# 807

# 转换构造函数

**概念：** 除了提供创建对象的方法，转换构造函数为编译器提供了隐式类型转换。接受除类以外的单个参数的构造函数被称为转换构造函数。

作为一个简单的例子，考虑以下类：

```cpp
class IntClass
{
private:
    int value;
public:
    // 从 int 的转换构造函数
    IntClass(int intValue)
    {
        value = intValue;
    }
```

当上下文需要类对象时，编译器会自动调用转换构造函数。这发生在四种不同的上下：

1. 类的对象使用构造函数类型的值进行初始化：例如

   `IntClass setObject = 23;`

2. 类的对象被赋值一个构造函数类型的值：例如

   `intObject = 24;`

3. 期望类类型值的函数被传递了构造函数类型的值。例如，我们可以定义一个函数

```cpp
void printValue(IntClass x)
{
    cout << x.getValue();
}
```

然后在调用它时传递它：`printValue(25);`。编译器将使用转换构造函数将整数 25 转换为 `IntClass` 对象，然后将对象传递给函数。

4. 声明类类型返回值的函数通常返回构造函数类型的值。例如，编译器将接受以下内容

注意，编译器将隐式将整数 `intValue` 转换为 `IntClass` 对象。从函数返回的是这个对象。

以下程序说明了转换构造函数的操作。

# Convert.h 内容

```cpp
#include <iostream>
using namespace std;

class IntClass
{
private:
    int value;
public:
    IntClass(int intValue)
    {
        value = intValue;
    }
    int getValue() const { return value; }
};
```

# Convert.cpp 内容

```cpp
#include "Convert.h"
//****************************************************
// 该函数返回一个 int，尽管
// IntClass 对象被声明为
// 返回类型。
//****************************************************
IntClass f(int intValue)
{
    return intValue;
}
```

## 11.10 转换构造函数

```cpp
//********************************
// 打印 IntClass 对象内部的 int 值。
//********************************
void printValue(IntClass x)
{
    cout << x.getValue();
}
```

## 程序 11-20

```cpp
// // 此程序演示了
// 转换构造函数的作用。
#include "Convert.h"

// 函数原型。
void printValue(IntClass);
IntClass f(int);

int main()
{
    // 使用 int 初始化
    IntClass intObject = 23;
    cout << "The value is " << intObject.getValue() << endl;

    // 赋值 一个 int
    intObject = 24;
    cout << "The value is " << intObject.getValue() << endl;

    // 将 int 传递给期望 IntClass 的函数
    cout << "The value is ";
    printValue(25);
    cout << endl;

    // 演示返回时的转换
    intObject = f(26);
    cout << "The value is ";
    printValue(intObject);

    return 0;
}
```

程序输出

The value is 23

The value is 24

The value is 25

The value is 26

在返回时演示转换。

值是 23

值是 24

值是 25

值是 26

当一个函数返回一个类型对象时，如果该类型与函数的返回类型不匹配，且该类型有一个相应的转换构造函数，C++ 就会使用转换构造函数。

## 检查点

- 11.37 使用转换函数来执行构造函数有什么好处？
- 11.38 为什么在执行构造函数时不需要指定类型？
- 11.39 假设有一个名为 BlackBox 的类。编写一个将 BlackBox 转换为 int 的成员原型。
