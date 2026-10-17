
```cpp
struct X {
    mutable int i;
    int j;
}
struct Y {
    X x;
    Y();
}
```

> 92 对于具有类型限定符或仅指定 cv 限定符类型限定符的声明限定符序列（`decl-specifier-seq`），没有特殊规定。C 的“隐含”规则不再被支持。

```cpp
const Y y;
// 格式良好：mutable 成员可以被修改
y.x.j++;      // 错误：修改了 const 限定的成员
Y* p = const_cast<Y*>(&y); // 格式良好：去掉 y 的 const 性
px.i = 99;      // 格式良好：mutable x.i 可以被修改
p->x.j = 99;      // 未定义：修改了 const 成员
// 示例结束
```

6 如果尝试通过非 `volatile` 类型的全局值（`glvalue`）引用一个用 `volatile` 限定类型定义的对象，则程序行为是未定义的。

[注：`volatile` 是对实现的一种提示，以避免激进的优化，因为对象的值可能会通过实现无法检测的方式发生改变。详细语义见 1.9。通常情况下，`volatile` 的语义在 C++ 中与 C 中是相同的。 — 备注结束]

## 7.1.6.2 简单类型限定符 [dcl.type.simple]

+ 1 简单类型限定符

`simple-type:` 

`nested-name-specifier_opt type-name`

`nested-name-specifier simple-template-id`

`char`

`char16_t`

`char32_t`

`char_t`

`bool`

`short`

`int`

`long`

`signed`

`unsigned`

`float`

`double`

`void`

`auto`

`dcltype-specifier`

`type-name:` 

`class-name`

`enum-name`

`typedef-name`

`simple-template-id`

`decl-specifier`

`dcltype ( expression )`

2 `auto` 是一个待推导类型的占位符（7.1.6.4）。其他简单类型限定符要么是之前声明的用户定义类型，要么是基本类型（3.9.1）。表 10 总结了简单类型限定符及其指定的类型的有效组合。

3 当允许使用简单类型限定符时，它们可以任意顺序与其他声明限定符混合。[注：`char` 类型对象和位域（9.6）是有符号还是无符号是由定义的。 — 备注结束]

### 表 10 简单类型限定符及其指定的类型

| 限定符 | 类型 |
| :--- | :--- |
| `type-name` | 命类型 |
| `simple-template-id` | 14.2 中定义的类型 |
| `char` | `char` |
| `unsigned char` | `unsigned char` |
| `signed char` | `signed char` |
| `char16_t` | `char16_t` |
| `char32_t` | `char32_t` |
| `bool` | `bool` |
| `short` | `short` |
| `unsigned short` | `unsigned short` |
| `signed short` | `signed short` |
| `int` | `int` |
| `unsigned int` | `unsigned int` |
| `signed int` | `signed int` |
| `long` | `long` |
| `unsigned long` | `unsigned long` |
| `signed long` | `signed long` |
| `float` | `float` |
| `double` | `double` |
| `void` | `void` |
| `auto` | 待推导类型的占位符 |

由 `decltype(e)` 表示的类型如下：

- 如果 `e` 是不带括号的标识表达式（`id-expression`）或不带括号的类访问（5.2），`decltype(e)` 是 `e` 命名的类型。如果没有这样的实体，或者 `e` 命名了一组函数，则程序格式错误；
- 否则，如果 `e` 是左值（`lvalue`），`decltype(e)` 是 `T&`，其中 `T` 是 `e` 的类型；
- 否则，如果 `e` 是右值（`rvalue`），`decltype(e)` 是 `T&&`，其中 `T` 是 `e` 的类型；
- 否则，`decltype(e)` 是 `e` 的类型。

示例：

```cpp
const int& foo();
int i;
struct A { double x; } a;
decltype(foo()); // 类型为 const int&
decltype(i) x2; // 类型为 int
decltype(a->x) x3; // 类型为 double
decltype(a->x) x4 = x3; // 类型为 const double
```

# ISO/IEC 14882:2011(E)

```
// 返回类型为 A<int>，因此引入了一个临时对象并使用了其
// 析构函数，程序格式错误的。
```

```
}
// 结束示例 -- 结束注释
```

## 7.1.6.3 详细类型限定符 (Elaborated type specifiers)

