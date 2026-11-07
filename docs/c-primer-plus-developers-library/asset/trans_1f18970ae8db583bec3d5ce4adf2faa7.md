
因此，我们可以这样修复 `ft()` 模板：

```cpp
template<class T1, class T2>
void ft(T1 x, T2 y)
{
    ...
    decltype(x + y) xpy = x + y;
    ...
}
```

`decltype` 设施比这些示例中看起来的要复杂一些。编译器必须经过一系列检查来决定类型。假设我们有如下代码：

```cpp
decltype(expression) var;
```

下面是该清单的一个简化版本。

**阶段 1：** 如果 *表达式* 是未加括号的标识符（即没有额外的括号），那么 `var` 与标识符具有相同的类型，包括 `const` 等限定符：

```cpp
double x = 5.5;
double y = 7.9;
double &rx = x;
const double * pd;
decltype(x) w;       // w is type double
decltype(rx) u = y;  // u is type double &
decltype(pd) v;      // v is type const double *
```

**阶段 2：** 如果 *表达式* 是函数调用，那么 `var` 具有函数返回类型的类型：

```cpp
long indeed(int);
decltype(indeed(3)) m; // m is type int
```

### 注意

调用 *表达式* 不会被求值。在这种情况下，编译器检查原型以获取返回类型；无需实际调用该函数。

**阶段 3：** 如果 *表达式* 是左值，那么 `var` 是对表达式类型的引用。这似乎意味着，既然 `w` 是左值，那么像 `w` 这样的早期示例本应是引用类型。但是请记住，那种情况已在阶段 1 中处理。要应用本阶段，*表达式* 不能是未加括号的标识符。那么它可能是什么呢？一个明显的可能性是加括号的标识符：

```cpp
double xx = 4.4;
decltype((xx)) r2 = xx;  // r2 is double &
decltype(xx) w = xx;     // w is double (Stage 1 match)
```

顺便提一下，括号不会改变表达式的值或左值性。例如，下面两条语句具有相同的效果：

```cpp
xx = 98.6;
(xx) = 98.6;    // () don't affect use of xx
```

**阶段 4：** 如果前面的特殊情况都不适用，`var` 与 `expression` 具有相同的类型：

```cpp
int j = 3;
int &k = j;
int &&n = j;
decltype(j+6) i1;    // i1 type int
decltype(100L) i2;   // i2 type long
decltype(k+n) i3;    // i3 type int
```

注意，尽管 k 和 n 是引用，但表达式 k+n 不是引用；它只是两个 int 的和，因此是 int。

如果需要多个声明，可以将 typedef 与 decltype 一起使用：

```cpp
template<class T1, class T2>
void f(T1 x, T2 y)
{
    ...
    typedef decltype(x + y) xytype;
    xytype xpy = x + y;
    xytype arr[10];
    xytype & rxy = arr[2];    // rxy a reference
    ...
}
```

## 另一种函数语法（C++11 尾置返回类型）

decltype 机制本身还留下另一个相关问题未解决。考虑下面这个不完整的模板函数：

```cpp
template<class T1, class T2>
?type? gt(T1 x, T2 y)
{
    ...
    return x + y;
}
```

同样，我们无法预先知道 x 和 y 相加会产生什么类型。看起来我们可以在返回类型中使用 decltype(x + y)。遗憾的是，在代码中的那个位置，参数 x 和 y 尚未声明，因此它们不在作用域内（对编译器不可见也不可用）。decltype 说明符必须放在参数声明之后。为了实现这一点，C++11 允许一种用于声明和定义函数的新语法。下面以内置类型说明其工作方式。原型

```cpp
double h(int x, float y);
```

可以用这种替代语法写成：

```cpp
auto h(int x, float y) -> double;
```

这会将返回类型移到参数声明之后。组合 `-> double` 称为 *尾置返回类型*。这里，`auto` 在 C++11 的另一个新角色中，是尾置返回类型所提供的类型的占位符。同样的形式也可用于函数定义：

```cpp
auto h(int x, float y) -> double
{ /* function body */ };
```

将这种语法与 `decltype` 结合，就得到下面为 `gt()` 指定返回类型的解决方案：

```cpp
template<class T1, class T2>
auto gt(T1 x, T2 y) -> decltype(x + y)
{
    ...
    return x + y;
}
```

现在 `decltype` 位于参数声明之后，因此 `x` 和 `y` 在作用域内并且可以使用。

## 总结

