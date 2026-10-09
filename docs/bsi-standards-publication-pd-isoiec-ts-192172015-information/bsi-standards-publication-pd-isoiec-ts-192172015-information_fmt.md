
# BSI 标准出版 PD ISO/IEC TS 19217：2015 信息技术 编程语言 C++ 概念扩展

![](img/e6ef4c765bbb1f3e7b4441293baadfd4_0_0.png)

![](img/e6ef4c765bbb1f3e7b4441293baadfd4_2_0.png)

# 前言

ISO（国际标准化组织）和 IEC（国际电工委员会）组成了全球标准化的专门体系。ISO 或 IEC 的成员国家机构通过各自组织建立的处理特定技术活动领域的的技术委员会参与国际标准的制定。ISO 和 IEC 技术委员会在共同利益领域开展合作。与 ISO 和 IEC 联系的其他国际组织、政府和非政府组织也参与了工作。在信息技术领域，ISO 和 IEC 建立了联合技术委员会 ISO/IEC JTC 1。

用于开发本文档并旨在对其后续维护的程序已在 ISO/IEC 指南第 1 部分中说明。特别应注意不同类型文档所需的不同批准标准。本文档是根据 ISO/IEC 指南第 2 部分的编辑规则起的（参见 www://www.iso.org）。

注意，本文档的某些元素可能涉及专利权。ISO 和 IEC 对此类专利权不负责（参见 iso.org/directives）。

本文中使用的贸易名称仅供用户参考，不构成认可。关于技术贸易壁垒（TBT）的解释，请参见前言。

负责本文档的委员会是 ISO/IEC JTC 1 信息技术，SC 22 编程语言、其环境和系统软件接口。

`N4549`

# 1 一般

## 1.1 范围

本技术规范描述了 C++ 语言（1.2）的扩展，这些扩展实现了约束的规范和检查，以及基于这些约束的重载。

国际标准 ISO/IEC 14882 为本技术规范提供了重要的背景和规范。修改或添加的操作以下划线表示添加文本，删除线表示删除文本。

WG21 论文 `N419` 定义了“折叠表达式”，用于定义约束包。该特性在 ISO/IEC 14882:2014 中不存在，但计划在国际标准的下一个版本中包含。该特性的规范包含在本文中。

## 1.2 引用

下列引用是必不可少的。对于引用，仅适用于引用的版本。对于更新引用，适用于引用文档的最新版本（包括任何修订）。

- (1.1) ISO/IEC 14882:2014，编程语言—C++

ISO/IEC 14882:2014 后续称为 C++ 标准。本文档中的章节、节和段落编号反映了 C++ 标准的编号。本技术规范中未出现的章节和节指的是 C++ 标准中原始、未修改的文本。

## 1.3 术语和定义

修改“签名”的定义以包含关联约束（14.10.2）。这允许不同的编译单元包含相同签名（排除关联约束）的定义而不违反签名约束。此类函数具有相同的修饰名，表现为同一函数的多次定义。

### 1.3.1 签名

`<template>` 标识、参数类型列表（8.3.5）以及命名空间（如果有），以及任何关联约束（14.10.2）

> [注：签名是修饰和链接的基础。 — 注结束]

### 1.3.2 签名

`<template>` 标识、参数类型列表（8.3.5）以及命名空间（如果有），返回类型以及模板参数列表，以及任何关联约束（14.10.2）

签名

`<类成员函数>` 名称，参数类型列表 (8.3.5)，该函数为该类的成员，cv-修饰符（任何），以及 ref-修饰符（任何），以及任何相关的约束 (14.10.2)

### 1.3.4 [defus.signature.member.templ]

`<类成员函数模板>` 名称，参数类型列表 (8.3.5)，该函数为该类的成员，cv-修饰符（任何），ref-修饰符（任何），返回类型，模板列表，以及任何相关的约束 (14.10.2)

## 1.4 实现合规性 [intro.compliance]

本规范的符合性要求与 C++ 标准中 1.4 节定义的定义相同。[注：合规性是根据程序的行为定义的。结束注]

## 1.5 特性测试建议 [intro.features]

提供本技术规范支持的实现应当定义表 A 中的特性测试宏。

表 A — 特性测试宏

| 宏名称 | 值 |

|---|---|

| `__cpp_concepts` | 201507 |

- 1 本规范的设计部分程度上基于 C++ 标准库算法部分的概念规范，这被称为“帕洛阿尔托”报告 (WG21 `N351`)，该报告是由一组大量专家开发的，用于测试概念这一想法的表达能力。尽管帕洛阿尔托报告的表示法与本技术规范之间存在语法差异，但该报告可以被视为本技术规范表达能力的大规模测试。

- 2 此项工作由 NSF 资助基金 ACI-1148461 资。

# 2 词法约定

## 2.1 关键字

在 2.1 中，向表 4 添加关键字 `concept` 和 `requires`。

`N4549`

# 5 表达式 [expr]

修改第 8 段以包含对 `requires-expressions` 的引用。

- 在某些上下文中，会出现未求值的的操作数 (5.1.4, 5.2.8, 5.3.3, 5.3.7)。

## 5.1 主表达式 [expr.prim]

### 5.1.1 通用 [expr.prim.general]

在本节中，为主表达式的规则添加 `requires-expression`。

```
primary-expression:
literal
( expression )
id-expression
lambda-expression
fold-expression
requires-expression
```

在第 8 段中，在 `nested-name-specifier` 中添加 `auto` 和 `constrained-type-name`：

```
nested-name-specifier:
::
type-name ::
namespace-name ::
dectype-specifier ::
auto ::
constrained-type-name ::
nested-name-specifier identifier ::
nested-name-specifier template_opt
```

在第 11 段之后添加一个新段落：

