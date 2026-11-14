

此函数可以使用一个或两个参数调用：

```
x = root(3.5, 3); // like root(7.0, 2)
y = root(7.0);
```

我们可以声明多个默认值，但只能放在参数列表的末尾。换句话说，在带有默认值的参数之后，不能再有没有默认值的参数。

默认值在添加额外参数时也很有帮助。假设我们有一个绘制圆形的函数：

```
draw_circle(int x, int y, float radius);
```

这些圆形都是黑色的。后来，我们添加了颜色：

```
draw_circle(int x, int y, float radius, color c = black);
```

多亏了默认参数，我们不需要重构应用程序，因为带有三个参数的 draw_circle 调用仍然有效。

## 1.5.2 返回结果

在之前的示例中，我们只返回了 double 或 int。这些是行为良好的返回类型。现在我们将看看两种极端情况：大量数据或没有数据。

### 1.5.2.1 返回大量数据

计算大型数据结构新值的函数更加困难。关于详细信息，我们将推迟到后面再讲，这里只提及可选方案。好消息是，编译器足够智能，在许多情况下可以省略返回值的拷贝；参见第 2.3.5.3 节。此外，移动语义（第 2.3.5 节）会窃取临时对象的数据，在前述省略不适用时避免拷贝。高级库使用一种称为表达式模板的技术，完全避免返回大型数据结构，并推迟计算，直到知道将结果存储在哪里（第 5.3.2 节）。无论如何，我们都不能返回指向局部函数变量的引用（第 1.8.6 节）。

### 1.5.2.2 返回空值

从语法上讲，每个函数都必须返回某些东西，即使没有东西可返回。这个困境由名为 void 的 void 类型解决。例如，一个仅打印 x 的函数不需要返回任何东西：

```
void print_x(int x)
{
 std::cout << "The value x is " << x << '\n';
}
```

void 不是真正的类型，而更像是一个占位符，使我们可以省略返回值。我们不能定义 void 对象：

```
void nothing; // Error: no void objects
```

void 函数可以提前终止：

```
void heavy_compute(const vector& x, double eps, vector& y)
{
    for (...) {
        ...
        if (two_norm(y) < eps)
            return;
    }
}
```

使用无参数的 return。

### 1.5.3 内联

调用函数代价相对较高：必须保存寄存器，将参数拷贝到栈上，等等。为了避免这种开销，编译器可以内联函数调用。在这种情况下，函数调用会被函数中包含的操作所替换。程序员可以使用适当的关键字要求编译器这样做：

```
inline double square(double x) { return x*x; }
```

然而，如果没有关键字，编译器并不有义务内联函数，即使这看起来对性能有好处。内联声明仍然有用：用于在多个编译单元中包含函数，我们将在第 7.2.3.2 节讨论。

### 1.5.4 重载

在 C++ 中，只要参数声明足够不同，函数就可以共享相同的名称。这称为函数重载。让我们先看一个示例：

```
#include <iostream>
#include <cmath>

int divide(int a, int b) {
    return a / b;
}

float divide(float a, float b) {
    return std::floor(a / b);
}

int main() {
    int x = 5, y = 2;
    float m = 5.0, n = 2.0;
    std::cout << divide(x, y) << std::endl;
    std::cout << divide(n, m) << std::endl;
    std::cout << divide(x, m) << std::endl; // Error: ambiguous
}
```

这里我们定义了两次 divide 函数：分别使用 int 和 double 参数。当我们调用 divide 时，编译器执行重载决议：

- 1. 是否存在与参数类型完全匹配的重载？如果有，使用它；否则：
- 2. 是否存在经过转换后匹配的重载？有多少个？
  - 0：错误：未找到匹配的函数。
  - 1：使用它。
  - > 1：错误：调用存在歧义。

这如何应用于我们的示例？调用 divide(x, y) 和 divide(n, n) 是精确匹配。对于 divide(x, n)，没有重载完全匹配，两者都通过隐式转换匹配，因此存在歧义。