C++ 扩展了 C 函数的能力。通过在函数定义中使用 inline 关键字，并将该定义放在对该函数的第一次调用之前，你向 C++ 编译器建议将该函数内联。也就是说，编译器不会让程序跳转到单独的代码段来执行该函数，而是用相应的代码内联替换函数调用。只有当函数很短时才应使用内联设施。

引用变量是一种伪装的指针，它允许你为变量创建别名（即第二个名称）。引用变量主要用作处理结构和类对象的函数的参数。通常，声明为对特定类型的引用的标识符只能引用该类型的数据。然而，当一个类派生自另一个类时，例如 ofstream 派生自 ostream，对基类型的引用也可以引用派生类型。

C++ 原型使你能够为参数定义默认值。如果函数调用省略了相应参数，程序将使用默认值。如果函数包含参数值，程序将使用该值而不是默认值。默认参数只能从参数列表的右向左提供。因此，如果你为某个特定参数提供默认值，那么也必须为该参数右侧的所有参数提供默认值。

- 6. 下面是一些期望的效果。指出每一项是否可以通过默认参数、函数重载、两者都可以，还是两者都不可以来实现。提供合适的原型。
  - a. mass(density, volume) 返回一个密度为 density、体积为 volume 的物体的质量，而 mass(density) 返回密度为 density、体积为 1.0 立方米的质量。所有量都是 double 类型。
  - b. repeat(10, "I'm OK") 将指定字符串显示 10 次，而 repeat("But you're kind of stupid") 将指定字符串显示 5 次。
  - c. average(3, 6) 返回两个 int 参数的 int 平均值，而 average(3.0, 6.0) 返回两个 double 值的 double 平均值。
  - d. mangle("I'm glad to meet you") 返回字符 I，或返回指向字符串 "I'm glad to meet you" 的指针，取决于你将返回值赋给 char 变量还是 char* 变量。

- 7. 编写一个函数模板，返回其两个参数中较大的那个。

- 8. 给定复习题 7 的模板和复习题 4 的 box 结构，提供一个模板特化，它接受两个 box 参数并返回体积较大的那个。

- 9. 在下面的代码中，v1、v2、v3、v4 和 v5 被赋予什么类型（假设该代码是一个完整程序的一部分）？

```cpp
int g(int x);
...
float m = 5.5f;
float &rm = m;
decltype(m) v1 = m;
decltype(rm) v2 = m;
decltype((m)) v3 = m;
decltype(g(100)) v4;
decltype(2.0 * m) v5;
```

## 编程练习

- 1. 编写一个函数，通常接受一个参数，即字符串的地址，并将该字符串打印一次。然而，如果提供了第二个 int 类型参数且该参数非零，函数应将字符串打印若干次，打印次数等于到那时为止该函数已被调用的次数。（注意，字符串被打印的次数不等于第二个参数的值；它等于该函数已被调用的次数。）是的，这是一个傻函数，但它让你使用本章讨论的一些技术。在一个简单程序中使用该函数，演示该函数如何工作。

- 2. CandyBar 结构包含三个成员。第一个成员保存糖果棒的品牌名。第二个成员保存糖果棒的重量（可能包含小数部分），第三个成员保存糖果棒中的卡路里数（整数值）。编写一个程序，使用一个函数，该函数接受对 CandyBar 的引用、指向 char 的指针、double 和 int 作为参数，并使用后三个值设置结构的相应成员。后三个参数应具有默认值 “Millennium Munch”、2.85 和 350。程序还应使用一个函数，该函数接受对 CandyBar 的引用作为参数并显示结构的内容。在适当的地方使用 const。

- 3. 编写一个函数，接受对 string 对象的引用作为参数，并将该 string 的内容转换为大写。使用第 6 章表 6.4 中描述的 toupper() 函数。编写一个程序，使用一个循环，允许你用不同的输入测试该函数。示例运行可能如下所示：

```cpp
Enter a string (q to quit): go away
GO AWAY
Next string (q to quit): good grief!
GOOD GRIEF!
Next string (q to quit): q
Bye.
```

- 4. 下面是一个程序骨架：

```cpp
#include <iostream>
using namespace std;
#include <cstring>      // for strlen(), strcpy()
struct stringy {
    char * str;          // points to a string
    int ct;              // length of string (not counting '\0')
};

// prototypes for set(), show(), and show() go here
int main()
{
    stringy beany;
    char testing[] = "Reality isn't what it used to be.";

    set(beany, testing);    // first argument is a reference,
                            // allocates space to hold copy of testing,
                            // sets str member of beany to point to the
                            // new block, copies testing to new block,
                            // and sets ct member of beany
