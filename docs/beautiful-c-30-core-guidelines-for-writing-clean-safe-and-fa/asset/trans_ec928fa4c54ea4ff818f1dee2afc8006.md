

## 第1.5章
### ES.10：每个声明只声明一个名字
### 让我来介绍

声明将一个名字引入程序中。它也可以重新引入一个名字：多个声明是完全允许的，因为没有它们，我们将无法进行前置声明。定义是一种特殊的声明，因为它提供了足够的细节，以便能够使用已命名的对象。

声明类型的数量惊人。你可以声明函数，像这样：

```
int fn(int a);
```

这是声明的一个非常常见的用途。引入了一个名字 fn，其类型是“接受一个整数并返回一个整数的函数”。你可以在代码中使用这个函数，而不必先定义它。你可以声明函数或类模板，像这样：

点击此处查看代码图像

```
template <class T, class U>
int fn(T a, U b);

template <class T>
class cl {
public:
cl(T);

private:
T t;
};
```

这是一个接受任意类型 T 和 U 并返回 int 的函数，以及一个用任意类型 T 构造的类。你还可以声明部分特化和显式模板特化，以及显式模板实例化：

点击此处查看代码图像

```
template <class T> int fn(T a, int b); // Partial specialization
template <> int fn(float a, int b); // Explicit specialization
template class cl<int>; // Explicit instantiation
```

你可以声明命名空间：

点击此处查看代码图像

```
namespace cg30 {
... // more declarations
}
```

你可以声明链接性，以便与其他语言互操作：

```
extern "C" int x;
```

你可以声明属性：

点击此处查看代码图像

```
// Warn if the return value is discarded rather than assigned
[[nodiscard]] int fn(int a);
```

还有一组只能在块内部进行的声明；例如，在函数体内。这些包括 asm 声明，在这里你可以为编译器指定要插入到输出流中的显式汇编语言指令：

点击此处查看代码图像

```
asm {
    push   rsi
    push   rdi
    sub    rsp, 184
}
```

类型别名声明可以为冗长的类型引入简短的名称：

```
using cl_i = cl<int>;
```

命名空间别名可以缩短冗长的嵌套命名空间：

点击此处查看代码图像

```
namespace rv = std::ranges::views;
```

using 声明可以将其他命名空间中的名字引入当前块：

点击此处查看代码图像

```
using std::string; // Now you no longer need to
// type the
// std:: prefix in this block for
// string
```

using 指令与 using 声明不同，它将整个命名空间注入当前块：

点击此处查看代码图像

```
using namespace std; // Never do this at global namespace scope. Ever.
```

还有使用相同限定符的独立声明。例如：

```
int a, b, c, d;
```

这里有四个整数实例，分别命名为 a、b、c 和 d。

### 向后兼容性

看这个：

```
int* a, b, c, d;
```

这些对象是什么类型？

我们希望你已经发现了陷阱，并说出 a 是指向 int 的指针，而 b、c、d 是 int（这就是为什么你经常看到指针声明时将星号放在标识符旁边而不是类型旁边的原因之一）。当然，你能发现它，是因为你在故意寻找问题；历史上我曾发现过编译错误，其中程序员假设它们都是指向 int 的指针。

这是合法的，但并不明智。这是一个等待发生的事故，应该从语言中剔除。至少，当我告诉一位同事这件事时，他就是这样说的。不幸的是，出于向后兼容的原因，这是合法的。C 编程语言允许这样做，因为它曾经要求你在函数顶部声明所有对象。这告诉编译器栈应该增长多少，并在函数入口处为所有数据提供地址。这是一个方便的优化。然而，更明智的做法是像这样将声明写在单独的行上：

```
int* a;
int b;
int c;
int d;
```

`std::auto_ptr`，而 `std::unique_ptr` 是其直接替代品。

### 编写更清晰的声明

回到本指南的主题，要求早期声明可能会导致一些相当繁忙的函数前奏。该指南给出了以下示例：

点击此处查看代码图像

```
char *p, c, a[7], *pp[7], **aa[10];
```

如果不允许每个声明有多个名字，这将扩展为

