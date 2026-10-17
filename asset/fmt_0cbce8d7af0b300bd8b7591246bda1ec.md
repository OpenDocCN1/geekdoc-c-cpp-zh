
```cpp
struct T {
    T(int x) { return T(x); }
    int operator=(int x) { return x; }
    T(int) { };
};
struct T2 { T2() { }; };
int a, (**b)(T2))(int), c, d;

void f() {
    // 消除歧义要求此处是一个声明：
    T1(a) = 3,               // T2 将声明为类型 T1 的变量，但这将
    T2(4);
    (**b)(T2(c)))(int);      // 允许声明的最后部分正确解析，
                             // 因为它取决于 T2 是否为类型名
}; — 示例结束
```

## 声明

### 9.1 前言

声明通常指定如何解释名称。声明具有 `decl-seq`：
`declaration`
`decl-seq-declaration`
`declaration:`
`block-declaration`
`declspec-function-declaration`
`function-definition`
`template-declaration`
`deduction-guide`
`explicit-instantiation`
`explicit-specialization`
`export-declaration`
`linkage-specification`
`namespace-definition`
`empty-declaration`
`attribute-declaration`
`module-import-declaration`
`block-declaration:`
`simple-declaration`
`asm-declaration`
`namespace-alias-declaration`
`using-declaration`
`using-enum-declaration`
`using-directive`
`static_assert-declaration`
`alias-declaration-enum-declaration`
`declspec-function-declaration:`
`attribute-spec-seq_opt declarator ;`
`alias-declaration:`
`using identifier-attribute-spec-seq_opt = defining-type-id;`
`simple-declaration:`
`decl-decl-spec-seq-opt init-declarator-list_opt`
`attribute-spec-seq_opt undecl-spec-seq init-declarator-list;`
`attribute-spec-seq_opt undecl-spec-seq ref-qualifier_opt [ identifier-list ] initializer;`
`static_assert-declaration:`
`static_assert ( constant expression );`
`static_assert ( constant expression, string-literal );`
`empty-declaration:`

