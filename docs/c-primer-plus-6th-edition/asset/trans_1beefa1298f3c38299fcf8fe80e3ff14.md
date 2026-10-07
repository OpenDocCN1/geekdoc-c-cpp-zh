
我们可以通过这样修复 ft() 模板：

```
template<class T1, class T2>
void ft(T1 x, T2 y)
{
    decltype(x + y) xpy = x + y;
};
```

`decltype` 功能比这些示例看起来要复杂一些。编译器必须通过一个检查列表来决定类型。假设我们有以下代码：

```
decltype(expression) var;
```

这里是列表的某种简化版本。
阶段 1：如果 `expression` 是一个未加括号的标识符（即没有额外的括号），那么 `var` 的类型与标识符的类型相同，包括 `const` 等限定符：

```
double x = 5.5;
double y = 7.9;
double &rx = x;
const double *pd;
decltype(x) w; // w 是类型 double
decltype(rx) u = y; // u 是类型 double &
decltype(pd) v; // v 是类型 const *
```

阶段 2：如果 `expression` 是一个函数调用，那么 `var` 的类型为函数的返回类型：

```
long indeed(int);
decltype(indeed(3)) m; // m 是类型 int
```

> 注意
表达式不会被求值。在这种情况下，编译器会检查原型以获取返回类型；不需要实际调用函数。

阶段 3：如果 `expression` 是一个左值（lvalue），那么 `var` 是指向该表达式类型的引用。这可能意味着由于 `w` 是一个左值，之前的示例如 `w` 将具有引用类型。然而，请记住这种情况情况已经在阶段 1 中捕获了。要应用这一点，`expression` 可以是一个未加括号的标识符。它可以是什么？一种可能性是带括号的标识符：

```
double xx = 4.4;
decltype((xx)) r2 = xx; // r2 是 double &
decltype(xx) w = xx; // w 是 double（阶段 1 匹配）
```

# 函数模板

顺便一下，括号不会改变表达式的值或左值属性。例如，以下两个语句的效果相同：

```
xx = 98.6;
(xx) = 98.6; // ( ) 不影响对 xx 的使用
```

阶段 4：如果上述任一特殊情况都不适用，`var` 的类型与 `expression` 的类型相同：

```
int j = 3;
int &k = j;
int &n = j;
decltype(j+6) i1; // i1 类型 int
decltype(100L) i2; // i2 类型 long
decltype(k+n) i3; // i3 类型 int;
```

注意 `k` 和 `n` 是引用，表达式 `k+n` 并不是引用；它只是两个 int 之和，因此是一个 int。
如果你需要多个声明，可以使用 `decltype` 的 `typedef`：

```cpp
template<class T1, class T2>
void ft(T1 x, T2 y)
{
    typedef decltype(x + y) xtype;
    xtype xpy = x + y;
    xtype arr[10]; xtype &rxy = arr[2]; // rxy 是引用
}
```

# 备用函数语法（C++11 后置返回类型）

`decltype` 机制本身留下了另一个相关问题尚未解决。考虑这个完整的函数：

```
template<class T1, class T2>
?type? gt(T1 x, T2 y)
{
    return x + y;
}
```

再次，我们无法提前知道 `decltype(x + y)` 对于返回类型是什么类型。遗憾的是，在代码的那个点，参数 `x` 和 `y` 还没有声明，因此它们不在作用域内（不可见）。`decltype` 指定符必须在参数声明之后。为了实现这一点，C++11 允许用于声明和定义函数的新语法。以下是使用内置类型的工作方式。原型

`double h(int x, float y);`

可以使用这种替代语法编写：

`auto h(int x, float y) -> double;`

这把返回类型移动到了参数声明之后。`->` 组合被称为后置返回类型。在这里，`auto` 在 C++11 中的角色是后置返回类型提供的占位符。相同的形式用于函数定义：

```cpp
auto h(int x, float y) -> double
/* 函数体 */;
```

将此语法与 `decltype` 结合产生了 `gt()` 返回类型的解决方案：

```cpp
template<class T1, class T2>
auto gt(T1 x, T2 y) -> decltype(x + y)
{
    return x + y;
}
```

现在 `decltype` 在参数声明之后，所以 `x` 和 `y` 在作用域内可以使用。

# 总结

