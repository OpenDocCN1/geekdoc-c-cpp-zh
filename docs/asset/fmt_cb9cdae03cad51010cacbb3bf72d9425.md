
- 2 退出作用域（无论如何汇聚）时，在该作用域内已构造的自动存储期对象 (`3.7.3`) 按构造的反序析构。[注：临时变量，见 `2.2`-- 注结束] 退出循环、块或跳过已初始自动存储期变量涉及在转移处存在但在目标处不存在的对象的析构。（进入块见 `6.7`）。

[注：然而，程序可以（通过调用 `std::exit()` 或 `std::abort()` (`18.5`) 等）终止而不析构自动存储期的类对象。— 注结束]

## 6.6.1 break 语句 [stmt.break]

`break` 语句只能出现在迭代语句或 `switch` 语句中。

## 6.6.2 continue 语句 [stmt.cont]

`continue` 语句只能出现在迭代语句中，并导致控制传递到最小迭代语句的末尾。

```cpp
while (foo) {
    ...
    continue;
}
```

## 6.6.3 return 语句 [stmt.return]

`return` 语句返回调用者。

## 6.6.4 goto 语句 [stmt.goto]

`goto` 语句无条件地将控制转移到标签。

## 6.7 声明语句 [stmt.dcl]

1 1 声明语句向块中引入一个或多个标识符；其形式为

```cpp
declaration-statement:
block
```

# 歧义消除

语法在涉及表达式语句和声明时存在一种歧义：一个以函数风格显式类型转换（`5.2.3`）作为其最左侧子表达式的表达式语句，与第一个声明符以 `{` 开头的声明是无法区分的。在这种情况下，该语句是一个声明。

