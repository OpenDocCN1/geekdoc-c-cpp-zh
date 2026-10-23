

为了说明本章以及第 6 章中将要介绍的内容，我们创建了众所周知的递归元函数来实现上述算法：

// Fibonacci
template <int N>
    struct Fibonacci
{
        enum { value = Fibonacci<N-1>::value + Fibonacci<N - 2>::value};
};

template <>
    struct Fibonacci<0>
{
        enum { value = 0 };
};

template <>
    struct Fibonacci<1>
{
        enum { value = 1 };
};

void TestFibonacci()
{
    // 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
    int x = Fibonacci<6>::value; // 8
    int y = Fibonacci<9>::value; // 34

    std::cout << x << ", " << y << '\n';
}
```

这里使用的 C++ 惯用法比类型生成器惯用法更通用，在类型生成器惯用法中，类型族的共同（不变）部分被收集到一个结构中，该结构唯一的目的是生成另一种类型。

类型生成器惯用法的意图是：

- 简化基于模板的复杂类型的创建。
- 基于模板参数合成新的类型或类型。
- 在使用基于策略的设计 PBD 时，定位默认策略（我们在第 9 章讨论 PBD）。

让我们举一个例子。考虑通过创建一个适配器类来引入间接的额外层，该适配器类捕获不变部分（本例中为 Boost 内存分配器）和可自定义的变体部分（列表中的底层元素类型）：

// Type generators
template <class Value>
    struct List

*operations.* 我们简要介绍这些主题，以便为后续章节中更高级的主题和应用做准备。

一般来说，当期望不同类型的值时，转换可能会在表达式中发生，例如：

- **A1:** 在赋值运算符中；右操作数的值被转换为左操作数未限定类型。
- **A2:** 标量初始化；初始化表达式的值被转换为左操作数未限定类型。
- **A3:** 调用函数时参数类型与函数原型声明中不同。
- **A4:** 函数返回语句中操作数的值被转换为具有函数返回类型对象。

一些简单的代码来展示我们所说的这些例子：

```
double func(double d)
{
    return d*d;
}

double func()
{  // Return type (an int) convert to double

    int result = 1'000'000;
    return result;
}