```
elaborated-type-specifier:
class-key attribute-specifier-seq_opt nested-name-specifier_opt identifier
class-key-nested-name-specifier_opt template_opt simple-template-id
enum nested-name-specifier_opt identifier
```

- 1. 除非该详细类型限定符是声明的唯一组成部分，否则 `attribute-specifier-seq` 不应出现在 `elaborated-type-specifier` 中。如果详细类型限定符是声明的唯一组成部分，则该声明是格式错误的，除非它是显式特化 (14.7.3)、显式实例化 (14.7.2) 或它具有以下形式之一：

   `class-key attribute-specifier-seq_opt identifier;`

   `friend-key :: identifier;`

   `friend-key :: simple-template-id;`

   `friend-key nested-name-specifier_opt identifier;`

   `friend-key nested-name-specifier_opt template_opt simple-template-id;`

- 2. 2.3.4.4 描述了 `elaborated-type-specifier` 中 `identifier` 的名称查找过程。如果 `identifier` 解析为一个类名（`class-name`）或枚举名（`enum-name`），则 `elaborated-type-specifier` 以一种与类型限定符（`type-specifier`）引入其类型名相同的方式将其引入声明中。如果 `identifier` 解析为一个类型定义名（`typedef-name`）或该 `simple-template-id` 解析为一个别名模板特化，则 `elaborated-type-specifier` 是格式错误的。[注：这意味着，如果有的话，它作用于被声明的类；`attribute-specifier-seq` 中的属性无论在何种情况下都被视为该类的属性。

   `friend class T;`

- 3. `elaborated-type-specifiers` 中的 `class-key` 或 `enum` 关键字的类型应与 `elaborated-type-specifiers` 中的名称所引用的声明保持一致。此规则也适用于声明类名或 `friend` 类的 `elaborated-type-specifier` 形式，因为它可以被解释为引用该类的定义。在任何 `elaborated-type-specifier` 中，该关键字应用于引用枚举 (7.2)，联合体 `class-key` 应用于引用联合体（第 9 节），且 `class` 或 `struct class-key` 应用于引用使用 `class` 或 `struct class-key` 声明的联合体（第 9 节）。

   [示例：

   `enum class E { a, b };`

   `enum E = E::a; // OK`

> 是格式错误的。然而，类似的声明 `friend T;` 是允许的 (11.3)。 --

```
-- 结束示例]
```

## 7.1.6.4 auto 限定符 (auto specifier)

- 1. `auto-type-specifier` 表示正在声明的变量的类型应从其初始化器中推导，或者函数声明应包含一个尾随返回类型（`trailing-return-type`）。
- 2. `auto-type-specifier` 可以与带有尾随返回类型的函数限定符 (8.3.5) 一起出现在任何此类声明符有效的上下文中。

§ 7.1.6.4

ISO/IEC 2011 – 版权所有

## ISO/IEC 14882:2011(E)

否则，变量的类型从其初始化器中推导。被声明变量的名称不应出现在初始化器中。在块 (6.3.6) 中声明变量以及在 `for-init-statement` (6.5.3) 中，这种对 `auto` 的使用是允许的，`auto` 应作为声明符（`decl-specifiers`）之一出现。

如果 `enum-key` 后面跟着一个嵌套限定符（`nested-specifier`），则 `enum-specifier` 指之前直接在类或命名空间中声明的枚举（即既不是通过 `using-declaration` 引入），并且 `enum-specifier` 应出现在包含该先前声明的命名空间中。

每个枚举定义了一个与所有其他类型都不同的类型。每个枚举都有一个底层类型。可以使用 `enum-base` 显式指定底层类型；如果未显式指定，则作用域枚举类型的底层类型被认为是固定的（fixed）。在 `enum-specifier` 结束大括号之后，每个枚举成员（enumerator）在结束大括号之前的类型即为底层类型；如果底层类型是固定的，则每个枚举成员的类型以及 `enumerator-specifier` 中的常量表达式应为底层类型的常量表达式 (5.19)；如果枚举的初始化值无法良好构造。如果底层类型不是固定的，则每个枚举成员的类型是其初始化值的类型。

- 如果为枚举成员指定了初始化器，则初始化值具有与表达式相同的类型，且该常量表达式应为整数常量表达式 (5.19)。
- 如果第一个枚举成员没有指定初始化器，则初始化值为一个无符号整数类型。
- 否则，初始化值与前一个枚举成员的初始化值的类型相同，除非增加后的值无法在该类型中表示，在这种情况下，该类型为足以容纳增加后值的无符号整数类型。如果不存在此类类型，则程序为非法构造的（ill-formed）。

对于底层类型固定的枚举，其底层类型可以表示枚举中定义的所有枚举成员值。如果是由实现决定的（即使用哪种整数类型作为底层类型），则底层类型不应大于 `int`，除非枚举成员的值无法放入 `int` 或 `unsigned int`。如果 `enumerator-list` 为空，则底层类型为 `int`，除非该枚举有一个默认值。

对于底层类型固定的枚举，枚举的值就是底层类型的值。否则，其中 $e_{min}$ 是最小枚举成员，$e_{max}$ 是最大枚举成员，其值处于 $e_{min}$ 到 $e_{max}$ 的范围内，定义如下：令 $K$ 对于补码表示为 1，对于反码或符号位表示表示为 0。$b_{min}$ 是大于或等于 $max(e_{min} - K)$ 和 $2^s - 1$ 的最小值，其中 $s$ 是非负整数。如果 $e_{min} - K$ 为负，则 $b_{min}$ 为零。足以容纳该枚举类型所有值的最小位域的大小为 $s$，如果是的话，否则为 $s+1$。可以定义一个具有未由任何枚举成员定义的值的枚举。如果 `enumerator-list` 为空，枚举的值等同于枚举有一个值为 0 的单个枚举成员。

如果两个枚举具有相同的底层类型，则它们是布局兼容的（layout-compatible）。

枚举成员的值或此类枚举对象的值通过整型提升（integral promotion）(4.5) 转换为整数。[示例：

```cpp
enum color { red, yellow, green=20, blue };ncolor col = red;
color* cp = &col;
// ...
```

> 93) 这组值用于定义该枚举类型的提升和转换语义。它并不排除枚举类型的表达式可能具有超出此范围的值。

使得 `color` 成为一个描述各种颜色的类型，并声明 `col` 为该类型的对象，`cp` 为该类型对象的指针。`color` 类型对象的可能值为 `red`、`yellow`、`green`、`blue`；这些值可以转换为整数值 0,1,20 和 21。由于枚举是不同的类型，`color` 类型的对象只能被赋予 `color` 类型的值。

```cpp
color c = 1; // 错误：类型不匹配，
// 无从 int 到 col 的转换
int i = yellow; // OK：yellow 转换为整数值 1
// 整型提升
```

此注释隐含作用域枚举未提供枚举到 int的转换：

```cpp
enum class Col { red, yellow, green };
int x = Col::red; // 错误：没有 Col 到 int 的转换
Col y = Col::red; // 错误：没有 Col 到 bool 的转换
if (y) { // 错误：没有 Col 到 bool
```

每个名称和每个非作用域枚举成员都声明在立即包含 `enum-specifier` 的作用域内。每个作用域枚举成员都声明在枚举的作用域内。这些名称遵循 (3.3) 和 (3.4) 中所有名称的作用域规则。示例：

```cpp
enum direction { left='1', right='r' };
void g() {
    direction d; // OK
    d = left; // OK
    d = direction::right; // OK
}
```

```cpp
enum class altitude { high='h', low='l' };
void h() {
    altitude a; // OK
    a = high; // 错误：high 不在作用域内
    a = altitude::low; // OK
}
```

在类作用域内声明的枚举成员可以使用类访问运算符 (::)、点运算符 (.) 和箭头运算符 (->) 来引用，见 5.2。示例：

```cpp
struct X {
    enum direction { left='1', right='r' };
    int f(int i) { return i=left ? 0 :right ? 1; }
}
void g(X* p) {
    X::direction d; // 错误：direction 不在作用域内
    int i;
    i = p->f(left); // 错误：left 不在作用域内
    i = p->f(X::right); // OK
    i = p->f(p->left); // OK
}
```

## 7.3 命名空间

1 命名空间是一个可选命名的声明式区域。命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

2 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

3 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

4 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

5 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

6 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

7 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

8 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

9 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

1 命名空间是一个可选命名的声明式区域。命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

2 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

3 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

4 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

5 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

6 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。

7 命名空间的名称可用于访问在该命名空间中声明的实体；即命名空间的成员。与其他声明式区域不同，命名空间的定义可以拆分成多个部分。