“隐式转换”这一术语需要一些解释。我们已经看到，数值类型可以相互转换。这些就是示例中演示的隐式转换。当我们稍后定义自己的类型时，可以实现从另一种类型到它的转换，或者反过来从我们的新类型到现有类型的转换。这些转换可以声明为 explicit，并且仅在明确请求转换时应用，而不用于匹配函数参数。

=> c++11/overload_testing.cpp

更正式地说，函数重载必须在其签名上有所不同。在 C++ 中，签名由以下部分组成：

- 函数名称；
- 参数的数量，称为 Arity；以及
- 参数的类型（按各自顺序）。

相比之下，仅在返回类型或参数名称上有所不同的重载具有相同的签名，被视为（禁止的）重新定义：

```
void f(int x) {}
void f(int y) {} // Redefinition: only argument name different
long f(int x) {} // Redefinition: only return type different
```

名称或 arity 不同的函数是不同的，这不言而喻。引用符号的存在将参数类型变为另一种参数类型（因此，f(int) 和 f(int&) 可以共存）。以下三个重载具有不同的签名：

```
void f(int x) {}
void f(int& x) {}
void f(const int& x) {}
```

这段代码片段可以编译。然而，当我们调用 f 时，会出现问题：

```
int i = 3;
const int ci = 4;

f(3);
f(i);
f(ci);
```

所有三个函数调用都存在歧义，因为在每种情况下，最佳匹配都是第一个带值参数的重载和其中一个带引用参数的重载。混合引用参数和值参数的重载几乎总会失败。因此，当一个重载具有引用限定参数时，另一个重载的相应参数也应该是引用限定的。我们可以在玩具示例中通过省略带值参数的重载来实现这一点。然后 f(3) 和 f(ci) 将解析为带常量引用的重载，而 f(i) 将解析为带可变引用的重载。

### 1.5.5 main 函数

main 函数与其他任何函数在本质上没有区别。标准中允许两种签名：

```
int main()

或

int main(int argc, char* argv[])
```

后者等价于

```
int main(int argc, char** argv)
```

参数 argv 包含参数列表，argc 是其长度。在大多数系统上，第一个参数（argv[0]）是被调用的可执行文件的名称（可能与源代码文件名不同）。为了操作参数，我们可以编写一个名为 argc_argv_test 的短程序：

```
int main (int argc, char* argv[])
{
    for (int i = 0; i < argc; ++i)
        cout << argv[i] << '\n';
    return 0;
}
```

使用以下选项调用此程序：

```
argc_argv_test first second third fourth
```

产生：

```
argc_argv_test
first
second
third
fourth
```

如您所见，命令中的每个空格都会分隔参数。`main` 函数返回一个整数作为退出代码，指示程序是否正确结束。返回 0（或来自 `<cstdlib>` 的宏 `EXIT_SUCCESS`）表示成功，其他任何值表示失败。在 `main` 函数中省略 return 语句是符合标准的。在这种情况下，`return 0;` 会自动插入。更多详细信息见第 A.2.5 节。

## 1.6 错误处理

> "只有在你拒绝纠正错误时，错误才成为过失。"
> —约翰·F·肯尼迪

### 1.6.1 断言

头文件 `<cassert>` 中的宏 `assert` 继承自 C 语言，但仍然很有用。它对表达式求值，当结果为假时，程序会立即终止。它应当用于检测编程错误。假设我们实现了一个酷炫算法来计算非负实数的平方根。那么根据数学知识，结果应该是非负的。否则，我们的计算就出了问题：

```
#include <cassert>

double square_root(double x)
{
    check_somehow(x >= 0);
    ...
    assert(result >= 0.0);
    return result;
}
```

目前尚未说明如何实现初始检查。当我们的结果为负数时，程序执行会打印类似以下的错误：

```
assert_test: assert_test.cpp:10: double square_root(double):
Assertion 'result >= 0.0' failed.
```

事实是，当我们的结果小于零时，我们的实现包含一个错误，在将此函数用于严肃应用之前必须修复它。

修复错误后，我们可能会想移除断言。我们不应该这样做。也许有一天我们会更改实现；那时我们仍然有所有的健全性测试在起作用。实际上，对后置条件的断言在某种程度上就像微型单元测试。