void ImplicitConversions()
{  // Simple examples of conversions

    // Assignment
    int i = 1L;                       // Convert long to int
    int j = 3.14;                     // Truncate a double

    // Scalar initialisation
    double d2 = 2.4;
    int i2 = 3;
    double d3 = i2*d2;

    // Function call expression
    int i3 = 5;
    std::cout << func(i3) << '\n';

    // Function return type
    int i4 = func(3.14);
    std::cout << i4 << '\n';

    std::cout << func() << '\n';
}
```

由于发生了转换，编译此代码时会生成警告。

我们现在讨论定义二元运算符的主题，其操作数类型不同。很明显，其中一个操作数必须使用算术转换提升为与另一个操作数相同的类型。目标是产生一个公共类型（也由我们将在第 6 章讨论的 std::common_type 类型特征支持）。我们在这里不深入细节，但重要的是要知道应用了哪些规则。一些指导原则是：

- 如果任一操作数是 long double，则另一个操作数被转换为 long double。
- 如果任一操作数是 double，则另一个操作数被转换为 double。
- 如果任一操作数是 float，则另一个操作数被转换为 float。
- 类型 bool、char、char16_t、char32_t、wchar_t 和无作用域枚举被提升为整数。
- 整数转换等级按以下顺序递增：bool、signed char、short、int、long、long long。

我们在第 6 章和第 8 章中更详细地讨论积分和浮点类型。

## 4.2.2 可变参数函数简介

可变参数函数是接受可变数量参数的函数。一个著名的例子是函数 std::printf。为了定义可变参数函数，我们使用对象类型 va_list，它保存有关函数参数的信息。此对象可通过以下函数宏访问：

- va_start：启用对可变参数函数参数的访问。
- va_arg：访问下一个可变参数函数参数。
- va_copy：复制可变参数函数参数。
- va_end：结束遍历可变参数函数参数。

我们举一个例子；在这种情况下，我们定义一个可变参数函数来求整数列表的和：

```
long AddIntegers(long count, ...)
{ // Variadic function

    long result = 0;

    // Hold information needed by other macros
    va_list args;

    // Enable access to variadic function arguments
    va_start(args, count);

    // Iterate over the arguments
    for (int n = 0; n < count; ++n)
    {
        // Access next variadic function argument
        result += va_arg(args, long);
    }

// End traversal of variadic function arguments
va_end(args);

return result;
}
```

一个例子是：

```
std::cout << AddIntegers(4, 10, 10, 10, 20) << '\n';      // 50
std::cout << AddIntegers(4, 10, 'A', true, false) << '\n';   // 76
```

## 4.2.3 值类别

一般来说，C++ 表达式是一个名称，它包含运算符及其操作数、文字和变量名。表达式由两个正交属性表征，即其类型和值类别。我们还注意到表达式具有标识，这意味着可以比较表达式（例如，它们是否引用同一实体？）并且我们可以比较对象或它们标识的函数的地址。

有三个主要值类别：

- xvalue：具有标识并且可以从中移动。
- lvalue：具有标识并且不能从中移动。
- prvalue：没有标识并且可以从中移动。它是一个纯值表达式。

- xvalue：具有标识并且可以从中移动。
- lvalue：具有标识并且不能从中移动。
- prvalue：没有标识并且可以从中移动。它是一个纯值表达式。

具有标识的表达式称为 glvalue 表达式（广义左值）。因此，xvalues 和 lvalues 都是 glvalues。可以从中移动的表达式称为 rvalue 表达式。prvalues 和 xvalues 都是 rvalue 表达式。

lvalue 表达式的例子是：a = b 和字符串文字。prvalue 表达式的例子是：42、true、转换为非引用类型的强制转换表达式（例如，static_cast<double>(x)）、&a（变量 a 的地址）和 lambda 表达式。xvalue 表达式的例子是：转换为右值引用类型的强制转换表达式（例如，static_cast<double&&>(x)）和函数调用。

我们将在第 4.3.4 节中给出这些类型和类别的一些具体示例。

## 4.3 decltype 说明符

decltype 说明符检查实体声明的类型或表达式的类型和值类别。它可以被视为一种元函数，因为它接受实体或表达式作为输入，并产生该实体或表达式的类型作为输出。当声明难以或无法使用标准记法声明的类型时，说明符很有用，例如 lambda 相关类型或依赖于模板参数的类型。我们期望 decltype 在创建涉及混合模式算术的代码、类和库时很有用。

### 4.3.1 初始示例

我们使用内置类型举一些混合模式算术的例子：

```
```cpp
int i=20;                  // Create an int.
double d=3.16;             // Create a double.

decltype(i) j=i;           // j is an int.
decltype(d) k=d;           // k is a double.

// Promote float * int to double
float f = 3.3F;
int n= 4;
decltype(d) d2 = f*n;
```
```

在最后一个例子中，我们声明变量 d2 应该是 double 类型。我们可以通过调用 `std::is_same` 类型特征（我们在第 6 章中更详细地讨论）来检查此声明的有效性：

```
```cpp
std::cout << "Check decltype:  " << std::is_same<double,
decltype(d)>::value; // true
```
```

（使用与上面相同的变量）。

另一个使用与上面相同的变量的例子是：

```
```cpp
// What is the result of int*double. With decltype we
// don't need to know anymore.
decltype(j*k) l=j*k; // Result of int*double is double.
std::cout<<j<<"*"<<k<<"="<<l<<std::endl;

std::cout << "Check decltype:  "
          << std::is_same<double, decltype(j*k)>::value;   // true
```
```

最后，decltype 可以应用于 lambda 函数，如以下代码所示：

```
```cpp
// decltype and lambda functions
auto f2 = [](double x, double y) -> int
{
    int result = std::floor(x + y);
    return result;
};

auto f3 = [](double x, double y) -> double
{
    double result = x + y;
    return result;
};

// Lambda function types are unique and unnamed
std::cout << std::boolalpha
          << "Type of lambda function, not its return type:  "
          << std::is_same<int, decltype(f2)>::value;  // false
```
```