C++ 扩展了函数能力。通过在函数定义中使用 `inline` 关键字并将其放在函数调用之前，你建议 C++ 编译器将函数内联。而不是让程序跳转到单独的代码段来执行函数，用相应的代码替换函数调用。只有当函数很短时使用内联设施。引用是一种伪装指针，允许为变量创建别名。引用变量主要作为结构体和对象的参数。通常，声明为引用的标识符只能引用该类型。但当一个类派生另一个类时，引用派生类型。

C++ 原型允许你为参数定义默认值。如果函数省略参数值，程序将使用默认值。如果函数包含参数值，程序将使用该值而不是默认值。默认参数只能从右到左提供。因此，如果你为某个参数提供默认值，你必须为该参数右侧的所有参数提供默认值。

- 5. 对列表 7.15 进行哪些更改使得 `fill()` 和 `show()` 函数使用引用参数？

# 第8章 函数中的冒险

- 6. 以下是某些效果。说明每种可以通过默认参数、函数重载、两者或均不能实现。提供相应的原型。

- a `mass(density, volume)` 返回密度为 `density` 且为 `volume` 的对象的质量，而 `mass(density)` 返回密度为 `density` 且为1.0 立方米的质量。所有数量都是 `double` 类型。

- b `repeat(10, "I'm OK")` 显示指定的字符串10次，而 `repeat("But're kind of stupid")` 显示指定的字符串5次。

- c `average(3,6)` 返回两个参数的 `int` 平均值，而 `average(3.0, 6.0)` 返回两个 `double` 的平均值。

- d `mangle("I'm glad to meet you")` 返回字符或字符串 "I'm mad to greet you" 的指针，取决于将返回值赋值给 `char` 变量还是 `char*` 变量。

- 7. 编写一个返回参数较大者的函数。

- 8. 给复习题7的模板和复习题4的 `box` 结构，提供一个接受两个 `box` 参数并返回体积较大的模板特化。

- 9. 在以下代码中，`v1`、`v2`、`v3`、`v4` 和 `v5` 被赋值什么类型（假设代码是完整的）：

```
int g(int x);
...
float m = 5.5;
float &rm = m;
decltype(m) v1 = m;
decltype(rm) v2 = m;
decltype((m)) v3 = m;
decltype(g(100)) v4;
decltype(2.0 * m) v5;
```

# 编程练习

- 1. 编写一个通常接受字符串地址作为参数并打印一次该字符串的函数。然而，如果提供了第二个 `int` 类型参数且非零，函数应该根据调用的次数打印字符串。（注意，打印字符串的次数不等于第二个参数的值。）是的，这是一个愚蠢的函数，但它让你使用了本章中的一些技术。在一个简单的程序中使用该函数来演示它是如何运行的。

- `CandyBar` 结构包含三个成员。第一个成员持有糖果的重量（可能带有小数部分），第三个成员持有糖果中的卡路里（整数值）。编写一个使用 `CandyBar` 引用、`char*` 指针、`double` 和 `int` 作为参数的函数，并使用这三个值设置结构中相应的成员。这三个参数应该有 "Millennium Munch,"、2.85 和 350 的默认值。此外，程序还应该使用一个接受 `CandyBar` 引用作为参数并显示结构内容的函数。在适当的地方使用 `const`。

- 编写一个接受 `string` 对象引用作为参数的函数，并将字符串内容转换为大写。使用第6章表6.4中描述的 `toupper()` 函数。编写一个使用循环的程序，允许你用不同的输入测试函数。示例运行可能如下：

```
Enter a string (q to quit): go away
GO AWAY
Next string (q to quit): good grief!
GOOD GRIEF!
Next string (q to quit): q
Bye.
```

- 4. 以下是程序骨架：
#include <iostream>
using namespace std;
#include <string>
struct string {
    char * str; // 指向字符串
    int ct; // 字符串长度（不包括'\0'）
};

set(), show(), 和 show() 的原型放在这里
int main() {
    string beany;
    char testing[] = "Reality isn't what it used to be.";

    set(beans, testing); // 第一个参数是引用，
    // 分配空间存放 testing 的拷贝，
    // 将 beany 的 str 成员指向新块，
    // 将 testing 拷贝到新块，
    // 并设置 beany 的 ct 成员
}
```
*(注：原文中 `beans` 和 `beany` 似乎存在拼写差异，翻译时保留了逻辑或进行了对应)*
