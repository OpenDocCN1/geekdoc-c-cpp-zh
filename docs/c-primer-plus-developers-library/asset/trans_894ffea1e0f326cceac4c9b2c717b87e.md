
模板函数 `use_f()` 有一个静态成员 `count`，我们可以使用它的地址来查看创建了多少个实例化。有五个不同的地址，因此 `use_f()` 模板一定有五个不同的实例化。

要了解发生了什么，请考虑编译器如何确定 `F` 模板参数的类型。首先，看下面这个调用：

```cpp
use_f(y, dub);
```

这里 `dub` 是一个函数的名称，该函数接受一个 `double` 参数并返回一个 `double` 值。函数名是一个指针，因此参数 `F` 的类型变成 `double (*) (double)`，即指向一个接受 `double` 参数并返回 `double` 值的函数的指针。

下一个调用是：

```cpp
use_f(y, square);
```

同样，第二个参数的类型是 `double (*) (double)`，因此这个调用与第一个调用使用相同的 `use_f()` 实例化。

接下来两个对 `use_f()` 的调用以对象作为第二个参数，因此 `F` 分别变成类型 `Fp` 和 `Fq`，所以对于这些 `F` 值，我们得到两个新的实例化。最后，最后两个调用将 `F` 设置为编译器用于 lambda 表达式的任意类型。

### 解决问题

函数包装器让你可以重写程序，使其只使用 `use_f()` 的一个实例化，而不是五个。请注意，程序清单 18.7 中的函数指针、函数对象和 lambda 表达式共享一种共同行为——每个都接受一个 `double` 类型的参数，并且每个都返回一个 `double` 类型的值。我们可以说它们具有相同的调用签名，调用签名由返回类型以及一对括号内以逗号分隔的参数类型列表描述。因此，这六个示例的调用签名都是 `double(double)`。

在 `functional` 头文件中声明的函数模板根据调用签名指定一个对象，并且可用于包装具有相同调用签名的函数指针、函数对象或 lambda 表达式。例如，下面的声明创建一个函数对象 `fdci`，它接受一个 `char` 和一个 `int` 参数并返回 `double` 类型：

```cpp
std::function<double(char, int)> fdci;
```

然后，你可以将任何接受 `char` 和 `int` 类型参数并返回 `double` 类型的函数指针、函数对象或 lambda 表达式赋给 `fdci`。

程序清单 18.7 中的各种可调用参数都具有相同的调用签名——`double(double)`。因此，为了修正程序清单 18.7 并减少实例化数量，我们可以使用 `function<double(double)>` 为六个函数、函数对象和 lambda 创建六个包装器。然后，所有六个对 `use_f()` 的调用都可以用相同的类型（`function<double(double)>`）作为 `F`，从而只产生一个实例化。程序清单 18.8 展示了结果。

### 程序清单 18.8 wrapped.cpp

```cpp
//wrapped.cpp -- using a function wrapper as an argument
#include "somedefs.h"
#include <iostream>
#include <functional>

double dub(double x) {return 2.0*x;}
double square(double x) {return x*x;}

int main()
{
    using std::cout;
    using std::endl;
    using std::function;

    double y = 1.21;
    function<double(double)> ef1 = dub;
    function<double(double)> ef2 = square;
    function<double(double)> ef3 = Fq(10.0);
    function<double(double)> ef4 = Fp(10.0);
    function<double(double)> ef5 = [] (double u) {return u*u;};
    function<double(double)> ef6 = [] (double u) {return u+u/2.0;};
    cout << "Function pointer dub:\n";
    cout << "  " << use_f(y, ef1) << endl;
    cout << "Function pointer square:\n";
    cout << "  " << use_f(y, ef2) << endl;
    cout << "Function object Fp:\n";
    cout << "  " << use_f(y, ef3) << endl;
    cout << "Function object Fq:\n";
    cout << "  " << use_f(y, ef4) << endl;
    cout << "Lambda expression 1:\n";
    cout << "  " << use_f(y, ef5) << endl;
    cout << "Lambda expression 2:\n";
    cout << "  " << use_f(y, ef6) << endl;
    return 0;
}
```

下面是一个示例输出：

```text
Function pointer dub:
  use_f count = 1, &count = 0x404020
  2.42
Function pointer square:
  use_f count = 2, &count = 0x404020
  1.4641
Function object Fp:
  use_f count = 3, &count = 0x404020
  11.21
Function object Fq:
  use_f count = 4, &count = 0x404020
  12.1
Lambda expression 1:
  use_f count = 5, &count = 0x404020
  1.4641
Lambda expression 2:
  use_f count = 6, &count = 0x404020
  1.815
```

从输出中可以看到，`count` 只有一个地址，而 `count` 的值表明 `use_f()` 已被调用六次。因此，我们现在只有一个实例化被调用六次，从而减小了可执行代码的大小。

### 更多选项