点击此处查看代码图像

```
char *p; char c; char a[7]; char *pp[7]; char **aa[10];
```

或者更可能的是：

```
char *p;
char c;
char a[7];
char *pp[7];
char **aa[10];
```

这将消耗五行认知空间，而不是一行。

> “但是，”你可能会想，“如果我的函数有很多状态怎么办？那我该怎么做？一条一条地列出来，占半个屏幕？我需要把相关部分组合在一起，而不是让它们在不同行上，它们之间还需要一整个空行。在到达实际函数之前会有太多东西。这不利于可读性。这是个愚蠢的想法。”

关键在“把相关部分组合在一起”，这在我看来很像“形成一种抽象”。如果你已经以某种方式关联了状态，那么通过定义一个结构体来形式化这种关系，并以一种能够捕捉和识别这种关系的方式为其命名。将相关功能推入结构体。然后你可以用一条声明替换那几行声明：该结构体的一个实例。你应该时刻保持警惕，寻找创建有用抽象的机会。

### 结构化绑定

本指南有一个例外，即涉及结构化绑定的使用。这一创新在 C++17 中引入，允许你将数组或非联合类类型绑定到一组名字。例如，最简单的情况：

点击此处查看代码图像

```
int a[2] = {1, 2};
auto [x, y] = a; // x = a[0], y = a[1]
```

绑定到类似 tuple 的类型也很简单：

点击此处查看代码图像

```
std::unordered_map<std::string, int> dictionary;
auto [it, flag] = dictionary.insert({"one", 1});
// it points to the element
// flag signals whether the insertion was successful
```

绑定到结构体以解包它的工作方式相同：

点击此处查看代码图像

```
struct s {
    int a;
    float b;
};

s make_s();

auto [sa, sb] = make_s(); // sa is an int
// sb is a float
```

在每种情况下，你都会看到每个声明中有多个名字。然而，我们可以通过将名字声明在单独的行上来减少任何混淆，如下所示：

点击此处查看代码图像

```
std::unordered_map<std::string, int> dictionary;
auto [it,    // it points to the element
      flag]   // flag signals whether the
// insertion was successful
    = dictionary.insert({"one", 1});
```

一个人的简化可能是另一个人的复杂化，所以这当然是个品味和风格问题。

### 总结

这是一个相当简单的指南，针对的是旧习惯。许多核心指南都引导你编写更易读、能快速理解的代码。本指南归结为三点考虑。

- 声明有很多种。
- 名字可以在任何地方引入。
- 除非语言要求，否则不要通过每行引入多个名字来混淆声明。

## 第1.6章
### NR.2：不要坚持函数中只能有一个 return 语句
### 规则在演变

令我惊讶的是，在21世纪已经过去了20%的时候，人们仍在争论这个问题。核心指南的这一部分被称为“非规则和神话”。一个非常普遍的建议是函数中应该只有一个 return 语句，这正好属于这一类。

强制要求单一 return 语句是一个很老很老的规则。人们很容易忘记编程领域已经取得的进步。我买了我的第一台计算机，或者更确切地说，是我的父母在1981年买的。那是一台 Sinclair ZX81，由运行在3.25MHz的 NEC Z80 CPU 驱动。操作系统存储在8KB的只读存储器（ROM）中，包含一个 BASIC 解释器，使我能够在可怜的1KB RAM中编写简单的程序。

当然，我当时14岁，我想编写游戏，我发现最好的方法是完全绕过 BASIC 解释器，直接用原生 Z80 汇编语言编写。在托尼·贝克¹的*精通ZX81机器代码*、罗德奈·扎克斯²的*Z80编程*以及一个汇编器的帮助下，我得以编写我的第一批游戏并卖给学校的同学们。

1. Baker, T, 1982. *精通ZX81机器代码*. Reston, VA: Reston Publishing Company, Inc.

2. Zaks, R, 1979. *Z80编程*. Berkeley, CA: Sybex.

我发现用 Z80 汇编语言编写东西比用 BASIC 困难得多。特别是，BASIC 有行号和子程序的概念。我可以通过执行 GOTO 来分支，也可以分支通过

