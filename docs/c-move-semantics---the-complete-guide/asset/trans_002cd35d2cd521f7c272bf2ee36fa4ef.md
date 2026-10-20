

This page is intentionally left blank

## Chapter 8

## Value Categories

本章介绍了移动语义的正式术语和规则。我们正式引入了诸如 lvalue、rvalue、prvalue 和 xvalue 等值类别，并讨论了它们在将引用绑定到对象时的作用。这使我们能够讨论移动语义不会自动传递的规则的细节，以及 decltype 在对表达式调用时非常微妙的行为。

本书中最复杂的一章就是本章。你可能会看到一些棘手且对某些人难以置信的事实和特性。以后每当你阅读关于值类别、将引用绑定到对象以及 decltype 的内容时，都可以回来重读本章。

## 8.1 Value Categories

要编译一个表达式或语句，不仅涉及类型的匹配是否合适。例如，你不能将一个 int 赋给一个 int，当赋值运算符的左手边使用的是一个 int 字面量时：

```
int i = 42;

i = 77;     // OK
77 = i;     // ERROR
```

因此，C++ 程序中的每个表达式都有一个值类别。除了类型之外，值类别对于判断可以用表达式做什么至关重要。

然而，值类别在 C++ 中随着时间的推移而发生了变化。

### 8.1.1 History of Value Categories

历史上（取自 Kernighan&Ritchie C，*K&R C*），我们只有值类别 *lvalue* 和 *rvalue*。这些术语来自赋值中允许的操作：

- 一个 *lvalue* 可以出现在赋值的 *左手* 边
- 一个 *rvalue* 只能出现在赋值的 *右手* 边

根据这个定义，当你使用一个 int 对象/变量时你使用的是一个 lvalue，但当你使用一个 int 字面量时你使用的是一个 rvalue：

```
int x;          // x is an lvalue when used in an expression

x = 42;         // OK, because x is an lvalue and the type matches
42 = x;         // ERROR: 42 is an rvalue and can be only on the right-hand side of an assignment
```

然而，这些类别不仅对赋值很重要。它们通常用于指定表达式是否以及在何处可以使用。例如：

```
int x;          // x is an lvalue when used in an expression

int* p1 = &x;   // OK: & is fine for lvalues (object has a specified location)
int* p2 = &42;  // ERROR: & is not allowed for rvalues (object has no specified location)
```

然而，随着 ANSI-C 的出现，事情变得更加复杂，因为声明为 const int 的 x 不能站在赋值的左手边，但仍然可以在只能使用 lvalue 的许多其他地方使用：

```
const int c = 42;    // Is c an lvalue or rvalue?

c = 42;              // now an ERROR (so that c should no longer be an lvalue)
const int* p1 = &c;  // still OK (so that c should still be an lvalue)
```

C 中的决定是，声明为 const int 的 c 仍然是一个 lvalue，因为大多数 lvalue 的操作仍然可以对特定类型的 const 对象调用。唯一不能再做的事情是让一个 const 对象出现在赋值的左手边。

因此，在 ANSI-C 中，l 的含义被改为 locator value。lvalue 现在是一个在程序中具有指定位置的对象（因此例如你可以取其地址）。同样，rvalue 现在可以被视为只是可读的值。

C++98 采用了这些值类别的定义。然而，随着移动语义的引入，问题出现了：用 std::move() 标记的对象应该具有哪种值类别，因为用 std::move() 标记的类对象的行为应遵循以下规则：

```
std::string s;
...
std::move(s) = "hello";   // OK (behaves like an lvalue)
auto ps = &std::move(s);   // ERROR (behaves like an rvalue)
```

然而，注意基本数据类型（FDTs）的行为如下：

```
int i;
...
std::move(i) = 42;        // ERROR
auto pi = &std::move(i);  // ERROR
```

除了基本数据类型之外，用 std::move() 标记的对象仍应像 lvalue 一样行为，允许你修改其值。另一方面，也有诸如你不应能够取其地址之类的限制。