让我们看看使用 `function` 还能做的另外几件事。首先，我们实际上不必在程序清单 18.8 中声明六个 `function<double (double)>` 对象。相反，我们可以使用临时的 `function<double (double)>` 对象作为 `use_f()` 函数的参数：

```cpp
typedef function<double (double)> fdd;   // simplify the type declaration
cout << use_f(y, fdd(dub)) << endl;     // create and initialize object to dub
cout << use_f(y, fdd(square)) << endl;
...
```

其次，程序清单 18.8 让 `use_f()` 中的第二个参数去匹配形参 `f`。另一种方法是调整形参 `f` 的类型，使其匹配原始实参。这可以通过将函数包装器对象用作 `use_f()` 模板定义的第二个参数来实现。我们可以这样定义 `use_f()`：

```cpp
#include <functional>
template <typename T>
T use_f(T v, std::function<T(T)> f)   // f call signature is T(T)
{
    static int count = 0;
    count++;
    std::cout << "  use_f count = " << count
              << ", &count = " << &count << std::endl;
    return f(v);
}
```

然后函数调用可以像这样：

```cpp
cout << " " << use_f<double>(y, dub) << endl;
...
cout << " " << use_f<double>(y, Fp(5.0)) << endl;
...
cout << " " << use_f<double>(y, [](double u) {return u*u;}) << endl;
```

参数 `y`、`Fp(5.0)` 等本身并不是 `function<double(double)>` 类型，因此这些调用在 `use_f` 后使用 `<double>` 来指示所需的特化。于是 `T` 被设为 `double`，而 `std::function<T(T)>` 变成 `std::function<double(double)>`。

### 可变参数模板

可变参数模板提供了一种创建接受可变数量参数的模板函数和模板类的方法。这里我们将研究可变参数模板函数。例如，假设我们想要一个函数，它接受任意数量的任意类型的参数（前提是该类型可以用 `cout` 显示），并将这些参数显示为以逗号分隔的列表。例如，考虑下面这段代码：

```cpp
int n = 14;
double x = 2.71828;
std::string mr = "Mr. String objects!";
show_list(n, x);
show_list(x*x, '!', 7, mr);
```

目标是能够以这样的方式定义 `show_list()`：使这段代码可以编译并产生以下输出：

```text
14, 2.71828
7.38905, !, 7, Mr. String objects!
```

要创建可变参数模板，有几个关键点需要理解：

- 模板参数包
- 函数参数包
- 展开参数包
- 递归

### 模板参数包和函数参数包

作为了解参数包工作方式的起点，让我们考虑一个简单的模板函数，它显示仅包含一项的列表：

```cpp
template<typename T>
void show_list0(T value)
{
    std::cout << value << ", ";
}
```

这个定义有两个参数列表。模板参数列表只有 `T`。函数参数列表只有 `value`。像下面这样的函数调用会将模板参数列表中的 `T` 设为 `double`，并将函数参数列表中的 `value` 设为 `2.15`：

```cpp
show_list(2.15);
```

C++11 提供了一个省略号元运算符，使你能够为模板参数包声明一个标识符，模板参数包本质上是一个类型列表。类似地，它还允许你为函数参数包声明一个标识符，函数参数包本质上是一个值列表。语法如下：

```cpp
template<typename... Args>   // Args is a template parameter pack
void show_list(Args... args) // args is a function parameter pack
{
    ...
}
```

`Args` 是模板参数包，`args` 是函数参数包。（与其他参数名一样，任何满足 C++ 标识符规则的名称都可用于这些包。）`Args` 与 `T` 的区别在于：`T` 匹配单个类型，而 `Args` 匹配任意数量的类型，包括零个。考虑下面的函数调用：

```cpp
show_list('S', 80, "sweet", 4.5);
```

在这种情况下，参数包 `Args` 包含与函数调用中的参数匹配的类型：`char`、`int`、`const char *` 和 `double`。

接下来，就像

```cpp
void show_list(T value)
```

声明 `value` 的类型是 `T` 一样，下面这行

```cpp
void show_list(Args... args)   // args is a function parameter pack
```

声明 `args` 的类型是 `Args`。更准确地说，这意味着函数参数包 `args` 包含一个值列表，该列表在类型和数量上都与模板参数包 `Args` 中的类型列表匹配。在这种情况下，`args` 包含值 `'S'`、`80`、`"sweet"` 和 `4.5`。

通过这种方式，`show_list()` 可变参数模板可以匹配以下任意函数调用：

```cpp
show_list();
show_list(99);
show_list(188.55, "cat");
show_list(1,2,4,6,8, "who do we", std::string("appreciate"));
```

在最后一种情况下，`Args` 模板参数包将包含类型 `int`、`int`、`int`、`int`、`int`、`const char *` 和 `std::string`，而 `args` 函数参数包将包含匹配的值 `1`、`2`、`4`、`6`、`8`、`"who do we"` 和 `std::string("appreciate")`。

### 展开参数包

但是，函数如何访问这些包的内容呢？没有索引功能。也就是说，你不能使用类似 `Args[2]` 的方式来访问包中的第三个类型。