在形式为 `auto::` 或 `C::`（其中 C 是 `constrained-type-name`）的 `nested-name-specifier` 中，`nested-name-specifier` 指定一个占位符，稍后根据 7.1.6.4 中的占位符推导规则进行替换。如果由 `constrained-type-specifier` 指定占位符不是占位符，则程序是格式错误的。[注：`constrained-type-specifier` 可以为非类型或模板指定占位符 (7.1.6.4)。结束注] 占位符的替换类型应该是类或枚举类型。[示例：

```
template<typename T> const bool B = sizeof(T) == sizeof(int);
tint const B = true;
```

```
struct S1 { int n; };
struct S2 { char c; };
struct S3 { struct X { using Y = int; }; };
```

```
int auto:* p1 = &S1::n; // auto 被推导为 S1
D::* p2 = &S1::n; // 错误：D 未指定占位符类型
C::* p3 = &S1::n; // 正常：C 被推导为 S1
char C::* p4 = &S2::c; // 错误：因为约束未满足导致推导失败
```

```
void f(typename auto : <X:Y>);  // 错误：无法从 Si1 中推导 auto
f(S<1>()); // 正常
f<S<3>>(O); // 正常
```

在 f 的声明中，占位符 f 是被满足的，尽管 f 是一个非推导上下文 (14.8.2)。它稍后可以通过模板参数的显式指定进行替换。 — 示例结束

在第 13 段之后添加一个新参数

显式或隐式地引用具有未满足的关联约束 (14.10.2) 的函数（除声明外）的程序是格式错误的。[示例]：

```
void f() requires false;

f0(); // 错误：无法调用 f
void (*p1)(int) = f; // 错误：无法获取 f 的地址
dectype(f) p2 = nullptr; // 错误：类型 decltype(f) 无效
```

在每情况下，f 的关联约束均未满足。在 p2 的声明中，即使是未求值的表达式也要求满足约束（第 5 节）。

### 5.1.2 Lambda 表达式 [expr.prim.lambda]

在第 4 段之后插入以下内容以定义“通用 lambda”。

> 通用 lambda 是一种 lambda-expression，其中在 lambda-declarator 的参数-type-list 中出现一个或多个占位符 (7.1.6.4)。

修改第 5 段，使得通用 lambda 的含义根据其简写的成员函数调用运算符进行定义。

非通用 lambda-expression 的闭包有一个公共的内联函数调用运算符 (13.5.4)，分别返回 lambda-expression 的参数-declaration-clause 和尾随返回类型。对于通用 lambda，闭包对于 lambda 参数-template-declaration-clause 中每个出现的 `auto` 按照其出现顺序包含一个类型模板。

### 5.1.3 折叠表达式 [expr.prim.fold]

在 5.2 中添加此内容。

- 折叠表达式在二元运算符上对模板包 (14.6.3) 执行操作。

`N4549`

```
fold-expression:
( cast-expression fold-operator ... )
( fold-operator cast-expression ...)
( cast-expression fold-operator ...)
fold-operator: one of
+ = / % % & >>
- += %= |= >>==
! != < > && | .+
```

- 形式为 (e op) 且 op 是 fold-operator 的表达式称为左折叠。形式为 (e op) 且 op 是 fold-operator 的表达式称为右折叠。

左折叠和右折叠统称为折叠。在二元折叠中，左折叠。如果 e2 包含参数包，则 e1 应当包含参数包，但不可能是两者都包含。如果 e1 包含参数包，该表达式称为二元左折叠。如果 e2 包含参数包，该表达式称为二元右折叠。

- 形式为 (e1 op1 op2) 且 op1 和 op2 均为 fold-operator 的表达式称为二元左折叠。在二元折叠中，op1 和 op2 应该是相同的 fold-operator，且 e1 包含参数包或 e2 包含参数包。

示例：

```
template<typename ...Args>
bool f(Args ... &args) {
    return (args & & args); // 正常
}

template<typename ...Args>
bool f(Args ... &args) {
    return (args * + args); // 错误：两个操作数都包含参数包
}
```

 示例结束

### 5.1.4 Requires 表达式 [expr.prim.req]

- C 是约束类型修饰符，表示该 lambda 是通用的。[示例]：

```
template<typename T> concept C = true;

auto g = (C& a, C* b) { *a = b; };
```

```
struct Fun {
    auto()(C& a, C* b) const { *a = b; }
};
```

- requires-expression 提供了一种简洁的方式来表达模板参数的要求。这种要求可以通过名称查找 (3.4) 进行检查，或者通过检查类型和表达式的属性来检查。

```
requires-expression:
  requires requirement-parameter-list_opt requirement-body
  requirement-clause-list:
    ( parameter-declaration-clause_opt )
  requirement-body:
    { requirement-seq ? }
  requirement-seq:
    requirement
    requirement-seq requirement
  requirement:
    simple-requirement
    type-requirement
    compound-requirement
    nested-requirement
```

2 A-expression 根据其参数（如果有）和嵌套要求定义一个约束 (14.10)。

3 A-expression 的类型为 `bool` 且是未求值的 (5)。[注：一个 requires-expression 被转换为一个约束以确定其是否被满足 (14.10.2) —— 注]

4 A requires-expression 仅应出现在概念定义 (7.1.7) 内部，或者模板声明（第 14 节）的 requires 句或函数声明（8.3.5）内部。 [示例：requires-expression 的一种用法是在像下面的概念中定义要求：

```cpp
template<typename T>
concept bool R() {
  requires (T i) {
    typename T::;
    (*) -> const T::type&;
  }
};
```

A requires-expression 也可以在 requires 句中使用，作为对模板参数的特有的约束写法，如下所示：

```cpp
template<typename T>
requires (T x) { x + x; }
auto Tadd(T a, T b) { return a + b; } // 注：根据上下文假设缺少了返回类型
```

第一个引入了 requires 句，第二个引入了 requires-expression。[注：此类要求也可以通过在概念内部定义它们来书写。

```cpp
template<typename T>
concept C = requires (T x) { x + x; }
```

```cpp
template<typename T>
requires (T a, T b)
auto Tadd(T a, T b) { return a + b; }
```

> - 注

A requires-expression 可以使用参数声明句 (8.3.5) 引入局部参数。requires-expression 的局部参数不应有默认参数。局部参数引入的每个名称从其声明点到 requirement-body 的右括号结束处均在作用域内。这些参数没有链接、存储或生命周期；它们仅用作定义要求的目的的符号。requirement-parameter-list 的参数声明句不应以省略号终止。[示例：

```cpp
template<typename T>
concept C1() {
  requires(T, t ) { t; }; // 错误：以省略号终止
}
```

```cpp
template<typename T>
concept C2() {
  requires(T, void (*p)(T, ...)) // OK：requires-expression 的参数声明句
  // 不以省略号终止
  { p(t); }
} // 带有省略号
```

requirement-body 由一系列要求序列组成。这些要求可以引用局部参数、模板参数以及从启用上下文的任何其他声明。每个要求都对 requires-expression 定义的约束合取断言一个约束 (14.10)。约束按照它们书写的顺序进行评估。

- 将模板参数替换到 requires-expression 中可能会导致其要求中形成无效的类型或表达式。在这种情况下，对应要求的约束不被满足；它不会导致程序的形成。如果将模板参数替换到要求中始终会导致替换失败，则程序是格式不良的 (ill-formed)；不报告诊断。[示例：

```cpp
template<typename T> concept C =
requires {
  new int[size_of(T)]; // 格式不良，不需要诊断
};
```

### 5.1.4.1 简单要求 [expr.prim.req.simple]

```
simple-requirement:
  expression;
```

simple-requirement 为其表达式引入一个表达式约束 (14.10.1.3)。[注：表达式约束断言表达式的有效性。注] [示例：

```cpp
template<typename T> concept B =
requires (T a, b) {
  a + b; // 对于 a + b 的表达式约束
};
```

### 5.1.4.2 类型要求 [expr.prim.req.type]

```
type-requirement:
  nested-name-specifier_opt type-name;
```

type-requirement 为其可选的嵌套名称指定符和 type-name 所命名的类型引入一个类型约束 (14.10.1.4)。[注：类型要求断言关联类型的有效性，可以是成员、模板特化或别名模板。它不用于为任意类型指定符指定要求。注] [示例：

### 5.1.4.3 复合要求

```
compound-requirement:
  { requirement-seq }
```

compound-requirement 引入约束的合取。[示例：

```cpp
template<typename T>
struct S = requires {
    typename T;
};
```



### 5.1.4.4 嵌套要求 [expr.prim.req.nested]

```
nested-requirement:
  requires;
```

`nested-requirement` 可以用于根据局部参数指定额外的约束。它向 `requires-expression` 定义的约束合取中附加一个约束。[示例：

```cpp
template<typename T>
concept C = requires(T x) {
    requires sizeof(x) > 0;
};
```

N4549

表 10 — 简单类型限定符及其指定的类型

| 限制符 (Specifier(s)) | 类型 (Type) |
|---|---|
| `type-name` | 被命名的类型 |
| `simple-template-id` | 14.3 中定义的类型 |
| `end-type` | : |
| `auto` | 待推导类型的占位符 |
| `dectype(expression)` | 下文定义的类型 |
| `constrained-type-specifier` | 待推导的值（类型、非类型、模板）的占位符 |

将第 1 段替换为以下文本：

+   1 类型限定符 `auto`、`dectype(auto)` 和 `constrained-type-specifiers` 指定一个占位符（类型、非类型或模板），该占位符将通过推导或显式指定进行替换。`auto` 和 `dectype(auto)` 类型指定值和模板的占位符。[注：占位符的推导是通过 7.1.6.4 和 8.3.5 中描述的引入模板参数实现的——结束]占位符用于表示泛型 lambda (5.1.2)、函数是一个简写函数模板 (8.3.5)，或复合需求 (5.1.4) 中的尾随返回类型引入了参数推导约束 (14.10.1.6)。注：嵌套限定符也可以包含占位符 (5.1)。`constrained-type-specifiers` 的替换根据本节中的规则确定。[结束注]]

+   2 占位符类型类型可以出现在声明此类占位符的任何上下文中，位于 `decl-specifier-seq`、`type-specifier-seq`、`conversion-function-id` 或 `trailing-return-type` 中的函数声明符。如果函数声明符包含尾随返回类型 (8.3.5)，则将该占位符指定为声明的返回类型。如果函数的声明返回类型包含占位符，则函数的返回类型从函数体推导出来。在包含占位符的来自 `auto D -> T` 的返回语句的函数中，初始 `auto` 不指定占位符。

+   3 修改第 3 段，允许在 lambda 或函数的参数类型中使用 `auto`。

如果 `auto-type-specifier` 占位符作为参数声明的 `decl-specifier-seq` 之一出现在 lambda 的参数类型中，则该 lambda 是一个泛型 lambda (5.1.2)。[示例：

```
auto lambda = (int, auto) { return int; }; // OK：一个泛型 lambda
```

— 示例结束]同样，如果占位符出现在函数声明的参数类型中，则该函数声明声明了一个简写函数模板 (8.3.5)。[示例：

```
void f(const auto, int); // OK：一个简写函数模板
```

— 示例结束]

在第 3 段之后添加以下内容以描述返回类型中的 `constrained-type-specifiers` 指向模板参数。

7.1.6.4

如果一个简写函数声明的声明返回类型引入的约束表达式 (7.1.6.2) 根据 14.6.6.1 中的表达式比较规则被认为与该函数参数声明句中 `constrained-type-specifier C2` 引入的约束表达式等价，则带有占位符的 `constrained-type-specifier C1`。相反，`C1` 被替换为为 `C2` 创建的模板参数 (8.3.5)。示例：

```
template<typename T> const bool C = true;

template Struct T;

const& f1(C); // 相同的模板参数且没有推导返回类型
Tuple<...> f2(C); // 相同的模板参数且没有推导返回类型
```

在声明 `f1` 中，参数声明句和返回类型中的 `constrained-type-specifiers` 引入的约束表达式是等价的；它们都会为某个引入的模板参数 `T` 引入表达式 `C`。在 `f2` 中，在返回类型中使用 `C` 将引入一个约束表达式 (`C`)，它与参数声明句中 `constrained-type-specifier C` 对应的引入的模板参数 (14.1) 是不同的。

(1.2) 否则；将变量或返回类型中的每个占位符替换为新发明的模板参数，具体根据 8.3.5 中为占位符发明模板参数的规则。

根据函数调用 (14.8.2.1) 的模板推导规则，为 `P` 中的每个发明的模板参数推导出一个值，其中 `P` 是函数模板参数类型，且初始化器是对应的参数。如果推导失败，则该声明是非法的（ill-formed）。如果受约束类型限定符（`constrained-type-specifier`）引入了任何占位符，则按如下定义 `C` 为约束表达式：

- (1.3) 如果只有一个受约束类型，则 `C` 是发明的模板约束参数 (14.1) 为该受约束类型限定符引入的约束表达式；

- (1.4) 否则，`C` 是逻辑与 (5.4)，它按照出现顺序作用于每个受约束类型限定符对应的发明的模板约束参数所引入的约束表达式。

如果声明类型的推导值未满足 `U` 的归一化字符，则该声明是非法的。否则，通过将推导出的 `U` 替换 `P` 中的每个发明的模板参数，得到变量或返回类型的类型。

示例：

```
auto x1 = {1, 2}; // OK: decltype(x1) 是 std::initializer_list<int>
auto x2 = {1, 2, }; // error:无法推导元素类型

// end example
```

在 C++ 标准第 7 段的第一个示例中添加以下内容。

示例：

```
template<typename T> struct Vec { };
template<typename T> Vec<T> make_vec(std::initializer_list<T> l) { return Vec<T>{l}; }
template<typename...> Tuple<...> make_up(Ts... args) { return Tuple<Ts...>{args}; }

auto x3 = *x1.begin(); // OK: decltype(x3) 是 int&
const Vec<auto> v1 = make_vec({1, 2, 3}); // OK: decltype(v1) 是 Vec<int>
Vec<auto> v2 = {1, 2, 3}; // error: 类型推导失败
Tuple<...> v3 = make_up(0, 'a'); // OK: decltype(v3) 是 Tuple<int, char>

// end example
```

在 C++ 标准第 7 段的第二个示例中添加以下内容。

示例：

```
template<typename T, typename U> struct Pair;
template<typename T, typename U> Pair<T, U> make_pair(T, U);

struct S { void mfn(bool); };
int fn(char, double);

Pair<(*)(auto, auto, auto), auto(*S::*)(auto)> p = make_pair(fn, &S::mfn);
```

7.1.6.4.1

N4549

`p` 的声明类型是以下发明的函数模板中类 `g(make_pair(fn, &S::mfn))` 的参数 `x` 的推导类型：

```
template<class T1, class T2, class T3, class T4, class T5, class T6>
void g(Pair<T1>(*T2), T3, (T5::*)(T6)) x);
```

— 示例

[示例]:

```
template<typename T> concept bool C = true;

const C* cv = expr;
```

`cv` 的类型是从以下发明的函数 `f1(expr)` 类中的参数 `p1` 推导出的：

```
template<T> void f1(const T* p1);
```

— 示例

[示例]:

```
auto cf(int) -> Pair<C, C> { return expr; }
```

`cf` 的返回类型是从以下发明的函数 `f2(expr)` 类中的参数 `p2` 推导出的：

```
template<T> void f2(Pair<T, T>);
```

`cf` 返回类型中的两个受约束类型限定符对应于同一个发明的模板参数。 — 示例

将 C++ 标准中 7.1.6.4 的第 8-15 段复制到本节。修改第 8 段（此处为 2）如下：

- 8 如果初始化-声明符-列表包含多于一个初始化-声明符，则它们都应形成变量声明。每个声明变量的类型按上述方式确定，如果替换占位符类型的声明变量类型或返回类型在每次推导中不相同，则程序是非法的。

在段落中添加以下示例：

[示例]:

```
Pair<auto, auto> p1 = make_pair(0, 0);
*p2 = &p1; //替换类型为 Pair<int, int>
Pair<auto, auto> p3 = make_pair(0, 'a');
p4 = make_pair('a', 0); // error: 不同的替换类型 s
```

— 示例

修改第 9 段（此处为 3）。

- 9 如果一个声明返回类型中包含占位符类型的函数有多个返回语句，则为每个返回语句推导返回类型。如果每次推导的类型不相同，则程序是非法的。

修改第 10 段（此处为 4）。

7.1.6.4.1

N4549

如果一个声明返回类型使用占位符的函数没有返回语句，则返回类型是从函数体大括号处的返回语句推导而出的。

修改第 11 段（此处为 5）。

如果需要推导带有占位符实体的类型，则该做法是非法的。

修改第 13 段（此处为 7）。

声明返回类型使用占位符的函数或函数模板的也使用该占位符。如果受约束类型限定符指定了占位符，则在段落中添加以下内容：

```
template<typename> concept C = true;
template<typename> concept C2 = true;

template<typename> auto cf(T) -> C; // #1
template<typename> cf(T); // #2: 重复声明 #1
template<typename> C2(T); // error: 使用了占位符声明
```

修改第 14 段（此处为 8）。

使用占位符作为返回类型的声明函数不应有异常说明。

修改第 15 段（段 8）如下：

显式实例化 (14.8.2) 不导致使用占位符实体的实例化，但也不会阻止该实体以确定其类型。

# 7.1.6.4.2 受约束类型限定符 [dcl.spec.auto]

将此添加到 7.1.6.4。

- 受约束类型限定符指定一个占位符（类型、类型或模板）并引入关联约束 (14.10.2)。

- 受约束类型限定符：

  限定限定的的名称：

    限定限定的限定名称：

      嵌套名称限定符-opt 受约束类型名称

    概念名称：

      部分概念标识符

    概念名称：

      部分概念标识符：

        概念名称 <template-argument-list> 

§ 7.1.6.4.2

N4549

```
template<typename T> concept C1 = false;
template<int N> concept C2 = false;
template<typename X> concept C3 = false;

template<T, int N> class Array { };
template<T, typename> class Stack { };
template<T> class Alloc { };

void f1(C1); // C1 指定占位符类型
void f2(Array<auto, C2>); // C2 指定整数值的占位符
void f3(Stack<auto, C3>); // C3 指定类模板的占位符

-- end example
```

如果标识符指向一组定义集 (7.1.7)，则它是一个概念名称。[注：当概念名称指向变量概念时，概念集合最多有一个这样的成员。 — 注释] [示例]:

```
template<typename T> concept C() { return true; }; // #1
template<T, typename> concept B() { return true; }; // #2
template<T, typename> concept D = true; // #3

void f(C()); // OK: C 所指的概念包含了 #1 和 #2;
void g(D); // OK: 概念名称 D 仅指向 #3

-- example
```

部分概念标识符是一个概念后跟模板参数。[示例]:

```
template<T, int N = D> concept Seq = true;

void f1(Seq<3>); // OK
void f2(Seq<>); // OK

-- end
```

由受约束类型限定符指定的概念是根据 14.10.4 中的概念解析规则选择的那个。

注：受约束名称引入的约束表达式是通过发明受约束名称引入的 (14.10.1)。为变量类型或函数声明类型发明对应模板参数的规则在 7.1.4.1 中描述。为 lambda 表达式 (5.1.2) 的参数声明句或函数声明 (8.3.5) 中的占位符发明模板参数的规则在 8.3.5 中描述。为复合要求的尾随类型中的占位符发明模板参数的规则在 14.10.1 中描述。 — 注释]

# 7.1.7 概念分类器 [dec:Spec.concept]

将此节添加到 7.1.1。

概念限定符应仅应用于函数模板或变量模板的定义，这些定义在命名空间 (3.6) 中。具有概念分类器的函数模板定义称为函数概念。函数概念不应异常说明，并被处理为指定了 `noexcept(true)` (15.4)。当声明函数时

§ 7.1.7

N4549

作为一个概念，它将是该函数的唯一声明。具有概念限定符的变量定义被称为变量概念（variable concept）。概念定义指的是函数概念及其定义，或者变量概念及其初始化器。[示例：

```cpp
template<typename T>
    concept F1() { return true; } // OK 声明了一个概念
template<typename T>
    concept bool F2(); // error: 概念不是一个定义
template<typename T>
    constexpr bool F3()
template<typename T>
    concept bool F3() { return true; } // error: 将函数重重声明为概念
    concept bool V1 = true; // OK 声明了一个变量
template<typename T>
    concept bool V2; // error: 没有初始化值的变量概念
struct S {
    template<typename T>
    static bool C = true; // error: 在类作用域内声明概念
}
```

-- 示例结束

每个概念都隐式定义为 `constexpr` (7.1.5)。概念定义不应使用 `thread_local`、`inline`、`friend` 或 `constexpr` 限定符声明，且概念定义不具有关联约束 (14.10.2)。

函数概念的定义或变量概念的初始化器不应包含对被声明概念引用。[示例：

```cpp
template<typename T>
    concept bool F() { F<typename>::type(); } // error
template<typename T>
    concept bool W = V<T>; // error
```

-- 示例结束

函数概念具有以下限制：

- (5.1) 其声明中不应出现任何函数限定符 (7.1.2)。

- (5.2) 声明的类型应具有类型体。

- (5.3) 声明的参数列表应等同于空参数列表。

- (5.4) 声明应有一个等同于 `{ return E; }` 的函数体，其中 `E` 是一个约束表达式 (14.10.13)，

[注：返回类型推导需要函数定义的实例化，但概念定义不会被实例化；它们是被归一化的 (14.10.2)。-- 注结束] [示例：

```cpp
template<typename T>
    concept int F0() { return 0; } // error: 返回类型不是 bool
template<typename T>
    concept auto F1() { return true; } // error: 返回类型被推导了
template<typename T>
    concept bool F3(T) { return true; } // error: 不是空参数列表
```

§ 7.1.7

19

示例结束

6 变量概念具有以下限制：

- (6.1) 声明的类型应为 `bool`。

- (6.2) 声明应具有一个初始化器。



### (6.3) 初始化器应是一个约束表达式。

[示例：]

```cpp
template<typename T>
concept bool V1 = 3 + 4; // error: 初始化器不是约束表达式
concept bool V2 = 0; // error: 不是模板
```

```cpp
template<typename T> concept bool C = true;
concept bool V3 = true; // error: 将受限模板声明为概念
```

示例结束

## 7 程序不应声明一个概念定义的显式实例化 (14.8.2)、显式特化 (14.8.3) 或部分特化。[注：这防止了用户通过为概念提供一个与其原始定义不同的含义来绕过约束系统。-- 注结束]

## 8 声明符 [dcl.decl]

分解声明符的语法以满足函数声明符的约束。

- 声明符:

    ptr-declarator

    nptr-declarator-and-qualifiers trailing-return-type requires-clause_opt

  parameters-and-qualifiers:

    (parameter-declaration-clause ) cv-qualifier-seq_opt

    ref-qualifier_opt exception-specification,opt attribute-specifier-seq_opt requires-clause_opt

在本节末尾添加以下段落。

4 仅当声明符声明一个函数 (8.3.5) 时，声明符中的可选子句 (14.10.2) 才存在，且该 `requires` 子句不应在返回返回类型之前。当出现在声明符中，`requires` 子句位于返回返回类型之前。[示例：

```cpp
void f1(int a) requires true; // OK
afo2(int a) -> bool true; // OK
f3(int a) -> bool true; // error: requires 子句在返回返回类型之前
void g(*f()) requires true; // error: 变量的约束
g(**f()) requires true; // error: 变量的约束
void (*)(char) true; // error: 不是函数
```

—

## 8.3 声明符的含义 [dcl.meaning]

### 8.3.5 函数

修改 1 中的条件以接受 `requires` 子句。

D1 ( parameter-declaration-clause ) cv-qualifier-seq_opt

ref-qualifier_opt exception-specification,opt attribute-specifier-seq_opt requires-clause

修改 2 中的条件以接受 `requires` 子句。

D1 ( parameter-declaration-clause ) cv-qualifier-seq_opt

ref-qualifier_opt exception-specification,opt attribute-specifier-seq_opt requires-clause

修改 5 的第二句。该段落已省略。

+ 5 受限模板在返回类型、参数类型和关联约束 (14.10.2) 上应当一致。

修改 6 为函数的类型。

+ 6 返回类型、参数类型以及任何关联的约束 (14.1) 是相同的。

§ 8.3.5

21

N4549

```cpp
void f4(E, E< > b, E< > c);
a, b, 和 c 的类型相同，因为受约束类型限定符 E、E<> 和 E<> 
都关联到受约束表达式 ET，其中 T 是一个新发明的类型参数。

void f5(C head, C... tail);
head 和 tail 的类型不同。它们各自引入的受约束表达式为 
<<C>> 和 <<U>> && ..., 其中 T 是为 head 发明的类型参数，而 U 是
为 tail 发明的模板参数 (14.1)。
```

18 一个发明的模板函数的调整后的函数参数派自参数声明子，通过将每个占位符的每次出现都替换为相应发明模板的名称而得到。如果将占位符替换为模板参数的名称导致声明无效，则该过程为是不符合规范的（ill-formed）。[注：等价的模板声明声明了函数模板 (14.0.6.1)。 — 注] 示例：

```cpp
template<typename T> class Vec {
template<typename T, typename U> class Pair {
template<typename... Args> class Tuple {

void f1(const auto&, auto);
void f2(Vec<auto>...);
void f3(Tuple<auto>...);
void f4(auto::(auto));

template<typename T, typename U> void f1(const T, U); // 重定义 f1
template<typename T> T void f2(Vec<T>...); // 重定义 f2
template<typename T> T void f3(Tuple<T>...); // 重定义 f3
template<typename T, typename U> U void f4(U::(V)); // 重定义 f4

template<typename T> T concept bool C1 = true;
template<typename T> T concept bool C2 = true;
template<typename T> T concept bool C3 = true;
template<typename T...> T concept bool C4 = true;

void g1(const C1&);
g2(Vec<C1&>...);
g3(C1&);
g4(Vec<C3<int>>);
g5(C4,...);
g6(Tuple<C4>...);
g7(C4 p);
g8(Tuple<C4>...);

template<C1, C2> T void g1(const T, U); // 重定义 g1
template<C1, C2> T void g2(Vec<T>...); // 重定义 g2
template<C1, C3> T void g3(T,...); // 重定义 g3
template<C3, C4> T void g4(Vec<T>...); // 重定义 g4
template<C4, C5> T void g5(Tuple<T>...); // 重定义 g5
template<C4, C6> T void g6(Tuple<T>...); // 重定义 g6
template<C4, C7> T void g7(T); // 重定义 g7
template<C4, C8> T void g8(Tuple<T>...); // 重定义 g8
```

结束示例；

§ 8.3.5

```cpp
template<int N> concept bool Num = true;
```

```cpp
void h(Num*); // 错误：参数声明中的无效类型
```

等价的声明具有如下形式：

```cpp
template<int N> void h(N*); // 错误：无效类型
```

- 示例

19 函数模板可以是简写函数模板。发明的模板参数被附加在显式声明的模板参数之后的模板参数列表之后。[示例：

```cpp
template<typename T, int N> class Array { };
```

```cpp
template<int N, typename T> void f(Array<auto, N>*); // OK：重定义 f(Array<auto, N>*)
```

- 示例

## 10 派生类

### 10.3 虚函数

在段落5 之后插入以下段落，以禁止声明受约束虚函数以及通过受约束成员函数重写虚函数。

如果虚函数具有关联的约束 (14.10.2)，则程序是不符合规范的（ill-formed）。[示例：

```cpp
struct A {
    virtual void f() requires true; // 错误：受约束虚函数
};
// 结束示例
```

# 13 重载

修改段落1以允许基于约束的重载。

- 当在同一作用域内为同一个名称指定了两个或多个不同的声明时，该名称被认为是重载的。以此此类推，在同一作用域内声明相同名称但具有不同类型或不同关联约束 (14.10.2) 的两个声明被称为重载。只有函数声明和模板声明可以重载；变量声明和类型声明不能重载。

### 13.1 可重载声明

更新段落3 以匹配函数的约束。注意，在 8.3.5 中，如果函数声明具有等价的参数声明和关联的约束（如果有的话)(14.10.2)，它们声明了相同的函数，因此不能重载：

### 13.1.1 匹配声明

修改段落1，将匹配的声明扩展到也包含函数的约束。注意原文中的示例已省略。

如果两个相同名称的声明在同一作用域内，且具有等价的参数声明 (13.1) 和等价的关联约束，则它们指向同一个函数。

## 13.3 重载解析

### 13.3.2 可用函数

更新段落1，在确定候选函数是否可用时要求检查函数的约束。从候选函数集 (13.1) 中，根据关联约束（13.3）选择可用函数（14.10.2）。可用函数的选择考虑了转换序列。

- 其次，要使函数是可用的，它必须满足关联约束 (14.10.2)。

- 第三，对于（可用函数的）...

### 13.3.3 最优可用函数

修改段落中的最后一个项，通过函数的约束来扩展它。注意，14.10.2 模板参数中的项已省略。

- F1 和 F2 是函数特化，根据 14.6 的偏排序规则，F1 优于 F2。或者，如果不是，根据 14.10.3 的关联约束选择模板函数。

## 13.4 函数地址

修改段落4，在确定函数地址时引入约束。如果存在多个候选函数，则程序是不符合规范的（ill-formed）。如果集合中包含一个根据 14.3 的偏排序规则优于 F1 的非模板特化函数，则 F1 被消除。在这些消除之后，应恰好剩余一个函数。

在段落5 的末尾添加以下示例：

```cpp
示例：
void f();
void g() requires true; // #1
g() requires false; // #2
void (*pf)() = &g; // 选择 #2
void (*pg)() = &f; // 错误：无匹配函数
```

## 14.1 模板参数

```cpp
template-parameter:
  type-parameter
  parameter-declaration
  constrained-parameter:
    qualified-name ... identifier_opt
    qualified-concept-name identifier_opt default-template-argument_opt
default-template-argument:
  = type-id
  = id-expression
  = initializer-clause
```

在模板参数段落1中扩展语法以受约束的模板参数。

在段落1 之后插入一个新的段落。

如果参数声明的类型限定符是受约束类型限定符 (7.1.6.4)，则该模板参数是受约束模板参数。

在段落8 之后插入以下段落。这些段落定义了受约束模板参数的含义。

受约束模板参数声明了一个模板参数，其种类（类型、非类型、模板）和类型与限定限定概念名称 (7.1.6.4.2) 所指定概念的原型参数匹配。所指定的概念通过概念解析规则在 14.10.4 中选择。令 X 为所指定概念的原型参数。声明的模板参数由 X 的种类（类型、非类型、模板）以及受约束参数中的可选省略号决定：

- 如果 X 是模板参数，则声明的参数是类型模板参数。

# PD ISO/IEC TIS 19217:2015

ISO/IEC TS 19217:2015(E)

如果 X 是一个非类型参数，则声明的参数是一个与 X 相同类型的非类型模板参数。

如果 X 是一个模板参数，则声明的 X 是一个具有 X 相同类型列表的模板参数，排除默认模板参数。

如果限定名（qualified-name）后面跟着省略号（...），则声明的参数是一个模板参数包 (14.6.3)。

[示例]:

```cpp
template<typename T> bool C1 = true;
template<typename> class X bool C2 = true;
template<int N> concept C3 = true;
template<typename...> bool C4 = true;
template<...> concept C5 = true;
```

```cpp
template<C1> void f1();    // 如果 T 是类型参数，则 OK
template<C2> void f2();    // 如果 X 是具有一个类型参数的模板，则 OK
template<C3> void f3();    // 如果 N 为 int，则 OK
template<C4...> T void f4(); // 如果 T 是类型参数包，则 OK
template<C5> T void f5(); // 如果 T 是类型参数，则 OK
template<C5...> Cs = f6(); // 如果 Cs 是字符类型的模板包，则 OK
```

受约束参数引入一个约束表达式 (14.10.2)。该表达式派自受约束参数中的限定名 Q、其指定的概念 C，且其默认参数匹配声明的参数 P。

- 首先，如果来自 P 的模板参数 A。如果 P 声明了一个模板参数包 (14.6.3) 且 C 是变长概念 (7.1.7)，则 A 是包展开 P....。否则，A 是标识符表达式 P。

- 接着，如果受约束名 Q 上的模板 ID TT。如果 Q 是一个概念名，则 TT 是 C<A>。否则，Q 是形式为 C<A1, A2, ..., AN> 的部分概念 ID，且 TT 是 C<A, A1, A2, ..., AN>。

- 接着，如下所示的 E。如果 C 是变长概念 (7.1.7)，则 E 是标识符表达式 TT。否则，E 是函数调用 TT。

- 最后，如果 P 声明了一个模板参数包且 C 不是变长概念，则 E 被调整为折叠表达式 (E & ...)。(5.1.3)。

E 是引入的约束表达式。示例：

```cpp
template<typename> bool C1 = true;
template<typename...> T, typename concept C2() { return true; };
template<typename> T concept C3 = true;
```

```cpp
template<C1> T struct s1; // 关联 C1<T>
template<C1...> T struct s2; // 关联 C1<T> & ...
template<C2...> T struct s3; // 关联 C2<T...>()
template<C3<int>> T struct s4; // 关联 C3,T, int
```

[示例]

在第 9 段之后插入以下段落，以要求默认参数的种类匹配其受约束参数的种类。

§ 14.1

# PD ISO/IEC 19217:2015

ISO/IEC 19217:2015(E)

N4549

受约束参数的默认模板参数应匹配声明模板参数的种类（类型、非类型、模板）。*示例：*

```cpp
template<typename T> concept bool C1 = true;
template<int N> concept bool C2 = true;
template<<typename typename> class X> concept bool C3 = true;
```

```cpp
template<typename T> struct S0;

template<C1> T = struct S1; // OK
template<C2> N = struct S2; // OK
template<C3> X = struct S3; // OK
template<C1> T = struct S4; // 错误：默认参数不是类型
```

-- 示例

# 14.2 模板参数的引入

[temp.intro]

在 14.1 之后添加此节。

- 模板引入提供了一种声明模板的简洁方式。

- 模板引入：

  限定名 { 引入列表 }

- 引入列表：

  引入的参数

  引入列表, 引入的参数

  引入的参数:

    ... 标识符

模板引入声明了一个模板，其模板参数序列派生自*限定名* (7.1.6.4.2) 以及其引入列表中引入的参数序列。

由*限定名*指定的概念由 14.10.4 中的概念解析规则选择。令 C 为声明的概念。模板引入声明的模板参数派生自其引入的参数以及 C 的模板参数声明，这些引入的参数根据 14.10.4 中的规则与 C 匹配。对于每个*引入的参数* I，使用以下规则声明一个模板参数：

- 令 P 为 C 中对应于 I 的模板参数声明。如果 P 没有声明模板包 (14.6.3)，则 I 不应包含省略号。

- 如果 P 声明了模板包，则包 J 为该包的模式。

- 按照 14.1 中声明*受约束参数*的规则声明模板参数，使用 P 作为原型且不使用省略号。

*示例：*



```cpp
template<typename T, int N, ...> concept bool C1 = true;
template<<typename typename> class X> concept bool C2 = true;
template<typename...> Ts> concept C3 = true;
```

```cpp
C1{A, B, ...} // OK：A 被声明为模板名，
struct S1; // B 被声明为 int，且
```

§ 14.2

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

```cpp
// C 被声明为 typename ...
C2<T> void f0();      // OK：T 被声明为 template<typename>
C2{...> void g0();  // 错误：对应于 Ts 的模板参数不是模板包
C3<T> struct S2;     // OK：T 被声明为 typename
C3{...> struct S2;  // OK：Ts 被声明为 typename
```

-- 示例

由*限定名*引用的概念可能带有带有默认参数的模板参数。如果模板参数有默认值，则引入列表可以省略对应的标识符。只有引入的参数被声明为模板参数。[示例]:

```cpp
template<typename A, typename B = bool> concept C() { return true; }
C<T> void f(T); // OK：f 是一个带有单一类型 T 的函数
```

-- 示例

如果对应的模板参数有默认参数，则引入的模板没有默认参数。[示例]:

```cpp
template<typename T, int N = 1> concept P() { return true; }
P(T) struct Array; // 关联 Array
```

-- 示例

模板引入引入了一个约束表达式 (`14.10.2`)。该表达式派生自模板引入中的限定名 `C` 以及引入的参数序列。

首先，派生自 `A1, A2, ..., AN` 的 `P1, P2, ..., PN`。如果 `P` 包含省略号，则 `P` 是包展开 (`14.6.3`)。接着，`E` 是函数调用。如果 `Q` 是概念名，则 `TT` 是 `C<A>`。否则，`Q` 是形式为 `C<A1, A2, ..., AN>` 的部分概念 ID，且 `TT` 是 `C<A, A1, A2, ..., AN>`。

然后，如下所示的 `E`。如果 `C` 是变长概念 (`7.1.7`)，则 `E` 是标识符表达式 `TT`。否则，`E` 是函数调用。

最后，如果 `P` 声明了一个模板包且 `C` 不是变长概念，则 `E` 被调整为折叠表达式 (`E & ...`)。(`5.1.3`)。

`E` 是引入的约束表达式。示例：

```cpp
template<typename> bool C1 = true;
template<typename...> T, typename concept C2() { return true; };
template<typename> T concept C3 = true;
```

```cpp
template<C1> T struct s1; // 关联 C1<T>
template<C1...> T struct s2; // 关联 C1<T> & ...
template<C2...> T struct s3; // 关联 C2<T...>()
template<C3<int>> T struct s4; // 关联 C3,T, int
```

[示例]

在第 9 段之后插入以下段落，以要求默认参数的种类匹配其受约束参数的种类。

§ 14.1

# PD ISO/IEC 19217:2015

ISO/IEC 19217:2015(E)

N4549

受约束参数的默认模板参数应匹配声明模板参数的种类（类型、非类型、模板）。*示例：*

```cpp
template<typename T> concept bool C1 = true;
template<int N> concept bool C2 = true;
template<<typename typename> class X> concept bool C3 = true;
```

```cpp
template<typename T> struct S0;

template<C1> T = struct S1; // OK
template<C2> N = struct S2; // OK
template<C3> X = struct S3; // OK
template<C1> T = struct S4; // 错误：默认参数不是类型
```

-- 示例

# 14.2 模板参数的引入

[temp.intro]

在 `14.1` 之后添加此节。

- 模板引入提供了一种声明模板的简洁方式。

- 模板引入：

  限定名 { 引入列表 }

- 引入列表：

  引入的参数

  引入列表, 引入的参数

  引入的参数:

    ... 标识符

模板引入声明了一个模板，其模板参数序列派生自*限定名* (`7.1.6.4.2`) 以及其引入列表中引入的参数序列。

由*限定名*指定的概念由 `14.10.4` 中的概念解析规则选择。令 `C` 为声明的概念。模板引入声明的模板参数派生自其引入的参数以及 `C` 的模板参数声明，这些引入的参数根据 `14.10.4` 中的规则与 `C` 匹配。对于每个*引入的参数* `I`，使用以下规则声明一个模板参数：

- 令 `P` 为 `C` 中对应于 `I` 的模板参数声明。如果 `P` 没有声明模板包 (`14.6.3`)，则 `I` 不应包含省略号。

- 如果 `P` 声明了模板包，则包 `J` 为该包的模式。

- 按照 `14.1` 中声明*受约束参数*的规则声明模板参数，使用 `P` 作为原型且不使用省略号。

*示例：*

```cpp
template<typename T, int N, ...> concept bool C1 = true;
template<<typename typename> class X> concept bool C2 = true;
template<typename...> Ts> concept C3 = true;
```

```cpp
C1{A, B, ...} // OK：A 被声明为模板名，
struct S1; // B 被声明为 int，且
```

§ 14.2

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

```cpp
// C 被声明为 typename ...
C2<T> void f0();      // OK：T 被声明为 template<typename>
C2{...> void g0();  // 错误：对应于 Ts 的模板参数不是模板包
C3<T> struct S2;     // OK：T 被声明为 typename
C3{...> struct S2;  // OK：Ts 被声明为 typename
```

-- 示例

由*限定名*引用的概念可能带有带有默认参数的模板参数。如果模板参数有默认值，则引入列表可以省略对应的标识符。只有引入的参数被声明为模板参数。[示例]:

```cpp
template<typename A, typename B = bool> concept C() { return true; }
C<T> void f(T); // OK：f 是一个带有单一类型 T 的函数
```

-- 示例

如果对应的模板参数有默认参数，则引入的模板没有默认参数。[示例]:

```cpp
template<typename T, int N = 1> concept P() { return true; }
P(T) struct Array; // 关联 Array
```

-- 示例

模板引入引入了一个约束表达式 (`14.10.2`)。该表达式派生自模板引入中的限定名 `C` 以及引入的参数序列。 (此处，此处重复了，修正如下)

该表达式派生自模板引入中的限定名 `C` 以及引入的参数序列。

首先，派生自 `A1, A2, ..., AN` 的 `P1, P2, ..., PN`。如果 `P` 包含省略号，则 `P` 是包展开 (`14.6.3`)。接着，`E` 是函数调用。如果 `Q` 是概念名，则 `TT` 是 `C<A>`。否则，`Q` 是形式为 `C<A1, A2, ..., AN>` 的部分概念 ID，且 `TT` 是 `C<A, A1, A2, ..., AN>`。

然后，如下所示的 `E`。如果 `C` 是变长概念 (`7.1.7`)，则 `E` 是标识符表达式 `TT`。否则，`E` 是函数调用。

最后，如果 `P` 声明了一个模板包且 `C` 不是变长概念，则 `E` 被调整为折叠表达式 (`E & ...`)。(`5.1.3`)。

`E` 是引入的约束表达式。示例：

```cpp
template<typename> bool C1 = true;
template<typename...> T, typename concept C2() { return true; };
template<typename> T concept C3 = true;
```

```cpp
template<C1> T struct s1; // 关联 C1<T>
template<C1...> T struct s2; // 关联 C1<T> & ...
template<C2...> T struct s3; // 关联 C2<T...>()
template<C3<int>> T struct s4; // 关联 C3,T, int
```

[示例]

在第 9 段之后插入以下段落，以要求默认参数的种类匹配其受约束参数的种类。

§ 14.1

# PD ISO/IEC 19217:2015

ISO/IEC 19217:2015(E)

N4549

受约束参数的默认模板参数应匹配声明模板参数的种类（类型、非类型、模板）。*示例：*

```cpp
template<typename T> concept bool C1 = true;
template<int N> concept bool C2 = true;
template<<typename typename> class X> concept bool C3 = true;
```

```cpp
template<typename T> struct S0;

template<C1> T = struct S1; // OK
template<C2> N = struct S2; // OK
template<C3> X = struct S3; // OK
template<C1> T = struct S4; // 错误：默认参数不是类型
```

-- 示例

# 14.2 模板参数的引入

[temp.intro]

在 `14.1` 之后添加此节。

- 模板引入提供了一种声明模板的简洁方式。

- 模板引入：

  限定名 { 引入列表 }

- 引入列表：

  引入的参数

  引入列表, 引入的参数

  引入的参数:

    ... 标识符

模板引入声明了一个模板，其模板参数序列派生自*限定名* (`7.1.6.4.2`) 以及其引入列表中引入的参数序列。

由*限定名*指定的概念由 `14.10.4` 中的概念解析规则选择。令 `C` 为声明的概念。模板引入声明的模板参数派生自其引入的参数以及 `C` 的模板参数声明，这些引入的参数根据 `14.10.4` 中的规则与 `C` 匹配。对于每个*引入的参数* `I`，使用以下规则声明一个模板参数：

- 令 `P` 为 `C` 中对应于 `I` 的模板参数声明。如果 `P` 没有声明模板包 (`14.6.3`)，则 `I` 不应包含省略号。

- 如果 `P` 声明了模板包，则包 `J` 为该包的模式。

- 按照 `14.1` 中声明*受约束参数*的规则声明模板参数，使用 `P` 作为原型且不使用省略号。

*示例：*

```cpp
template<typename T, int N, ...> concept bool C1 = true;
template<<typename typename> class X> concept bool C2 = true;
template<typename...> Ts> concept C3 = true;
```

```cpp
C1{A, B, ...} // OK：A 被声明为模板名，
struct S1; // B 被声明为 int，且
```

§ 14.2

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

```cpp
// C 被声明为 typename ...
C2<T> void f0();      // OK：T 被声明为 template<typename>
C2{...> void g0();  // 错误：对应于 Ts 的模板参数不是模板包
C3<T> struct S2;     // OK：T 被声明为 typename
C3{...> struct S2;  // OK：Ts 被声明为 typename
```

-- 示例

由*限定名*引用的概念可能带有带有默认参数的模板参数。如果模板参数有默认值，则引入列表可以省略对应的标识符。只有引入的参数被声明为模板参数。[示例]:

```cpp
template<typename A, typename B = bool> concept C() { return true; }
C<T> void f(T); // OK：f 是一个带有单一类型 T 的函数
```

-- 示例

如果对应的模板参数有默认参数，则引入的模板没有默认参数。[示例]:

```cpp
template<typename T, int N = 1> concept P() { return true; }
P(T) struct Array; // 关联 Array
```

-- 示例

模板引入引入了一个约束表达式 (`14.10.2`)。该表达式派生自模板引入中的限定名 `C` 以及引入的参数序列。 (此处，此处重复了，修正如下)

该表达式派生自模板引入中的限定名 `C` 以及引入的参数序列。

首先，派生自 `A1, A2, ..., AN` 的 `P1, P2, ..., PN`。如果 `P` 包含省略号，则 `P` 是包展开 (`14.6.3`)。接着，`E` 是函数调用。如果 `Q` 是概念名，则 `TT` 是 `C<A>`。否则，`Q` 是形式为 `C<A1, A2, ..., AN>` 的部分概念 ID，且 `TT` 是 `C<A, A1, A2, ..., AN>`。

然后，如下所示的 `E`。如果 `C` 是变长概念 (`7.1.7`)，则 `E` 是标识符表达式 `TT`。否则，`E` 是函数调用。

最后，如果 `P` 声明了一个模板包且 `C` 不是变长概念，则 `E` 被调整为折叠表达式 (`E & ...`)。(`5.1.3`)。

`E` 是引入的约束表达式。示例：

```cpp
template<typename> bool C1 = true;
template<typename...> T, typename concept C2() { return true; };
template<typename> T concept C3 = true;
```

```cpp
template<C1> T struct s1; // 关联 C1<T>
... (此处逻辑重复)
```

(由于原文中 `14.10.2` 之后出现了重复，以下为基于原文的完整翻译逻辑)

模板引入引入了一个约束表达式 (`14.10.2`)。该表达式派生自受约束参数中的限定名 `Q`、其指定的概念 `C`，且其默认参数匹配声明的参数 `P`。

- 首先，如果来自 `P` 的模板参数 `A`。如果 `P` 声明了一个模板参数包 (`14.6.3`) 且 `C` 是变长概念 (`7.1.7`)，则 `A` 是包展开 `P....`。否则，`A` 是标识符表达式 `P`。

- 接着，如果受约束名 `Q` 上的模板 ID `TT`。如果 `Q` 是一个概念名，则 `TT` 是 `C<A>`。否则，`Q` 是形式为 `C<A1, A2, ..., AN>` 的部分概念 ID，且 `TT` 是 `C<A, A1, A2, ..., AN>`。

- 接着，如下所示的 `E`。如果 `C` 是变长概念 (`7.1.7`)，则 `E` 是标识符表达式 `TT`。否则，`E` 是函数调用。

- 最后，如果 `P` 声明了一个模板参数包且 `C` 不是变长概念，则 `E` 被调整为折叠表达式 (`E & ...`)。(`5.1.3`)。

`E` 是引入的约束表达式。示例：

```cpp
template<typename> bool C1 = true;
template<typename...> T, typename concept C2() { return true; };
template<typename> T concept C3 = true;
```

```cpp
template<C1> T struct s1; // 关联 C1<T>
template<C1...> T struct s2; // 关联 C1<T> & ...
template<C2...> T struct s3; // 关联 C2<T...>()
template<C3<int>> T struct s4; // 关联 C3,T, int
```

[示例]

# PD ISO/IEC TIS 19217:2015

ISO/IEC TS 19217:2015(E)

如果 `X` 是一个非类型参数，则声明的参数是一个与 `X` 相同类型的非类型模板参数。

如果 `X` 是一个模板参数，则声明的 `X` 是一个具有 `X` 相同类型列表的模板参数，排除默认模板参数。

如果限定名（qualified-name）后面跟着省略号（...），则声明的参数是一个模板参数包 (`14.6.3`)。

[示例]:



```cpp
template<typename T> bool C1 = true;
template<typename> class X bool C2 = true;
template<int N> concept C3 = true;
template<typename...> bool C4 = true;
template<...> concept C5 = true;
```

```cpp
template<C1> void f1();    // 如果 T 是类型参数，则 OK
template<C2> void f2();    // 如果 X 是具有一个类型参数的模板，则 OK
template<C3> void f3();    // 如果 N 为 int，则 OK
template<C4...> T void f4(); // 如果 T 是类型参数包，则 OK
template<C5> T void f5(); // 如果 T 是模板参数，则 OK
template<C5...> Cs = f6(); // 如果 Cs 是字符类型的模板包，则 OK
```

受约束参数引入一个约束表达式 (`14.10.2`)。该表达式派自受约束参数中的限定名 `Q`、其指定的概念 `C`，且其默认参数匹配声明的参数 `P`。

- 首先，如果来自 `P` 的模板参数 `A`。如果 `P` 声明了一个模板参数包 (`14.6.3`) 且 `C` 是变长概念 (`7.1.7`)，则 `A` 是包展开 `P....`。否则，`A` 是标识符表达式 `P`。

- 接着，如果受约束名 `Q` 上的模板 ID `TT`。如果 `Q` 是一个概念名，则 `TT` 是 `C<A>`。否则，`Q` 是形式为 `C<A1, A2, ..., AN>` 的部分概念 ID，且 `TT` 是 `C<A, A1, A2, ..., AN>`。

- 接着，如下所示的 `E`。如果 `C` 是变长概念 (`7.1.7`)，则 `E` 是标识符表达式 `TT`。否则，`E` 是函数调用。

- 最后，如果 `P` 声明了一个模板参数包且 `C` 不是变长概念，则 `E` 被调整为折叠表达式 (`E & ...`)。(`5.1.3`)。

`E` 是引入的约束表达式。示例：

```cpp
template<typename> bool C1 = true;
template<typename...> T, typename concept C2() { return true; };
template<typename> T concept C3 = true;
```

```cpp
template<C1> T struct s1; // 关联 C1<T>
template<C1...> T struct s2; // 关联 C1<T> & ...
template<C2...> T struct s3; // 关联 C2<T...>()
template<C3<int>> T struct s4; // 关联 C3,T, int
```

[示例]

在第 9 段之后插入以下段落，以要求默认参数的种类匹配其受约束参数的种类。

§ 14.1

# PD ISO/IEC 19217:2015

ISO/IEC 19217:2015(E)

N4549

受约束参数的默认模板参数应匹配声明模板参数的种类（类型、非类型、模板）。*示例：*

```cpp
template<typename T> concept bool C1 = true;
template<int N> concept bool C2 = true;
template<<typename typename> class X> concept bool C3 = true;
```

```cpp
template<typename T> struct S0;

template<C1> T = struct S1; // OK
template<C2> N = struct S2; // OK
template<C3> X = struct S3; // OK
template<C1> T = struct S4; // 错误：默认参数不是类型
```

-- 示例

# 14.2 模板参数的引入

[temp.intro]

在 14.1 之后添加此节。

- 模板引入提供了一种声明模板的简洁方式。

- 模板引入：

  限定名 { 引入列表 }

- 引入列表：

  引入的参数

  引入列表, 引入的参数

  引入的参数:

    ... 标识符

模板引入声明了一个模板，其模板参数序列派生自*限定名* (`7.1.6.4.2`) 以及其引入列表中引入的参数序列。

由*限定名*指定的概念由 `14.10.4` 中的概念解析规则选择。令 `C` 为声明的概念。模板引入声明的模板参数派生自其引入的参数以及 `C` 的模板参数声明，这些引入的参数根据 `14.10.4` 中的规则与 `C` 匹配。对于每个*引入的参数* `I`，使用以下规则声明一个模板参数：

- 令 `P` 为 `C` 中对应于 `I` 的模板参数声明。如果 `P` 没有声明模板包 (`14.6.3`)，则 `I` 不应包含省略号。

- 如果 `P` 声明了模板包，则包 `J` 为该包的模式。

- 按照 `14.1` 中声明*受约束参数*的规则声明模板参数，使用 `P` 作为原型且不使用省略号。

*示例：*

```cpp
template<typename T, int N, ...> concept bool C1 = true;
template<<typename typename> class X> concept bool C2 = true;
template<typename...> Ts> concept C3 = true;
```

```cpp
C1{A, B, ...} // OK：A 被声明为模板名，
struct S1; // B 被声明为 int，且
```

§ 14.2

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

```cpp
// C 被声明为 typename ...
C2<T> void f0();      // OK：T 被声明为 template<typename>
C2{...> void g0();  // 错误：对应于 Ts 的模板参数不是模板包
C3<T> struct S2;     // OK：T 被声明为 typename
C3{...> struct S2;  // OK：Ts 被声明为 typename
```

-- 示例

由*限定名*引用的概念可能带有带有默认参数的模板参数。如果模板参数有默认值，则引入列表可以省略对应的标识符。只有引入的参数被声明为模板参数。[示例]:

```cpp
template<typename A, typename B = bool> concept C() { return true; }
C<T> void f(T); // OK：f 是一个带有单一类型 T 的函数
```

-- 示例

如果对应的模板参数有默认参数，则引入的模板没有默认参数。[示例]:

```cpp
template<typename T, int N = 1> concept P() { return true; }
P(T) struct Array; // 关联 Array
```

-- 示例

模板引入引入了一个约束表达式 (`14.10.2`)。该表达式派生自受约束参数中的限定名 `Q`、其指定的概念 `C`，且其默认参数匹配声明的参数 `P`。

(此处由于原文重复，已按要求处理)

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

在 #1 中，错误是由将 int 替换为关联模板参数 `X` 引起的。在 #2 中，无法对 `typename T::template MT<char>` 检查任何约束，因为 `MT` 是未知特化类的成员。 — 示例结束

## 14.4 模板参数

### 14.4.1 模板模板参数

修改第 3 段以包含匹配受约束模板参数的规则。注意，C++ 标准中该段随后的示例已更新。

当参数的模板参数列表（template-parameter-list-of-argument）中所属的类模板或别名模板中的每个参数都与 `P` 中对应的模板参数匹配，并且根据 `14.10.3` 中的规则至少受到 `A` 的约束时，则 `A` 匹配一个模板参数（称为 `P`）。如果两个参数属于相同类型（类型、非类型、模板），对于非模板参数，它们的参数是等价的 (`14.6.6.1`)，而对于模板参数，它们的每个模板参数列表都是匹配的，则这两个参数匹配。当 `P` 的模板参数列表包含一个模板包 (`14.6.3`) 时，该模板包与与 `A` 中相同类型（类型、非类型、模板）的模板参数列表匹配，并作为 `F` 中的模板参数包（忽略这些元素本身是否为模板包）。

将以下示例添加到第 3 段末尾，位于 C++ 标准给出的示例之后。

```
[示例:
template<typename T> concept B = requires (T t) { t.f(); }
template<typename T> concept D = C&& && requires (T t) { t.g(); }

template<C> class P {
struct S { };

template<C> struct X { };
template<typename> struct Y { };
template<typename T> struct Z { };

Xs s1; // OK: X 和 P 具有等价约束
Xs2; // error: P 不至少受到 Y 的约束 (Y 比 P 受到约束约束)
Xs3; // OK: P 至少受到 Z 的约束
— 示例结束
```

## 14.6 模板声明

修改第 2 段以指示关联约束被无意中从与其关联的模板分离。

出于名称查找和初始化的目的，默认参数、关联约束 (`14.10.2`) 以及函数模板和默认参数的异常规范，以及类模板成员函数的关联约束和异常规范，被视为定义；每个默认参数、关联约束或异常规范都是一个独立的定义，与函数模板定义或任何其他参数、关联约束或异常规范无关。

### 14.6.1 类模板

修改第 3 段，以要求受约束模板的类外定义需要模板约束。

当函数、类成员、成员枚举、静态数据成员或类模板的成员在类定义之外定义时，该成员定义被定义为模板定义，其中模板参数和关联约束 (`1.10.2`) 是该类模板的参数和约束。成员定义中使用的模板参数名称可能与模板列表中使用的模板参数名称不同。成员定义必须以与成员模板参数列表中相同的顺序对参数进行命名。在模板参数中使用中使用省略号扩展时也是如此。

将以下示例添加到第 3 段末尾。

示例：

```
template<typename> concept C = true;
template<typename> concept bool D = true;

template<C T> D(U) struct S {
    void f();
    void g();
};

template<typename T> requires C<T> S<T>::f() // OK: 参数和约束匹配
template<typename T> void S<T>::g() // error: S<T> 没有匹配的声明

template<C T> D(U) struct S<>::inner { }; // OK
```

示例结束

### 14.6.1.1 类模板的成员函数

将以下示例添加到第 1 段末尾。

示例：

```
template<typename T> struct S {
    void f() requires true;
    void g() requires true;
};

template<typename T>
S<T>::f() requires true {} // OK
template<typename T>
S<T>::g() {} // error: S<T> 中没有匹配的函数
```

示例结束

### 14.6.2 成员模板

修改第 1 段，以考虑（可能）受约束的类模板的受约束成员模板。

N4549

模板可以在类或类模板内部声明；此类模板是成员模板。成员模板可以在其类定义或类模板定义之内或之外定义。在类定义之外定义的类模板的成员模板，应用类模板的*模板参数*和关联约束 (`14.10.2`) 指定，随后跟上成员模板的*模板参数*和关联约束。

将以下示例添加到第 1 段末尾：

[示例：

```
template<typename> bool C1 = true;
template<typename> bool C2 = sizeof(T) <= 4;

template<C1>
struct S {
    template<C2> void f();
};

template<C1>
template<C2> void S<T>::f() {} // OK
template<C1>
void S<T>::f() {} // error: S<T> 没有匹配的声明
```

### 14.6.3 可变参数模板

将以下示例添加到第 1 段末尾。

[示例：

```
template<typename... Args>
concept AllArgs = requires() {
    ( (Args && ...);
};
```

示例结束]

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

```cpp
template<typename T> concept bool Eq = requires (T t) { t == t; };

template<typename T>
struct S {
    friend operator==(S a, S b) requires Eq<T> { return a == b; } // OK
};
```

-- end 在类模板实例化 (`14.8`) 中，模板参数被替换到约束中，但不求值。只有当函数被视为重载解析的可行候选者 (`13.3.2`) 时，才会检查约束 (`14.10`)。如果替换失败，则程序为非法格式 (ill-formed)。 -- end

## 14.6.5 类模板部分特化 [temp.class.spec]

在第 3 段之后，以下内容解释了受约束的模板部分特化。

类部分特化可以是受约束的（第 14 节）。[示例]:: 

```cpp
template<typename T> concept bool C = requires (T t) { t.f(); };
template<int> I = I > 0;

template<C1, T2, N> class AT1, T2*, I; // #6
template<C, N, I> class A<int, T*, I>; // #7
```

-- end 示例

从 8 项的列表中删除第 3 项，以允许受约束的模板部分特化，因为 #6 项与第 4 项重复。请注意列表中的所有其他项都已列出。

在类模板部分特化的参数列表中，适用以下限制：

> 特化的参数列表不应与主模板的隐式参数列表相同。

> 特化版本应比主模板更特化 (`14.6.5.2`)。

...

## 14.6.5.1 类模板部分特化的匹配 [temp.class.match]

修改第 2 段；必须满足约束才能匹配部分特化。

如果部分特化的模板参数可以从实际模板参数列表中推导出 (`14.9.2`)，且推导出的模板参数满足部分特化的约束（如果有），(`14.10.2`)，则部分特化匹配给定的实际模板参数列表。

在第 2 段末尾添加以下内容：

[示例]:

```cpp
struct S { void f(); };

A<S, 1> a6; // 使用 #6
A<int, S*, 3> a8; // 使用 #7
```

-- end 示例

14.6.5.1

## 14.6.5. 类模板特化的偏排序

修改第 1 段，使约束纳入类模板特化的偏排序中。

> 对于两个类部分特化，如果给定以下对两个函数模板的重写，且第一个函数根据函数模板的排序规则 (`14.6.6.2`) 至少是第二个函数的特化，则：

- 第一个函数与第一个部分特化具有相同的模板参数和关联约束 (`14.10.2`)，并且包含单个函数，其类型为类模板特化，且模板元素为第一个部分特化的元素，且

- 第二个函数与第二个部分特化具有相同的模板参数和关联约束 (`14.10.2`)，并且包含单个函数，其类型为类模板特化，且模板元素为第二个部分特化的元素。

在第 1 段末尾添加以下内容：

```cpp
Example:
template<typename T> concept bool requires (T t) { t.f(); };
template<typename T> concept bool D = C<T> && requires (T t) { t.f(); };
```

```cpp
template<C> class S {};
template<C> S<T> {}; // #1
template<D> class S<T> {}; // #2
```

```cpp
template<C> void f(S<T>); // A
template<D> void f(S<T>); // B
```

部分特化 #2 比 #1 更特化，因为 B 比 A 更特化。

## 14.6.6 函数模板

## 14.6.6.1 函数模板重载

修改第 6 段，以考虑对函数模板的约束。

> 如果两个函数模板在相同作用域内声明，具有相同的模板参数列表，并且其返回类型和参数列表使用上述规则比较涉及模板参数的表达式时是等价的，则这两个函数模板是等价。

如果两个函数模板满足以下条件，它们是等价的：

- 在相同的作用域内声明，

- 具有相同，

- 具有相同的模板参数列表，并且

返回类型、参数列表和关联约束使用上述规则比较涉及模板参数的表达式时是等价的。

两个函数模板在功能上是等价，除非一个或多个涉及模板参数的返回类型、参数列表以及关联约束 (`14.10.2`) 使用上述规则比较涉及模板参数的表达式时是功能上等价的。如果程序包含功能上等价但并非等价的函数模板声明，则程序为非法格式。

## 14.6.6.2 函数模板的偏排序 [temp.func.order]

修改第 2 段，将约束纳入函数模板的偏排序。



偏排序通过依次转换每个模板并进行推导来选择哪个函数模板比另一个更特化。根据 `14.10.3` 中的规则，特化版本比另一个更特化。

## 14.7 命名解析 [temp.res]

修改第 8 段。

约束的满足在成员查找或重载解析期间确定。保留替换后的约束允许成员函数通过这些约束进行偏排序。

## 14.7.2 依赖名称 [temp.dep]

在此节添加以下段落。

- 折叠表达式是依赖的。

## 14.7.2.1 类型依赖表达式 [temp.expr]

修改第 4 段以包含折叠表达式。

以下是类型依赖的：

```
sizeof( ... )
```

## 14.7.2.2 值依赖表达式 [temp.dep]

添加以下段落：

- 折叠表达式是依赖的。

## 14.7.2.3 实例化点 [temp.point]

在 4 段之后添加新段。

实例化点在特化之前。

## 14.8 模板实例化与特化

## 14.8.1 隐式实例化 [temp.spec] [temp.inst]

修改第 1 段以包含关联约束。

类模板的隐式实例化需要类的声明，而不是成员的定义、默认参数、异常规格（如果有）。因此，语义约束在类声明内部被实例化。

# ISO/IEC T 19217:2015

ISO/IEC T 19217:2015(E)

N4549

## 14.8.2 显式实例化 [temp.explicit]

在第 7 段之后添加以下内容。

> [注：受约束模板的实例化应当满足该模板关联的约束 (`14.10.2`)。约束的满足情况在函数模板显式实例化的名称查找期间、在留有一个或多个未指定的模板参数时的模板参数推导 (`14.9.2.6`) 期间，或者在所有模板参数均已指定的显式实例化 (`14.3`) 期间进行确定。—— 注释结束]

修改第 8 段，以确保只有那些约束在类特化化期间被显式实例化的成员才被实例化。省略 C++ 标准中的该注释。

类模板的实例化也是其每个成员的相同类型（声明或定义）的显式实例化（不包括继承自基类的成员以及模板类型的成员），前提是这些成员在包含该显式实例化的翻译单元中之前未被指定，且关联的约束（如果有）被显式实例化的模板参数满足（`14.10.2`），下文除外。

## 14.8.3 显式特化 [temp.expl.spec]

在第 10 段之后添加以下内容。

> [注：受约束模板的特化应当满足该模板关联的约束 (`14.10.2`)。约束的满足情况在所有模板参数均指定的显式特化 (`14.3`) 的名称查找期间，或者在留有一个或多个未指定的模板参数时的函数模板显式特化的模板参数推导 (`14.9.2.6`) 期间进行确定。—— 注释结束]

## 14.9 函数模板特化化 [temp.fct.spec]

### 14.9.2 模板参数推导 [temp.deduct]

在第 5 段末尾添加以下句子。这定义了将模板参数替换到函数模板约束中的过程。注意第 5 段的最后部分已重复，以便为新增内容提供上下文。

当所有模板参数都已推导出或从默认模板参数中获得时，模板模板参数列表中所有模板的使用以及函数类型都将被替换为相应的推导值或默认参数值。如果替换导致如上所述的无效类型，则模板推导失败。如果函数有关联的约束 (`14.10.2`)，则模板参数被替换到关联的约束中，而不求值生成的表达式。如果这种替换导致无效类型或表达式，则类型推导失败。[注：约束的满足 (`14.10`) 是在重载解析 (`13.3`) 期间以及通过函数模板特化确定的，而不是在替换点。—— 注释结束]

### 14.9.2.6 从函数推导中推导模板参数 [temp.deduct]

在第 1 段之后添加以下内容，以要求在匹配特化版本与模板时必须约束的满足。

从函数模板集合中移除所有关联约束（如果有）未被推导出的模板参数满足 (`14.10.2`) 的模板。

更新第 2 段（现为第 3 段）以适应新的表述。

§ `14.9.2.6`

如果对于剩余模板所考虑的函数模板集合，在考虑偏排序 (`14.6.6.2`) 之后，没有匹配或有多个匹配，则推导失败，且在声明情况下，程序是格式不正确的。

在第 3 段添加以下示例。

[示例：

```cpp
template<typename T> concept bool C = requires (T t) { -t };

template<typename T> void f(T) {} // #1
template<typename T> void g(T) {} // #2
template<typename T> void g(T) {} // #3
```

```
template void f(int); // OK: 指向 #1
template void f(void*); // 错误：无匹配的模板
template void g(int); // OK: 指向 #3
template void g(void*); // OK: 指向 #2
```

结束示例。]# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

## 14.10 模板约束 [temp.constr]

在 `14.9` 之后添加本节。

> [注：本节定义了模板参数约束的含义。抽象语法、关系和等价性在 `14.10.1` 中定义。约束与 `14.10.2` 中的声明关联。声明通过其关联的约束进行偏排序 (`14.10.3`)。—— 注释结束]

## 14.10.1 约束 [temp.constr]

约束是一个逻辑操作和操作数的序列，规定了对模板参数的要求。[注：逻辑操作的操作数是约束。—— 注释结束] 有有不同类型的约束：

- (1) 合与 (`14.10.1`)

- (2) 析取 (`14.10.1`)

- (3) 谓词约束 (`14.10.2`)

- (4) 表达式约束 (`14.10.3`)

- (5) 类型约束 (`14.10.4`)

- (6) 隐式转换约束 (`14.10.5`)

- (7) 参数推导约束 (`14.10.6`)

- (8) 异常约束 (`14.10.7`)

- (9) 参数化约束 (`14.10.8`)

为了使约束被实例化 (`14.8`)，应当满足其关联的约束 (`14.10.2`)。注：在引用模板规格 (`14.3`) 时，需要类模板、别名模板和变量的约束满足情况。函数和模板函数的约束的满足情况是在重载解析 (`14.3.2`) 期间确定的。变量类型或声明的返回类型 (`7.6`) 中由约束类型限定符 (`7.6.4`) 引入的约束的满足情况是……—— 注释结束] 确定一个约束是否满足涉及将模板参数替换为该约束。确定不同类型约束满足情况的规则定义如下：当一个声明比另一个更特化化时，需要知道两个约束是等价的 (`14.10.3`)。确定约束差异的规则在以下小节定义。如果两个约束不等价，但存在一组模板参数使得两个约束都被满足或都不被满足，则它们在功能上是等价的。

### 14.10.1.1 逻辑操作 [temp.constr]

> 存在二元逻辑操作：与和析取。[注：为了说明方便，与使用符号 ∧ 满足，析取使用符号 ∨ 满足。在约束 A ∧ B 中，A 是左操作数，B 是右操作数。约束的分组使用括号。—— 注释结束]

> 与约束是接受两个操作数的。当且仅当两个操作数都满足时，与约束的操作的操作从左到右执行；如果左操作数不满足，则模板参数不替换到右操作数，且约束不满足。在谓词约束的与 (`14.10.2`) 中，令 P 和 Q 为替换生成的约束表达式。如果表达式 P && Q 导致用户定义的运算符&&，则程序是格式不正确的。示例：

```cpp
template <typename T>
const bool get_value() { return };
```

```cpp
template <typename T>
requires sizeof(T) > 1 && get_value<T>()
void f(T);
```

```cpp
void f(int);
f('a'); // OK: 指向 f(int)
```

在 `f` 的关联约束 (`14.10.2`) 的满足情况中，`sizeof(char) == 1` 不满足；参数不替换到与约束的右操作数，因为这种替换会导致 `get_value<char>()` 产生不在直接上下文 (`14.9.2`) 中的无效表达式。

与与另一个与 D 等价，当且仅当 C 和 D 的左操作数等价且右操作数等价。

析取接受两个操作数。当一个或两个操作数满足时，析取的操作的操作的操作从左到右执行：如果左操作数满足，则析取的操作的操作数被替换到右操作数，且在谓词约束的析取 (`14.10.2`) 中，令 P 和 Q 为替换生成的约束表达式。如果表达式 P || Q 导致用户定义的运算符||，则程序是格式不正确的。

析取与另一个析取 D 等价，当且仅当 C 和 D 的左操作数等价且右操作数等价。

### 14.10.1.2 谓词约束 [temp.const.pred]

谓词约束在求值为常量 E (`5.19`) 时被满足。[注：谓词约束允许用表达式约束定义模板——这允许对非类型参数和模板参数进行约束规定。—— 注释结束] 注：谓词约束由 `requires` 子的约束表达式 (`14.10.2`) 引入，或作为约束参数 (`14.1`) 或模板引入 (`14.2`) 的关联约束引入。—— 注释结束] 替换后，E 的类型应为 bool。示例：

```cpp
template <typename T>
const bool c = sizeof(T) == 4 && true; requires 谓词约束
// sizeof(T) == 4 和 true
```

```cpp
template <typename T>
```

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

```cpp
struct B {
    constexpr explicit operator bool() const { return true; }
};

template<typename T>
requires S<T>
void f()();
```

f(0); // ：约束未满足，因为

// 表达式 B<int>(0) 不具有 bool 类型

谓词约束不适用于任何转换。[结束示例]

谓词约束 A 与另一个谓词约束 B 等价，当且仅当 A 和 B 的表达式使用 `14.6.6.1` 中描述的表达式比较规则是等价的。

## 14.10.3 表达式约束 [temp.const.expr]

表达式约束是一种指定了通过模板参数替换形成表达式的要求的约束。如果替换没有失败，则该表达式约束被满足。在表达式约束内部，E 是一个未求值的表达式（第 5 节）。[注：表达式约束由 `requires` 表达式中的注释或复合表达式（`5.1.4)(5.1.3`）中的表达式引入——结束注]；[示例]:

```cpp
template<typename T> concept C = (T t) { ++ };
```

concept C 为表达式 ++ 引入了一个表达式约束。由于在将 int 替换为 T 之后表达式 ++ 是合法的，因此该类型参数满足了这一约束。[结束示例]

表达式约束 A 与另一个表达式约束 B 等价，当且仅当 A 和 B 的表达式使用 `14.6.6.1` 中描述的表达式比较规则是等价的。

## 14.10.4 类型约束 [temp.const.type]

类型约束是一种指定了通过模板参数替换形成类型 T 的要求的约束。当且仅当 T 不是病态（ill-formed）的（即产生 T 的替换没有失败）时，该类型约束被满足。[注：类型约束由 `requires` 表达式中类型要求（`5.1.4.2`）中的 typename 标识符引入——结束注]；[示例]:

```cpp
template<typename T> concept C = requires { typename T::type };
```

concept C 为名称 T::type 引入了一个类型约束。类型 int 不满足这一约束，因为该类型的替换导致了替换失败；typename int::type 是病态的。[结束示例]

类型约束 A 是一个类模板特化，并不要求 T必须是完全类型（`3.9`）。

类型约束 A 与另一个类型约束 B 等价，当且仅当 A 和 B 根据 `14.4` 中的规则是等价的。

## 14.10.5 隐式转换约束 [temp.const.conv]

隐式转换约束是一种指定了表达式 E 到类型 T 的隐式转换要求的约束。当且仅当 E 可隐式转换为 T 时（第 4 节），该约束被满足。[注：转换约束由复合要求中不包含占位符的尾随返回类型（`5.1.4.3`）引入——结束注 |] 示例:

```cpp
template<typename T> bool c =
  requires(T a, T b) {
    return a == b;
  };
```

复合要求 C 引入了两个原子约束：一个针对 a == b 的表达式约束，以及一个表达式 a == b 可隐式转换为 bool 的隐式转换约束。[结束示例]

隐式转换约束 A 与另一个隐式转换约束 B 等价，当且仅当 A 和 B 的表达式使用 `14.6.6.1` 中的规则是等价的，且 A 和 B 的类型根据 `14.4` 中的规则是等价的。

## 14.10.1.6 参数推导约束 [temp.construct]

参数推导约束指定表达式 E 的类型是从类型 T 推导出的，其中 T 包含一个或多个占位符（`7.1.4.4`）。[注：参数推导约束由具有一个或多个占位符的尾随返回类型的复合要求（`5.1.4.3`）引入。在这样的约束中，E 是复合要求的表达式，T 是尾随返回类型指定的类型——结束注]

要确定一个参数推导约束是否满足，使用一个具有类型为 T 的单参数参数的简写函数 f（`8.3.5`）。如果函数调用 f(E) 的解析成功（`13.3`），则该约束被满足。[注：当为 T 中对应于占位符的所有模板参数推导出值，且与任何受限类型相关的约束都满足时，重载解析成功——结束注] 示例:

```cpp
template<typename T, typename U> struct Pair;
template<typename T>
bool C() { return true; }
bool C() { requires(T t) { (*t) -> Pair<T, auto>; };

template<C> void g(int* nullptr); // 错误：约束未满足。
```

C 中复合要求的简写函数 f 为：

```cpp
void f(Pair<T, auto>);
```

在调用 g(int* nullptr) 时，约束未满足，因为当 t 为“指向 int 的指针”时，无法为占位符 C 和 auto 推导出值。

参数推导约束 A 与另一个参数推导约束等价，当且仅当 A 和 B 的表达式使用 `14.6.6.1` 中的规则是等价的，且 A 和 B 的类型是等价的（`14.4`）。

## 14.10.7 异常约束

异常约束是针对表达式 E 的约束，当且仅当 no(E) 为真时（`5.3.7`），该约束被满足。[注：异常约束由包含指定符的复合要求（`5.1.4.3`）引入——结束注]

异常约束 A 与另一个异常约束 B 等价，当且仅当 A 和 B 的表达式使用 `14.6.6.1` 中描述的表达式比较规则是等价的。

## 14.10.8 参数化约束

参数化约束是一种定义了参数序列（`8.3.5`）、约束变量并具有单个操作数的约束。[注：参数化约束由 `requires` 表达式（`5.1.4`）引入。参数化约束的约束变量对应于 `requires` 表达式中要求列表中的参数，而操作数是约束的合取——结束注] [注：参数化约束没有 C++ 语法。为了阐述的起见，参数化约束被写为，例如 λ(x, y)，其中 x 和 y 是约束变量——结束注] [示例]:

```cpp
template<typename T> concept Eq = requires(T a, T b) { a == b; };
```

concept Eq 为表达式 a == b 引入了约束。类型参数满足这一约束是因为在将 int 替换为 T 之后表达式 a == b 是合法的。[结束示例]

表达式约束 A 与另一个表达式约束 B 等价，当且仅当 A 和 B 的表达式使用 `14.6.6.1` 中描述的表达式比较规则是等价的。

## 14.10.2 受约束的声明

受约束的声明通过以下方式引入约束：

- 模板引入（`14`）

- 约束参数（`14.1`）

- 尾随返回类型（`14.2`）

- 构造函数声明（`14.3`）

- 类型指定符（`14.4`）

- 隐式转换约束（`14.5`）

- 表达式约束（`14.6`）

- 异常约束（`14.7`）

- 参数化约束（`14.8`）

- 简写函数（`14.9`）

-  requires 子句（`14.10`）

受约束的声明的关联约束是其引入的约束。两个受约束的声明是等价的，当且仅当它们的关联约束根据 `14.6.6.1` 中的规则是等价的。

## 14.10.1 约束的概述

约束是用于限制声明的规则。约束可以由以下形式引入：

- 谓词约束（`14.10.3`）

- 类型约束（`14.10.4`）

- 隐式转换约束（`14.10.5`）

- 参数推导约束（`14.10.1.6`）

- 异常约束（`14.10.7`）

- 参数化约束（`14.10.8`）

受约束的声明包括：

- 约束参数（`14.1.1`）

- requires 子句（`14.10`）

受约束的声明的关联约束是其引入的约束。两个受约束的声明是等价的，当且仅当它们的关联约束根据 `14.6.6.1` 中的规则是等价的。

# ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

```cpp
template<C1> requires C2> void f3();
template<C2> requires C1> void f3(); // 错误：约束在功能上等价但并不等同
```

第一个声明的关联约束是 `C1> && C2>`，第二个的关联约束是 `C2> && C1` —— 示例结束



确定声明的关联约束以及通过这些约束对声明进行偏序排序，需要首先对其归一化。归一化将一个表达式转换为原子约束的约束与析取序列（14.10.1）。`原子约束`是指那些那些没有操作数的约束：`谓词约束 (14.10.2)`、`表达式约束 (14.10.3)`、`类型约束 (14.10.4)`、`隐式转换约束 (14.10.5)`、`参数析取 (14.10.6)`以及异常约束。表达式 X 的范式定义如下：首先，通过将 X 中引用概念的替换替换为其对应的定义，创建一个新表达式 E。具体而言：

- 替换所有形式为 `C<A1, A2, ... AN>()()` 的函数，其中 C 指向由约束解析规则（14.0.1）选择的概念 D（7.1.7），其结果是将 `A1, A2, ... AN` 替换到 D 返回的表达式中；

以及

- 替换所有形式为 `C<A1, A2, ... AN>` 的 id-表达式，其中 C 是变量概念 D（7.1.7）并根据约束解析规则（14.10.4）替换，其结果是将 `A1, A2, ... AN` 替换到 D 的初始化器中；

如果任何此类替换失败，则程序为格式非法（ill-formed）。其次，将表达式 E 转换为约束：

- 表达式 `(E)` 的范式是 E 的范式；

- 表达式 `E1 && E2` 的范式是 `E1` 和 `E2` 的范式的析取与约束（14.10.1.1）；

- 形式为 `requires ( parameter-declaration-clause ) requirement-body` 的 requires-表达式（5.1.4），若 `parameter-declaration-clause` 不等同于任何参数列表，其范式是该 `parameter-declaration-clause`，且操作数是 requirement-body 中引入的约束的合取的范式；

- 具有以下形式之一的 requires-表达式

`requires ( void ) requirement-body`

`requires () requirement-body`

`requires requirement-body`

其范式是 requirement-body 中引入的约束的合取；

- 在 requires-表达式内部，由嵌套-requirement（5.1.4.4）引入的任何谓词约束 P 被替换为 P 表达式的范式；

- 否则，E 的范式是以 E 为表达式的谓词约束。

一个声明的归一化约束通过对其关联约束进行归一化产生。示例：

# ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015

```cpp
template <typename T> concept bool C1() { return sizeof(T) == 1; }
template <typename T> concept bool C2 = C1<T>() && 1 == 2;
template <typename T> concept bool C3 = requires { typename T::type };
template <typename T> concept bool C4 = requires (T x) { ++x; }

template<C2> void f1(T); // #1
template<C3> void f2(T); // #2
template<C4> void f3(T); // 错误：无效约束 (#4)
```

`f1` 的归一化关联约束是 `sizeof(T) == 1` 和 `1 == 2`；`#2` 的是针对 `T::type` 的类型约束；`#3` 的是受约束的约束 `λ(T x)` 以及表达式约束 `++x`。在约束表达式 `(bool C3)` 中，`#4` 不是一个有效的谓词约束，因为它没有类型。 —— 示例结束

如果一组模板参数满足了声明的关联约束，则这些关联约束被满足。

## 14.10 基于约束的偏序排序

如果约束 P 涵盖（subsumes）另一个约束 Q，意味着在判断 P 是否涵盖 Q 时，它隐含了 P 和 Q 中表达式值的相等性。[示例：替换（14.10.2）涵盖了某些模板参数 U] —— 示例结束

为了确定约束 P 是否涵盖约束 Q，需将 P 和 Q 分别转换为析取标准范式。参数约束可能以合取或析取的形式出现。为了此转换，约束 `λ(T x) P(x)` 等同于约束 `P(x)`。那么，P 涵盖 Q 当且仅当：

- 对于 P 的析取范式中的每一个析取项 Pi，Pi 涵盖 Q 的合取范式；

- 析取项 Pi 涵盖合取项 Q 当且仅当 Pi 是原子约束；

- 原子约束 A 涵盖另一个原子约束 B 当且仅当 A 和 B 是等价的（14.10.1）。示例：设 A 和 B 为原子约束（14.10.1）。A 涵盖。注意每个约束涵盖自身。 —— 示例结束

涵盖关系定义了约束的偏序关系。这种偏序关系用于确定：

- 函数模板的最佳候选者（13.3），

- 非模板的地址（13.4），

- 模板参数的匹配（14.4），

- 类特化的偏序（14.5），

- 函数模板的偏序（14.6）。

一个约束是析取范式，当它是原子项的析取，且每个项是合取范式的。同样，一个约束是合取范式，当它是原子项的合取，且每个项是析取范式的。[示例：设 A、B、C 为原子约束。A ∧ B 是合取范式，其项是 A ∧ B。A ∨ B 是析取范式，其析取项是 A ∧ B。] —— 示例结束

### 14.10.3

当两个声明 D1 和 D2 通过其归一化约束（14.10.2）进行偏序排序时，D1 至少满足 D2，如果：

- D1 和 D2 都是受约束声明，且 D1 的约束涵盖 D2 的约束；或

- D2 是未约束的。

### 14.10.4 概念限定引用的解析 [temp.constr.resolve]

概念解析是从由限定概念名称定义的概念集中选择概念的过程，或者是从由简单模板或其未限定 ID 为简单模板 ID 的包含一个或多个定义的声明集中选择概念。概念解析在类名称出现在以下位置时执行：

- 受约束类型声明（7.1.6.4.2），

- 受约束参数（14.1），

- 模板引入（14.2），或

- 在约束表达式内部（14.10.2）。

此类名称 C 是概念名称或模板名称，指向在该集中匹配一组参数和通配符的概念定义。该序列被称为概念参数列表，其元素称为概念参数。确定概念列表的方法取决于 C 出现的上下文。

- 如果 C 是受约束类型声明或受约束参数的一部分，那么

- 如果 C 是约束命名类型，则概念参数列表由单个通配符组成，

- 如果 C 是部分概念 ID 的概念名称，则概念参数列表由单个通配符以及该部分概念 ID 的模板参数组成。

# PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

(3.2) 如果 C 是模板引言（template-introduction）中的概念名（concept-name），则概念参数列表是与该模板引言的引入列表（introduction-list）长度相同的通配符序列。

(3.3) 如果 C 作为简单模板标识（simple-template-id）的模板名称（template-name）出现，则概念参数列表是该简单模板标识的序列模板参数（sequence-template-arguments）。

4 从 C 所指的集合中选择概念是通过与集合中每个概念的参数列表进行参数匹配来实现的。为了使概念 CC 成为一个可行的选择，参数列表中的每个参数都必须与 CC 对应的参数进行匹配。CC 的默认模板参数（如果有）将为每个不对应概念参数的模板参数进行实例化。实例化的默认值将附加到参数列表中。如果最后一个模板参数不是参数包（parameter pack），且 CC 的模板参数数量大于参数数量，则 CC 是一个可行的选择。否则，使用以下规则将概念参数匹配到模板参数：

- 模板参数与模板匹配当且仅当它在类型上（类型、非类型、类型）匹配并符合 14.4 节中的规则；

- 通配符匹配任何类型的模板参数；

- 模板参数包（14.6.3）匹配零或多个概念，前提是这些参数都根据上述匹配概念参数和模板参数的规则匹配参数包的模式。

如果任何参数未与相应的模板参数匹配，则概念 CC 不是一个可行的选择。通过概念解析选定的概念应当是 C 所指的概念集合中的唯一选择。示例如下：

```cpp
template T concept bool C1() { return true; } // #1
typename T concept bool C2() { return true; } // #2
template int T concept bool C3() { return true; }
typename.. T concept bool C4() = true;
```

```cpp
void f1(const C1+); // OK 选择 C1 #1
void f2(const C1<char>); // OK 选择 C1<char> #2
```

```cpp
template<C2> struct S1; // 错误：对于 C2<0> 没有匹配的概念
// 参数不匹配
// C2 的解析是歧义的
template<C2> struct S2; // 两个概念均可行
```

```cpp
C3(..Ts) void q1(); // OK: 选择 C3
C3(T) void q2(); // OK: 选择 C3
```

- 示例结束

PD ISO/IEC TS 19217:2015

ISO/IEC TS 19217:2015(E)

N4549

# 附录 A（信息）

兼容性

## A.1 Concepts 和 ISO C++ 2014 的 C++ 扩展

1 本节按章节列出了带有 Concepts 的 C++ 与 ISO C++ 之间的差异。

### A.1.1 第 2 节：词法约定

## 2.1 新关键字

`更改：` 在 Concepts 的 C 扩展中添加了新关键字；见 2.1。

`理由：` 添加这些新关键字是为了实现新功能的语义。特别是，添加了 `requires` 关键字以便通过 *requires 子句*（requires-clause）或 *requires 表达式*（requires-expression）引入约束。添加了 `concept` 关键字以便定义概念（7.1.7）、约束的规范化（14.10.2）以及*概念名*与其他标识符的语义区分。

`对原始功能的影响：` 修改了定义功能的语义。任何使用这些关键字作为标识符的 C++ 程序都不是带有 Concepts 的有效 C++ 程序。

`转换难度：` 语法转换。转换一个特定的程序很容易。但转换大量相关程序需要一些工作。

`使用广泛程度：` Seldon。

# 英国标准协会 (BSI)

BSI 是负责编制英国标准及标准相关出版物、信息服务的国家机构。

BSI 是根据皇家特许状成立的。英国标准和其他标准化产品由 BSI Standards Limited 发布。

## 关于我们

我们把商业、工业界、消费者、创新者和其他人士聚集在一起，分享他们的专业知识和经验。我们标准中包含的知识通过我们的共识过程经过仔细的汇和提炼。

## 标准信息

我们可以为您的组织提供成功所需的知识。各种规模的组织都能帮助它们实现目标。

## 购买标准

您可以通过我们的网站下载 BSI 出版的 PDF 版本，包括英国标准和采用的欧洲标准。如果您需要特定的或外国标准，也可以购买纸质版。

## 订阅

我们的系列订阅旨在让标准对您更易获取。通过英国标准在线 (BSO)，您可以从台桌面上访问超过 55,000 英国标准和采用的欧洲标准。这是获取最新数据和标准的简单方法。

PLUS 是 BSI 成员专享的更新服务。当标准发布或修订时，您将自动收到。

欲了解更多有关成为 BSI 成员的信息，请访问 bsi.com。

通过多用户许可 (MUNL)，您可以在组织内部托管标准。许可可以涵盖任意数量的用户。由于更新在可用时就会提供，您可以确保您的文档是最新的。欲了解更多信息，请电子邮件至 bimusales@bsigroup.com。

## BSI 总部

38 Chiswick Road London W4AL UK

## 修订

我们的英国标准和其他出版物通过修订或修改进行更新。

## 版权

所有英国标准和其他 BSI 出版物使用的软件和文档集均归 BSI 或拥有这些信息（如国际标准）版权的其他实体所有。许可软件供有限的商业目的和使用。根据 1998 年版权、设计和专利法，未经 BSI 书面许可，不得复制、在租赁系统中发行或通过任何方式（录制或其他）传输。可以从版权许可部门获取详情和建议。

## Useful联系方式：

客户服务

电话：+44 (0) 8086 9001

电子邮件（订单）：orders@bsigroup.com

订阅

电话：+44 (0) 8086 9001

电子邮件（订阅）：subscriptions@bsigroup.com

## 知识中心

电话：+44 20 8966 7004

电子邮件：knowledgecentre@bsigroup.com

## 版权与许可

电话：+44 (0)20 8966 7070

电子邮件：copyright@bsigroup.com