因此引入了一个新的类别 xvalue（“eXpiring value”）来指定显式标记为我不再需要此处的价值的对象（主要是用 std::move() 标记的对象）的规则。然而，前 rvalue 的大部分规则也适用于 xvalue。因此，前主要值类别 rvalue 变为一个复合值类别，现在同时表示两个新的主要值类别 prvalue（对于以前是 rvalue 的所有内容）和 xvalue。参见 http://wg21.link/n3055 中提出这些更改的论文。

### 8.1.2 Value Categories Since C++11

自 C++11 以来，值类别如 Figure 8.1 所描述。

![](img/c6f2c4fe3e0701d95a17354ad517147a_144_0.png)

*Figure 8.1. Value categories since C++11*

我们有以下主要类别：

- **lvalue**（“locator value”）
- **prvalue**（“pure readable value”）
- **xvalue**（“eXpiring value”）

复合类别为：

- **glvalue**（“generalized lvalue”）作为“lvalue 或 xvalue”的通用术语
- **rvalue** 作为“xvalue 或 prvalue”的通用术语

#### Value Categories of Basic Expressions

**lvalues** 的例子有：

- 仅为变量、函数或数据成员名称的表达式（除 rvalue 的普通值成员外）
- 仅为字符串字面量的表达式（例如，"hello"）
- 如果函数声明为返回 lvalue 引用，则该函数的返回值（返回类型 *Type&*）
- 对函数的任何引用，即使标记了 `std::move()`（见下文）
- 内置一元 `*` 运算符的结果（即解引用原始指针得到的内容）

**prvalues** 的例子有：

- 由非字符串字面量的内置字面量组成的表达式（例如，42、true 或 nullptr）
- 如果函数声明为按值返回，则该函数的返回类型（返回类型 *Type*）
- 内置一元 `&` 运算符的结果（即取表达式地址得到的内容）
- 一个 lambda 表达式

**xvalues** 的例子有：

- 用 `std::move()` 标记对象的结果
- 对对象类型（非函数类型）的 rvalue 引用进行转换
- 如果函数声明为返回 rvalue 引用，则该函数的返回值（返回类型 *Type&&*）
- rvalue 的非静态值成员（见下文）

例如：

```
class X {
};

X v;
const X c;
```

```
f(v);      // passes a modifiable lvalue
f(c);      // passes a non-modifiable lvalue
f(X());    // passes a prvalue (old syntax of creating a temporary)
f(X{});    // passes a prvalue (new syntax of creating a temporary)
f(std::move(v));  // passes an xvalue
```

粗略地说，作为经验法则：

- 所有用作表达式的名称都是 lvalues。
- 所有用作表达式的字符串字面量都是 lvalues。
- 所有非字符串字面量（42、true 或 nullptr）都是 prvalues。
- 所有没有名称的临时对象（尤其是按值返回的对象）都是 prvalues。
- 所有用 std::move() 标记的对象及其值成员都是 xvalues。

值得强调的是，严格来说，glvalues、prvalues 和 xvalues 是表达式的术语，而不是值的术语（这意味着这些术语是误称）。例如，变量本身不是 lvalue；只有表示该变量的表达式才是 lvalue：

```
int x = 3;      // here, x is a variable, not an lvalue
int y = x;      // here, x is an lvalue
```

在第一个语句中，3 是一个 prvalue，用于初始化变量（而不是 lvalue）x。在第二个语句中，x 是一个 lvalue（其求值指定包含值 3 的对象）。lvalue x 被用作 rvalue，这就是初始化变量 y 的方式。

### 8.1.3 Value Categories Since C++17

C++17 具有相同的价值类别，但澄清了值类别的语义含义，如 Figure 8.2 所描述。

解释值类别的关键方法现在是，一般来说，我们有两种主要类型的表达式：

- glvalues：用于长寿命对象或函数的定位的表达式
- prvalues：用于初始化的短寿命值的表达式

xvalue 然后被视为一个特殊的位置，表示其资源/值不再需要的（长寿命）对象。

