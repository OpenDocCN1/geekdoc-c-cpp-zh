

```
constexpr int prev(int x)
{ return --x; }        // OK
constexpr int g(int x, int n) { // OK
  int r = 1;
  while (--n > 0) r *= x;
  return r;
}
```

— end example]

4 constexpr 构造函数的定义如果其函数体不是 = delete，则还应满足以下要求：

- (4.1) — 对于非委托构造函数，用于初始化非静态数据成员和基类子对象的每个构造函数都应为 constexpr 构造函数；
- (4.2) — 对于委托构造函数，目标构造函数应为 constexpr 构造函数。

[Example 3:

```
struct Length {
  constexpr explicit Length(int i = 0) : val(i) { }
private:
  int val;
};
```

— end example]

5 constexpr 析构函数的定义如果其函数体不是 = delete，则还应满足以下要求：

- (5.1) — 对于每个类类型或其（可能多维的）数组的子对象，该类类型应具有 constexpr 析构函数。

6 如果 constexpr 函数既不是默认的也不是模板，则在评估任何有效的显式常量求值表达式时，如果无法执行该函数调用的求值，则该函数格式错误，无需诊断。

[Example 4:

```
constexpr int f(bool b)
{ return b ? throw 0 : 0; }        // OK
constexpr int f() { return f(true); }    // ill-formed, no diagnostic required

struct B {
  constexpr B(int x) : i(0) { }          // x is unused
  int i;
};

int global;

struct D : B {
  constexpr D() : B(global) { }          // ill-formed, no diagnostic required
                                      // lvalue-to-rvalue conversion on non-constant global
};
```

— end example]

7 如果 constexpr 函数模板或类模板成员函数的实例化模板特化无法满足 constexpr 函数的要求，则该特化仍然是 constexpr 函数，即使对该函数的调用不能出现在常量表达式中。如果没有任何模板特化在作为非模板函数考虑时能够满足 constexpr 函数的要求，则该模板格式错误，无需诊断。

8 在给定上下文中对 constexpr 函数的调用在所有方面产生的结果都与在相同上下文中对等价的非 constexpr 函数的调用相同，只是

- (8.1) — constexpr 函数的调用可以出现在常量表达式中（7.7）并且
- (8.2) — 在常量表达式中不执行拷贝省略（11.10.6）。

> [Note 4: 声明函数为 constexpr 可能会改变表达式是否为常量表达式。这可能会间接导致在函数调用中 std::is_constant_evaluated 的调用产生不同的值。 — end note]

9 constexpr 和 consteval 说明符对 constexpr 函数的类型没有影响。

```
[Example 5:
    constexpr int bar(int x, int y)        // OK
    { return x + y + x*y; }
    // ...
    int bar(int x, int y)                 // error: redefinition of bar
    { return x * 2 + 3 * y; }
— end example]
```

10 在对象声明中使用 constexpr 说明符声明该对象为 const。该对象应具有字面类型并应被初始化。在任何 constexpr 变量声明中，初始化的完整表达式应为常量表达式（7.7）。constexpr 变量应具有常量销毁。

```
[Example 6:
    struct pixel {
        int x, y;
    };
    constexpr pixel ur = { 1294, 1024 };    // OK
    constexpr pixel origin;                 // error: initializer missing
— end example]
```

### 9.2.7 The constinit specifier [dcl.constinit]

1 constinit 说明符只能应用于具有静态或线程存储期的变量的声明。如果该说明符应用于变量的任何声明，则应应用于初始化声明。在初始化声明点处如果无法到达任何 constinit 声明，则无需诊断。

2 如果使用 constinit 说明符声明的变量具有动态初始化（6.9.3.3），则程序格式错误。

> [Note 1: constinit 说明符确保变量在静态初始化期间（6.9.3.2）进行初始化。 — end note]

```
[Example 1:
    const char * g() { return "dynamic initialization"; }
    constexpr const char * f(bool p) { return p ? "constant initializer" : g(); }
    constinit const char * c = f(true);      // OK
    constinit const char * d = f(false);     // error
— end example]
```

### 9.2.8 The inline specifier [dcl.inline]

1 inline 说明符只能应用于变量或函数的声明。

2 带有 inline 说明符的函数声明（9.3.4.6, 11.4.2, 11.9.4）声明一个内联函数。inline 说明符指示实现在调用点执行函数体的内联替换优于通常的函数调用机制。实现不必在调用点执行此内联替换；然而，即使省略了此内联替换，本小节中指定的内联函数的其他规则仍应得到尊重。

> [Note 1: inline 关键字对函数链接没有影响。在某些情况下，内联函数不能使用具有内部链接的名称；参见 6.6。 — end note]

3 带有 inline 说明符的变量声明声明一个内联变量。

4 inline 说明符不得出现在块作用域声明或函数参数的声明上。如果 inline 说明符用于友元函数声明中，则该声明应为定义或该函数之前已被声明为 inline。

5 如果在首次声明为 inline 时可以到达函数或变量的定义，则程序格式错误。如果在一种定义中具有外部或模块链接的函数或变量被声明为 inline

for detailed semantics. In general, the semantics of volatile are intended to be the same in C++ as they are in C. — end note]

### 9.2.9.3 Simple type specifiers [dcl.type.simple]

1 简单类型说明符为

- simple-type-specifier:
    - nested-name-specifieropt type-name
    - nested-name-specifier template simple-template-id
    - decltype-specifier
    - placeholder-type-specifier
    - nested-name-specifieropt template-name
    - char
    - char8_t
    - char16_t
    - char32_t
    - wchar_t
    - bool
    - short
    - int
    - long
    - signed
    - unsigned
    - float
    - double
    - void
- type-name:
    - class-name
    - enum-name
    - typedef-name

2 placeholder-type-specifier 是用于推导类型的占位符（9.2.9.6）。形式为 typenameopt nested-name-specifieropt template-name 的 type-specifier 是用于推导类类型的占位符（9.2.9.7）。nested-name-specifier（如果有）应为非依赖的，且 template-name 应命名一个可推导的模板。可推导的模板要么是类模板，要么是其定义类型 id 形式为

typenameopt nested-name-specifieropt templateopt simple-template-id

的别名模板，其中 nested-name-specifier（如果有）为非依赖的，且 simple-template-id 的 template-name 命名一个可推导的模板。

> [Note 1: 在会执行类模板参数推导的上下文中（13.8.2），injected-class-name 从不被解释为 template-name。 — end note]

其他简单类型说明符指定先前声明的类型、从表达式确定的类型或基本类型之一（6.8.2）。表 14 总结了简单类型说明符的有效组合以及它们指定的类型。

3 当允许多个简单类型说明符时，它们可以与其它 decl-specifier 以任意顺序自由混合。

> [Note 2: char 类型的对象是否表示为有符号或无符号量是实现定义的。signed 说明符强制 char 对象为有符号；在其他上下文中它是冗余的。 — end note]

### 9.2.9.4 Elaborated type specifiers [dcl.type.elab]

- elaborated-type-specifier:
    - class-key attribute-specifier-seqopt nested-name-specifieropt identifier
    - class-key simple-template-id
    - class-key nested-name-specifier templateopt simple-template-id
    - elaborated-enum-specifier
- elaborated-enum-specifier:
    - enum nested-name-specifieropt identifier

1 attribute-specifier-seq 不应出现在 elaborated-type-specifier 中，除非后者是声明的唯一组成部分。如果 elaborated-type-specifier 是声明的唯一组成部分，则该声明是