[注：如果该语句在语法上是一个声明，则不存在歧义，但此规则不适用。可能需要检查该语句以确定是否属于此类情况。这解决了许多示例的含义。[示例：假设 `T` 是一个简单类型限定符（`7.1.6`）。

```cpp
T(a)->m = 7;               // 表达式语句
T(a++);                   // 表达式语句
T(a,5)<;                // 表达式语句
T(*d)(int);             // 声明
T(e)[5];                // 声明
T(f) = { 1, 2 };         // 声明
T(*g)(double(3));      // 声明
```
在最后一个示例中，`g` 是指向 `T` 的指针，被初始化为 `double(3)`。从语义角度来看这也是错误的，但这不影响语法分析。—— 示例结束

其余情况都是声明：[示例：

```cpp
class T {
//
public:
// 
T();
T(int);
T(int, int);
T(a)                     // 声明
T(*b)(0);                  // 声明
T(c)=7;                   // 声明
T(d,e,f=3;               // 声明
extern int h;
T(h,2);\ // 声明
```
—— 示例结束—— 注

歧义消除纯粹是语法的；也就是说，语句中出现的名称含义（无论是否为类型名）通常不会通过歧义消除在使用或改变。通过实例化类模板来确定限定名是否为类型名。歧义消除发生在解析之前，被歧义消除为声明的语句可能是一个错误的声明。如果在解析期间，模板参数中的名称绑定方式与在尝试解析期间相同，则该程序是错误的。[注：这仅当该名称在声明中定义时才可能发生。—— 注] |示例：

```cpp
struct T1 {
T1 operator(int x) { return T1(x);
int operator=(int x) { return x; }
T1(int x) {
};
struct T2 { T2(int) { };
int a, (*b)(T2))(int), c, d;
void f() {
```
```
// 歧义消除要求将其解析为声明：
// T1(a) = 3,
// T2(4), // T2 将声明为
// (*(*b)(T2(c)))((int(d)); // 类型为 T1 的变量
// 但将不允许
// 声明的最后部分
// 正确解析
// 因为因为它取决于
// T2 是否为类型名
}
-- 示例结束]
```

# 7 声明

声明通常指定名称如何被解释。声明具有声明-seq：
`declaration`
`declared-seq-declaration`
`declared:`
`block-declaration`
`function-definition`
`template-declaration`
`explicit-instantiation`
`explicit-specialization`
`linkage-specification`
`namespace-definition`
`empty-declaration`
`attribute-declaration`
`block-declaration:`
`simple-definition`
`asm-definition`
`namespace-alias-definition`
`using-directive`
`static_assert-declaration`
`alias-declaration`
`opaque-enum-declaration`
`alias-declaration:`
`using identifier attribute-specifier-seq-opt* type-id;`
`simple-declaration:`
`decl-specifier-seq-opt init-declarator-list-opt`
`attribute-specifier-seq decl-specifier-seq-opt init-declarator-list`
`static_assert-declaration:`
`static_assert ( constant-expression )`
`static_assert ( constant-expression , string-literal )`
`non-empty-declaration:`
`attribute-declaration:`
`attribute-specifier-seq;`

> [注：`asm` 声明在 `7.4` 中描述，链接 限定符在 `7.5` 中描述。函数定义在 `8.4` 中描述，模板声明在第 `14` 节中描述。命名空间定义在 `7.3.1` 中描述，`using` 声明在 `7.3.3` 中描述，`using` 指令在 `7.3.4` 中描述。—— 注]

- 2 简单声明
`attribute-specifier-seq decl-specifier-seq init-declarator-list-opt;`

它分为三部分。属性在 `7.6` 中描述。`decl-specifier`（`decl-specifier-seq` 的主要部分）在 `7.1` 中描述。声明符（`init-declarator-list` 的组件）在第 `8` 节中描述。简单声明中的 `attribute-specifier-seq` 属于 `init-declarator-list` 中声明符所声明的每个实体。[注：在实体的声明中，属于该实体的属性出现在声明的开头，以及该声明的声明符-id 之后。—— 注] [示例：

```cpp
-- [noreturn] void f() {noreturn}; // OK
```
-- 示例结束

- 3 除另有规定外，声明符-声明的含义由实现定义。

- 4 声明发生在一个作用域（`3.3`）中；作用域规则在 `3.4` 中总结。定义类、命名空间、模板或函数的声明内部包含一个或多个嵌套作用域。这些嵌套作用域内部可以声明。除非另有说明，第 `7` 节关于声明组件的表述仅指未嵌套在当前作用域内的声明组件。

- 5 在简单声明中，当声明类（第 `9` 节）或枚举（`7.2` 节）时，可选的声明符列表可以省略；也就是说，如果 `decl-specifier-seq` 包含类限定符、带有类键限定符（`9`）或枚举限定符。在这种情况下，每当存在类限定符或枚举限定符时，这些限定符中的标识符是声明的。限定符可能引入一个或多个名称，或重新声明由声明引入的名称。[示例：

```cpp
enum {}; // 错误
typedef class {}; // 错误
```
-- 示例

- 6 在静态声明中，常量表达式应该是可以常量转换为真（`5.2`）的常量表达式（第 `4` 节）。如果表达式的值转换为真，则该声明没有作用。如果程序是错误的，生成的诊断信息（`1.4`）应该包含字符串字面量的文本（如果提供了），除了基础字符集（`2.3`）之外的字符出现在诊断信息中。[示例：

```cpp
static_assert(sizeof(long) >= 8, "64-bit code required.");
```
-- 示例

- 7 空声明没有作用。

- 8 列表中的每个声明符恰好包含一个声明符-id，它是由该声明符声明的名称，以及声明声明的名称。`decl-specifier-seq` 中的限定符（`7.1.6`）和初始化声明符的递归结构描述了一个类型（`8.3`），该类型与初始化声明符声明的名称相关。

- 9 如果 `decl-specifier-seq` 包含 `typedef` 限定符，则该声明称为 `typedef` 声明，每个初始化声明符的称为 `typedef` 名称，与其关联类型相同（`7.1.3`）。如果 `decl-specifier-seq` 不包含 `typedef` 限定符，如果与名称相关的类型是类型（`8.5`），则称为函数声明，否则称为对象声明。

- 10 通用形式中的语法组件添加到函数声明中形成函数定义。然而，对象声明除非包含 `extern` 限定符且没有初始化器（`3.1`），否则需要适当的存储以及任何适当的初始化（`8.5`）。

- 11 仅在函数的构造函数、析构函数和转换中省略 `decl-specifier-seq`。（`9`）不支持 C 的隐式规则。

## 7.1 限定符

声明中使用的限定符有：

```
decl-specifier:
  storage-class-specifier
  type-specifier
  function-specifier
  friend
  typedef
  const
decl-specifier-seq:
  decl-specifier attribute-specifier-seq-opt
  decl-specifier attribute-specifier-seq
```

`decl-specifier-seq` 中遇到的可选 `decl-specifier-seq` 属于前一个限定符确定的类型（`8.3`）。`attribute-specifier-seq` 仅影响它所在的声明，而不影响使用相同类型的其他声明。

- 2 每个限定符在声明的完整 `decl-specifier-seq` 中最多出现一次，`typedef` 可以出现两次。

- 3 如果在解析 `decl-specifier-seq` 时遇到类型名，当且仅当 `decl-specifier-seq` 中没有 `cv` 限定符以外之前的类型限定符时，它被解释为 `decl-specifier-seq` 的一部分。该序列应如文所述自一致。[示例]：

```cpp
typedef char Pc;
  static Pc; // 错误：缺少名称
```
在这里，声明 `Pc` 是错误的，因为没有为该类型的静态变量指定名称。为了获得变量 `Pc`，必须存在一个 `const` 或 `volatile` 以外的类型限定符，以指示 `typedef` 名称 `Pc` 是正在被（重）声明的名称，而不是 `decl-specifier` 序列的一部分。例如：

```cpp
void f(const Pc); // void f(char const (不是 const char*)
void g(const int Pc); // void g(const int)
```
-- 示例

- 4 [注：`signed`, `unsigned`, `long` 和 `short` 默认隐含 `int`，出现在这些符号之后的类型名被视为正在被（重）声明的名称。[示例]：

```cpp
void h(unsigned int); // void h(unsigned int)
void k(unsigned int); // void k(unsigned int)
```
-- 示例

## 7.1.1 存储类限定符

存储类限定符是：

```
storage-class-specifier:
  register
  static
  thread_local
  extern
  volatile
```

给定的 `decl-specifier-seq` 中最多出现一个存储类限定符，`thread_local` 可以与 `static` 或 `extern` 同时出现。如果 `thread_local` 出现在变量的任何声明中，它应该出现在该实体的所有声明中。如果存储类限定符出现在 `decl-specifier-seq` 中，可以

- 匿名 `decl-specifier-seq` 不允许有 `typedef` specifier，且声明的 `init-declarator-list` 不为空（对于命名命名空间或全局命名空间中的匿名 union，其应声明为 `static` (`9.5`)）。存储类-specifier 适用于列表中每个 `mit-declarator` 声明的名称，而不适用于由其他 specifier 声明的任何名称。显式中除 `thread_load` 以外的存储类-specifier 不应在显式特化 (`14.7.3`) 或显式实例化 (`14.7.2`) 中指定。

2. `register` 标识符应仅应用于在块 (`6.3`) 中声明的变量或函数参数 (`4.4`)，如果该命名变量具有自动存储生存期 (`3.7.3`)。在块中或作为函数参数声明且未指定存储类 specifier 的变量默认具有自动存储生存期。

3. `register` 是对实现的一种提示，指示所声明的变量将被频繁使用。[注：该提示可以被忽略，在许多实现中，如果使用了变量的地址，它将被忽略。这一点有规定（参见 `D.2.`。）——注结束]

4. `thread_local` 标识符指示命名实体具有存储生存期 (`3.7.2`)。它应仅应用于命名空间作用域的变量名称或静态数据成员名称。当 `thread_local` 应用于块作用域的变量时，如果 `decl-specifier-seq` 中没有出现其他存储类-specifier，则隐含了该存储类-specifier。

5. `static` 标识符只能应用于变量和函数的名称，以及匿名 union (`9.5`)。块内不能有静态函数，也不有任何静态函数参数。静态声明声明变量具有静态存储生存期 (`3.7.1`)，除非用于 `thread_local` specifier 的声明中，此时则声明变量具有线程存储生存期 (`3.7.2`)。对于使用 `static` specifier 声明的名称的链接（linkage），参见 `9.4`。

6. `extern` 标识符只能应用于变量和函数的名称。`extern` 标识符不能用于类成员或函数参数的声明。使用 `extern` 标识符 声明的名称的链接，参见 `3.5`。[注：`extern` 关键字也可以用于显式实例化和链接规范，但在这些语文中，它不是存储类-specifier。——注结束]

7. 给定实体的连续声明所隐含的链接应当一致。也就是说，在给定的作用域内，每个声明变量名或同一函数名相同重载的声明应隐含相同的链接。然而，给定重载函数集中的每个函数可以有不同的链接，例如：

```cpp
static char f();           // f() 有内部链接
char f();
{ /* ... */ }         // f() 仍有内部链接
char* g();              // g() 有外部链接
static char* g()()
{ /* ... */ }         // 错误：链接不一致
void h();               // 外部链接
inline void h();
inline void l();       // 外部链接
void l();
inline void m();       // 外部链接
extern void m();
static void n();       // 内部链接
inline void n();
```

# § 7.1.1

# ©ISO/IEC N4296

```cpp
static int a; // a 有内部链接
int a; // 错误：重复定义
```

```cpp
static int b; // b 有内部链接
extern int b; // b 仍有内部链接
```

```cpp
int c; // c 有外部链接
static int c; // 错误：链接不一致
```

```cpp
extern int d; // d 有外部链接
static int d; // 错误：链接不一致
```

```cpp
// 示例结束
```

8. 延迟未定义（deferred undefined）的名称可以用于 `extern` 声明。此类声明只能在不需要完整类类型的方式上使用。[示例：

```cpp
struct S;
extern S a;
extern S f();
extern void g(S);
```

```cpp
void h() {
  g(a); // 错误：S 是不完整的
  f(); // 错误：S 是不完整的
}
```

```cpp
// 示例结束
```

9. `mutable` 标识符应出现在非静态数据成员 (`9.2`) 的声明中，其类型既不是 `const` 也不是引用类型。[示例：

```cpp
class X {
  mutable const int* p; // OK
  mutable int* const q; // 错误
};
```

```cpp
// 示例结束
```
