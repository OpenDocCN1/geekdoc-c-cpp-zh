
### 7.5.4.2 限定标识符

`qualified-id`:
`class-name-::qualified-id`

- 1 表示类非静态成员的标识表达式在用于该成员的定义 (`11.4`) 中是 prvalue。

> [Note 1] 在可选的成员初始化 (`11.4`) 中，该类不需要完整。

- 2 否则，类型为 `bool`、`char16_t`、`char32_t`、`wchar` 或枚举类型的操作数转换为整数类型。

> [Note 2] 在范围枚举类型中，该操作数的类型是该范围枚举类型。 — 脚注结束

- 3 否则，如果标识是类 `X` 的非静态成员 (`11.4`)，则该表达式是目标类型的 prvalue。

[Example 2:

```cpp
class Outer {

  int a[&this]; // 错误：不是成员函数

  unsigned int sz = size(*this); // OK：在成员初始化

  void f() {

    int b[&this]; // OK

    struct Inner {

      int c[&this]; // 错误：不是 Inner 的成员函数

    }

  }

};
```
— 示例结束

```cpp
int j = sizeof(S::m + 42);   // OK
// end example;
```

3 一个表示立即函数（immediate function）的潜在评估 id-表达式 (`9.2.6`) 仅应出现在
—作为立即调用（immediate invocation）的子表达式，或
—在立即函数上下文中 (`7.7`)。

4 对于表示重载集合的 id-表达式，允许通过重载解析选择一个唯一的函数 (`12.4`, `12.5`)，

> [Note 2: 程序不能引用一个带有 `requires-clause` 且其约束表达式未满足的函数，因为此类函数永远不会被重载解析所选择。

> [Example 2:

```cpp
template<typename T> struct A {

    static void f(int) requires false;

}

void g() {

    A<int> f(0); // error: cannot call f

    void (*p)(int) = A<int>::f; // error: cannot take the address of f

    decltype(A<int>::f) = nullptr; // error: the decltype(A<int>*) is invalid
```
在每种情况下，`f` 的约束均未满足。在 `p` 的情况下，这些约束要求必须满足，即使 `f` 是一个未计算的操作数（unvaluated operand）（`7.2`）。 — end example

## § 7.5.42 统一名称 (Unified names)

- 无限定标识符 (`unqualified-id`):
    `标识符` (`identifier`)
    `运算符函数标识` (`operator-function-id`)
    `转换函数标识` (`conversion-function-id`)
    `类型标识` (`type-id`)
    `声明说明符` (`declaration-specifier`)
    `模板标识` (`template-id`)

标识符只有在它已经过适当声明（第 9 条）或作为声明符-标识（declarator-id）的一部分出现（`9.3`）时，才是一个 id。一个命名参数名-id 的标识符看到该参数的拷贝 (`9.5.4`)。

> [Note 1: 对于运算符函数标识，请参见 `12.6`；对于转换函数标识，参见 `11.4.8.3`；对于字面量运算符标识，参见 `13.3`。以 — 前缀的类型名或声明说明符表示所命名类型的析构函数；参见 `7.5.4.4`。在非静态成员函数的定义内部，命名非静态成员的标识符在定义该函数的类作用范围内始终是有效的。

2 该实体由标识符表示。如果该实体是局部的，并且在无限定标识符可能出现的区域内，从未计算的操作数的外部对其进行命名，并借用捕获它的 lambda 表达式（`7.6.1.5`）时，则该实体的类型是类访问表达式的类型，即为了在该 lambda 表达式的闭包（closure）中为类捕获而要声明的非静态成员数据。

> [Note 2: 如果 lambda 表达式没有声明为 `mutable`，则此类标识符的类型将是 `const` — end note]

类型表达式是结果的类型。

> [Note 3: 如果该实体是类型 `T` 的模板参数模板对象 (`13.2`)，则表达式的类型为 `const T`。 — end note]

4 如果该类型是 cv 限定或引用类型，将按照 `7.2.2` 的描述进行调整。 — end note

如果实体是函数、结构化绑定 (`9.6`)、数据成员或模板参数对象，则表达式为值；否则为原始值 (`7.2:1`)；如果标识符指定位域，则是位域。

```cpp
Example 1:

void f() {

    float x, &r = x;

    []={

        decltype(x) y1; // y1 类型为 float

        decltype((x)) y2 = y1; // y2 类型为 float const&，因为此 lambda
// 不是 mutable 且 x 是匿名值

        decltype(r) r1 = y1; // r1 类型为 float&

        decltype((r)) r2 = y2; // r2 类型为 float const&

    };

}

// end example
```

### 7.5.4.3 限定名称 (Qualified names)

限定标识 (`qualified-id`):
嵌套名称说明符_模板 (`nested-name-specifier_template_opt`) 无限定标识
嵌套名称说明符 (`nested-name-specifier`):
`::`
类型名 (`type-name`) :
命名空间名 (`namespace-name`) :
`decltype`说明符 (`decltype-specifier`) ::
嵌套名称说明符 (`nested-name-specifier`)
嵌套名称说明符_模板 (`nested-name-specifier_template_opt`) 简单模板标识 (`simple-template-id`) ::

由 `decltype` 说明符表示一个类，可选地后跟成员 (`11.4`) 或其基类之一 (`11.7`)，`6.5.4.2` 描述限定 id 中的类成员名称查找。结果是成员。结果的类型是成员的类型。如果成员是静态成员或数据成员，则是值。

> [Note 1: 类成员可以在其任何点 (`6.4.7`) 使用限定 id 引用。 — end]

使用 `~type` 时，两个名称指向同一个类型（忽略限定）；此符号表示所命名的析构函数 (`7.5.4.4`)。除非另如此，无限定 id 是析构函数的名称。嵌套名称说明符命名命名空间 (`9.8`)，可选后跟关键字 `template` (`13.3`)，然后后跟成员名称（或命名空间名称），是一个枚举的限定。结果是枚举。结果的类型是枚举。如果无限定 id 是转换函数标识，其类型首先在限定 id 的嵌套名称说明符指定的类中查找，如果找到，则在限定 id 发生的环境中查找。在这些情况下，只考虑表示模板或特化的名称。

### 7.5.4.4 析构 (Destruction)

如果 id-表达式是类类型 (`11.4.7`)，它表示类型 `T` 的析构函数；否则 id-表达式命名为伪析构函数。如果 id-表达式是伪析构函数，它是标量并在类访问 (`7.6.1.5`) 的右操作数或函数调用 (`7.6.1.3`) 的后缀表达式。

```cpp
Example 1:

struct C { };

void f() {

  C* pc = new C;

  using C2 = C;

  pc->C2(0); // OK, 析构 *pc // 未定义行为：C 类型被析构两次

  using T = int;

  pc()~T(0); // OK, 无影响

  T 是用户定义的

}
```

### 7.5.5 Lambda 表达式 (Lambda expressions)

### 7.5.5.1 通用 (General)

lambda 表达式:
lambda-引入符 lambda-声明符_可选 复合语句
lambda-引入符 `<` 模板参数列表 `>` 要求 lambda-声明符子句 lambda-声明符_可选 复合语句
lambda-引入符:
{ lambda-声明符_可选 }
lambda-声明符:
{ 参数声明符子句 声明说明符序列_可选
`noexcept` 子句 属性说明符序列_可选 尾随类型_可选 要求约束子句

- 1 lambda 表达式提供了一种创建函数作用域的方法。
```cpp
Example 1:

#include <algorithm>

#include <cmath>

void absort(float* x, int N, [float a, float b]) { return std::abs(a) < std::abs(b); }
```

2 lambda 表达式是一个值，其结果被称为闭包对象。
[Note 1] 闭包对象类似于函数对象 (`20.14`)。 — end

3 在 lambda-声明符的声明说明符序列中，每个说明符必须是 `const`、`constexpr` 或 `constval` 之一。
[Note 2] `9.3` 中要求尾随子句。 — end

4 如果 lambda 表达式不包含 lambda-声明符，则就像 lambda-声明符为 `()` 一样。lambda 返回类型是 `auto`，它会被由尾随返回类型指定的类型替换，或者从 `9.2.9.6` 中的 `return` 语句中推导。
```cpp
Example 2:

auto x1 = [](int i) { return i; }; // OK: 返回类型为 int

auto x2 = []() { return {1, 2}; }; // error: 从初始化列表推导返回类型

int j = [](auto&& j) { return j; }; // OK: 返回类型为 int
```

5 如果 lambda 表达式具有任何泛型类型占位符 (`9.2.9.6`)，或者 lambda 模板参数，则 lambda 是泛型 lambda。
```cpp
Example 3:

int i = [](int i, auto a) { return i; }; (3, 4); // OK: 一个泛型 lambda

int j = []<class T>(T t, int i) { return i; }; (3, 4); // OK: 一个泛型 lambda
```

### 7.5.2 闭包类型 (Closure types)

- 1 lambda 表达式的类型（也是闭包对象的类型）是一个唯一的、无命名的非联合类类型，称为闭包类型，其属性下文所述。

闭包类型声明在包含相应 lambda 表达式的最小块作用域、类作用域或命名空间作用域中。

> [注意1: 这决定了与闭包类型相关的命名空间和类的集合 (`6.5.3`)。lambda 装饰器的参数不会影响这些命名空间和类。结束注意]

闭包类型不是一个聚合类型 (`9.4.2`)。实现中定义的闭包类型可能与下面描述的不同；这不会通过更改以下内容改变程序的可观测行为：

- 闭包类型的大小和/或对齐方式 (`11.2`)，或
- 闭包类型是否为平凡可拷贝的 (`trivially copyable`)，
- 闭包是否为标准布局拷贝 (`11.2`)。

实现中不允许向闭包类型添加值引用类型的成员。

lambda 表达式的闭包具有一个公有的函数调用运算符（针对非泛型 lambda）或函数运算符模板（针对泛型 lambda），其参数和返回类型分别由 lambda 表达式的参数声明闭包（parameter-declaration-closure）和尾随返回类型（trailing-return-type）描述，其模板参数列表（template-parameter-list）由指定的模板参数列表组成（如果有）。函数调用运算符的 `requires-of` 是紧随于 `<template-operator-list>` 之后的 `requires`（如果有）。函数调用运算符或运算符模板的尾随 `requires-of` 是 lambda 装饰器的 `requires-of`（如果有）。

> [注意2: 泛型 lambda 的函数运算符模板可以简写为 `requires-template` (`9.3.4.6`)。结束注意]

示例 1:
```cpp
auto lambda = [](auto a, auto&& b) { return a < b };

bool b = lambda(3, 14); // OK
```
```cpp
auto vlambda = [](auto printer) {

  return [auto&& ts](...) {

    print(std::decay<decltype(ts)>(ts)...);

  }}; // OK: ts 是一个函数参数
```
```cpp
return []() {

  print(ts ...);

};
```
```cpp
auto p = vlambda(auto v1, auto v2, auto v3) {

  std::cout << v1 << v2 << v3;

}; // OK: 输出 13.14
auto q = p('1', 'a', 34); // OK: 输出 1a3.14
```

只有当 lambda 表达式的参数声明句不是 `mutable` 时，函数调用运算符才被声明为 `const` (`11.4.3`)。它既不是 `virtual` 的，也没有声明为 `volatile`。lambda 表达式中指定的 `noexcept` 不适用于相应的函数调用运算符或运算符模板。lambda 符（lambda-declarator）中的属性规范序列（attribute-specification-seq）属于相应函数调用运算符或运算符模板的类型。如果相应 lambda 表达式的参数声明句后面跟着 `constexpr` 或 `conststeval`，或者它满足 `constexpr` 函数的属性 (`9.2.6`)，则函数调用运算符或任何运算符模板特化为 `const` 函数。它是一个 `inline` 函数。

示例 2:
```cpp
auto ID = [](auto a) { return a; };

static_assert(ID(3) == 3); // OK
```
```cpp
struct NonLiteral {

  NonLiteral(int n) : n(n) {}

  int n;

};

static_assert(ID(NonLiteral(3)).n == 3); // OK
// 结束示例
```

示例 3:
```cpp
auto mono = [](auto v) { return v; };

auto add = [](auto m1) constexpr {

    auto ret = m1();

    return [ret](auto m2) mutable {

        auto mval = m1();

        auto plus = [auto m2] mutable constexpr {

            return plus(m2);

        };

        return mono(ret);

    };

};

constexpr auto zero = monoid();

constexpr auto one = monoid(1);

static_assert(add(one)(zero()) == one); // OK
// 由于 two 下方不是 constexpr，其 constexpr 成员函数调用的评估无法对其主体之一执行左值引用转换
// 在常量表达式中

auto two = monoid(2); // OK, 不是常量表达式

static_assert(add(one)(one) == two()); // 错误: two 不是常量表达式

static_assert(add(one)(one) == monoid(2)); // OK
// 结束示例
```

> [注意4: 函数调用或运算符可以通过类型约束 (`13.2`)、`requires` (`13.1`) 或尾随捕获 (`9.3`) 进行约束 (`13.5.3`)。]

示例 4:
```cpp
template <typename T> class C1 = /* ... */;
template <size_t B, typename C> concept C2 = /* ... */;
template <typename A, typename B> concept C3 = /* ... */;
```
```cpp
auto f = [](auto T1, auto T2) requires C2(sizeof(T1) <= sizeof(T2)) {

    // T1, a1, T2, a2, a3, a4 requires C2(decltype(a4), T2)
    // T2 被类型约束约束。
    // T1 和 T2 被 requires 子句约束。
    // a4 的类型被尾随的 requires 子句约束。

};
// 结束示例
```