注 [1：`as-declarations` 在 9.11 中描述；函数定义在 9.5 中描述，模板声明和推导指引在 13.7.2.3 中描述；命名空间定义在 9.8.2 中描述；使用声明在 9.9 中描述，使用指引在 9.8.4 中描述。 — 结束

形式为 `attribute-spec-seq_opt undecl-decl-seq, init-declarator-list` 的简单声明或 `undecl-spec-function-declaration` 被分为三部分。属性在 9.12 中描述，`undecl-spec-seq` 的主要组件在 9.2 中描述，`init-declarator-list` 的组件在 9.3 中描述。`attribute-spec-seq` 属于 `init-declarator-list` 所声明的实体的每个声明符。

[Note 2：在对实体的声明中，属于该实体的属性可以出现在声明的开头，也可以出现在该声明的声明-id 之后。-- 备注结束]

[Example 1:
`[[noreturn]] void f [[noreturn]] (); // 正确`
-- 示例结束]

除非有说明，否则带属性的声明的含义由实现定义。

声明发生在作用域（6.4）中；作用域规则总结在 6.5 中。定义函数或类、命名空间的声明包含嵌套的作用域。除非另有说明，简单声明中的 `init-declarator-list` 仅在 `decl-spec` 包含类限定符（11）、一个枚举举例（9.7）或枚举限定符时省略。在这些情况下，当 `decl-seq` 中存在类限定符或枚举限定符时，`decl-seq` 将引入一个或名称，或重申之前引入的名称。

[Example 2:
// enum {}; // 错误
-- 示例结束]

在静态声明中，常量表达式必须是有效的类型（7.7）。如果表达式的值为，则声明无效。否则，如果表达式是非形式的，生成的诊断（4.1）应包含字符串字面量（如果提供了）。

[Example 3:
`static_assert(sizeof(int) == sizeof(void),"wrong size");`
-- 示例结束]

空声明无效。

带有声明符列表的简单声明称为结构绑定声明（9.6）。如果 `decl-seq` 包含除 `static`、`thread_local` 或 `cv` 限定符以外的任何 `decl-spec`，则程序是非形式的。初始化器应为“赋值表达式”的形式，或者 `(赋值表达式)`，或者 `(赋值表达式)`，其中赋值表达式为数组或非类类型。

`init-declarator-list` 中的每个声明符恰好包含一个声明符-id，即该声明符-id 声明的名称以及由声明引入的名称。`decl-seq` 中的定义类型限定符（9.2.9）和 `int-declarator` 的递归声明描述了一个类型（9.3.4），该类型与 `in-declarator` 关联。

如果简单声明包含 `typedef` 限定符，则声明称为 `typedef` ，每个 `in-declarator` 的名称被声明为类型名，与之等同（9.2.4）。如果 `decl-spec` 不包含 `typedef`，则当与名称关联的类型是函数（9.3.4）时，称为函数声明，或对象声明。

泛声明形式中的语法组件被添加到函数声明中以构成函数定义。然而，对象声明除非包含 `extern` 限定符且没有初始化器（6.2），否则就是定义。对象定义会预留适当大小和对齐的存储空间并进行相应的（9.4）。

节点特定函数声明应声明构造函数、析构函数或转换函数。

[Note 3：节点特定类型只能用于模板声明（13.1）、显式实例化（13.9.3）或或显式规格化（13.9.4）。-- 备注结束]

# ISO/IEC 14882:2020(E)

## 9.2 限定符 (Specifiers)

### 9.2.1 通用

在声明中使用的限定符为：
```text
decl-specifier:
storage-class-specifier
defining-type-specifier
function-specifier
friend
typedef
constexpr
constval
consinit
inline
decl-specifier-seq:
decl-specifier-attribute-specifier-seq_opt
decl-specifier decl-specifier-seq
```
`decl-specifier-seq` 中可选的 `attribute-specifier` 属于由前面的 `decl-specifiers` 决定的类型 (9.3.4)。`attribute-specifier` 仅影响该声明所处的类型，而不影响涉及该类型的其他声明。

- 每个 `decl-specifier` 在一个完整的 `decl-specifier-seq` 中应只出现一次，但 `long` 可以出现两次。在 `decl-specifier-seq` 中，`constexpr`、`constval` 和 `consinit` 关键字最多出现其中一个。
- 在解析 `decl-specifier-seq` 时如果遇到类型名（type-name），其解释为该 `decl-specifier-seq` 中除 `cv-qualifier` 外不再有其他的 `defining-type-specifier`。此时该序列应按描述的方式进行不一致处理。

示例 1：
```c
tchar Pc;
static Pc;
```
此处，声明 `static` 是格式错误的，因为没有为 `Pc` 的 `static` 变量指定名称。为了获得一个有效的变量 `Pc`，必须存在一个类型指定符（`const` 或 `constval` 除外）来标识该 `typedef-name Pc` 是正在被（重）声明的名称，而不是 `decl-specifier-seq` 的一部分。例如：

```c
void f(const Pc);
void g(char* const char*);
void h(unsigned int);
void k(unsigned int)
```
> [注 1：由于 `signed`、`unsigned`、`long` 和 `short` 默认为 `int`，出现在这些限定符之后的类型名被视为正在被（重）声明的名称。]

示例 2：
```c
void h(unsigned Pc);
void k(unsigned int)
```

### 9.2.2 存储类分类符 (Storage class classifiers)

- 存储类限定符为：
```text
storage-class-specifier:
static
thread_local
extern
mutable
```
在给定的 `decl-specifier-seq` 中，最多出现一个 `storage-class-specifier`，但 `thread_local` 可以与 `static` 一起出现。如果 `thread_local` 出现在变量的任何声明中，它必须在该变量的所有声明中都存在。如果 `decl-specifier-seq` 中出现了 `storage-class-specifier`，则该 `decl-specifier` 中不能有 `typedef`，且声明的 `init-declarator-list` 或 `member-declarator-list` 不为空（在命名空间或全局命名空间中定义的匿名声明除外，应声明为 `static` (11.5.2)）。存储类限定符适用于由限定符声明的每个 `init-declarator` 所声明的名称。

[注 1：关于显式特化和实例化的限制，请分别参阅 13.9.4 和 13.9.3。— 注释结束]

[注 2：在块作用域内或作为函数参数的没有存储类限定符的变量默认具有自动存储期 (6.7.5.4)。— 注释结束]

`thread_local` 标识符表示该名称具有线程存储期 (6.7.5.3)。它应仅应用于命名空间或块作用域变量的声明、结构绑定声明 (9.6) 或静态成员的声明。当 `thread_local` 应用于块作用域变量时，如果 `decl-spec-scope` 中没有出现其他存储类限定符，则该存储类限定符为 `static`。

`static` 限定符应仅应用于变量或函数的声明、结构绑定声明 (9.6) 或匿名联合体的声明 (11.5.2)。块内部不能有静态函数声明，也不能有静态函数参数。在局部变量声明中使用 `static` 用于使其具有静态存储期 (6.7.5.2)，除非伴有 `thread_local` 限定符，后者将声明变量具有线程存储期 (6.7.5.3)。`static` 限定符可用于类成员声明 (11.49)，其影响另有描述。对于用 `static` 限定符声明的名称的链接，请参阅 6.6。

`extern` 限定符应仅应用于变量或函数的声明。`extern_specifier` 不应用于类成员或函数参数的声明。对于用 `extern` 限定符声明的名称的链接，请参阅 6.5。

[注 3：`extern` 关键字也可能用于显式特化和链接规范，在这些语境下它不是一个存储类限定符。— 注释结束]

给定实体的连续声明所蕴含的链接应当保持一致。也就是说，在给定的作用域内，每个共享相同名称或相同名称重载的声明应意味着相同的链接。

示例 1：
```c
static char f();    // f() 有内部链接
char f();               // f() 仍然具有内部链接
{ ... / }
char g();              // g() 有内部链接
static char g();       // 错误：链接不一致
{ ... / }
void h();
inline void h();      // 外部链接
inline void l0();
void l0();             // 外部链接
inline void m();
extern void m();      // 外部链接
static void n();
inline void n();      // 内部链接
static int a;
int a;                 // a 有内部链接
                        // 错误：重复定义
static int b;
// b 有内部链接
extern int b;         // b 仍然具有内部链接
int c;                // c 有外部链接
static int c;          // 错误：链接不一致
extern int d;         // d 有外部链接
static int d;          // 错误：链接不一致
```
已声明但未定义的类名用于 `extern` 声明。此类声明可以用于不需要类类型的方式。

[示例 2：
```c
struct S
extern S a;
extern S f();
extern void g(S);
void h() {
    g(a); // 错误：S 是不类型
    f();  // 错误：S 是不类型
}
```
`mutable` 限定符应仅出现在非静态数据成员的声明中，其类型既不是 `const` 修饰的也不是引用类型。

[示例 3：
```cpp
class X {
    mutable const int* p; // 正确
    mutable int* const q; // 错误
};
```
> 注意：类成员上的 `mutable` 限定符抵消了应用于对象的 `const` 限定符，并允许修改该可变成员 (6.8.4, 9.2.9)。

### 9.2.3 函数限定符 (Function specifiers)

1 函数限定符仅用于函数声明。
```text
function-specifier:
virtual
explicit-specifier:
explicit (constant-expression)
explicit
```
2 `virtual` 限定符仅用于非静态成员函数的声明；参阅 11.7。`explicit` 限定符仅用于类定义内部构造函数或转换函数的声明：11.4.2 和 11.4.3。

4 在 `explicit-specifier` 中，如果使用了 `const-declaration`，应转换为 `bool` 类型的常量表达式 (7.7)。不带常量表达式的 `explicit` 等同于 `explicit(true)`。如果常量为真，则该函数是显式的；否则，不是显式的。`explicit` 之后的标记被解析为 `explicit-specifier` 的。

### 9.2.4 typedef 限定符 (The typedef specifier)

1 包含 `decl-typedef` 限定符的声明用于命名目的 (6.2) 或复合 (6.8) 类型。`typedef` 限定符不应与除 `defining-type-specifier` 外的任何限定符组合，且不应用于参数声明 (9.3.4) 或函数定义 (9.5) 的 `decl-specifier-seq`。如果 `typedef` 限定符出现在没有声明符的声明中，则解析错误。

```
typedef:
identifier
simple-template-id
```
