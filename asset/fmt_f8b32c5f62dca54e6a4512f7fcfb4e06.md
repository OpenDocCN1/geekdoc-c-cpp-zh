
- 7 直接包含在链接规范中的声明，在确定所声明名称的链接以及其是否为定义时，被视为包含了 `extern` 限定符 (10.1.1)。此类声明不应指定存储类型。[示例：
`extern "C" double f();` // 错误
`static double f();`
`extern "C" int i;` // 声明
{
} // 定义
`extern "C" static void g();` // 错误
// 示例结束[]]

- 8 [注意：由于链接语言是函数类型的一部分，通过 C 函数的指针进行间接引用时，结果值被视为一个 C 函数的。— 注意结束]
9 从 C++ 到其他语言定义的对象，以及从其他语言到 C++ 对象的链接取决于实现并取决于语言。只有当两种语言的对象布局策略足够相似时，才能实现此类链接。

## 10.6 属性 [dcl.attr]

## 10.6.1 属性语法和语义 [dcl.attr.grammar]

- 1 属性为各种源构造结构（如类型、变量、名称、块或编译单元）指定附加信息。
`attribute-specifier-seg`:
`attribute-specifier-seq_opt attribute-specifier`
`attribute-specifier`:
`[[ attribute-using-prefix_opt attribute-list ]]`
`alignment-specifier`:
`alignment-specifier`:
`alignas (type-id, ...opt)`
`alignas (constant-expression ...opt)`
`attribute-using-prefix`:
`using attribute-namespace :`
`attribute-list`:
`attribute-list_opt`
`attribute-list , attribute_opt`
`attribute`:
`attribute , ...`
`attribute-list , attribute ...`
`attribute`:
`attribute-token attribute-argument-clause_opt`
`attribute-token`:
`identifier`
`attribute-scoped-token`:
`attribute-scoped-token`:
`attribute-namespace :: identifier`

`attribute-namespace`:
`identifier`

`attribute-argument-clause`:
`balanced-token-seq-opt ]`

`balanced-token-seq`:
`balanced-token`
`balanced-token-seq-balanced-token`

`balanced-token`:
`{ balanced-token-seq-opt }`
`{ balanced-token-seq-opt }`
圆括号、中括号或大括号以外的任何字符

- 2 如果 `attribute-specifier` 包含 `attribute-using-prefix`，则 N 不应包含 `attribute-scoped-token`，且 `attribute-list` 中的每个 `attribute-token` 都被视为其标识符带有缀 N；N 是 `attribute-using-prefix` 中指定的 `attribute-namespace`。（注意：此规则不限制 `attribute-using-prefix` 如何影响 `attribute-clause` 中的标记。— 注意结束）示例：

```cpp
using CC: opt(1), [[debug]]

void f() {

using CC: opt(1)) [[CC::debug]] // 等于 [[CC:opt(1)] [[CC::debug]]

using G: opt(1));

// 错误：不能结合 using 和 scoped attribute-token

}
```

- 3 对于每个 `attribute-list`，只有当指定了 `balanced-token-seq` 的形式时，允许出现省略号。— 注意结束

- 4 在 `attribute-list` 中，省略号 (17.3.3)。不包含任何属性的 `attribute-specifier` 无影响。`attribute-token` 在 `attribute-list` 中出现的顺序并不重要。如果考虑了关键字（5.11）或替代方案（5.10），则对 `attribute-token` 中包含的任何标识符不执行查找（6.4），它被视为。

- 5 不包含任何属性的 `attribute-specifier` 被认为属于某个实体，如果 `attribute-specifier-seq` 属于某个实体，且 `attribute-specifier` 不适用于该实体，则该程序是非良的。`attribute-specifier` 决定了 `attribute-argument-clause`。

- 6 相同名称且具有 C 语言链接的函数两个声明（忽略其修饰的名称）出现在不同的命名空间中指向同一个函数。全局作用域内具有相同名称且具有 C 语言链接的变量两个声明指向不同的变量，除非两个声明都表示同一个实体，否则该程序是非良的；全局作用域内应以相同名称声明实体，除非具有 C 语言链接的实体与具有 C 语言链接的实体名称相同（忽略各自修饰的名称）；如果声明出现在不同的编译单元中，则不需要进行诊断。*注意：对于具有 C 语言链接的给定名称，程序中最多出现一个定义（见 6.3）；这意味着一个实体不能在多个命名空间作用域中定义。* 示例：

```cpp
int x;

namespace B {

    extern "C" int f();

    extern "C" int g() { return 1; }

    extern "C" int h();

    extern "C" int x0;

} // 非良的：与全局作用域对象同名

namespace B {

    extern "C" int f();

    extern "C" int g() { return 1; } // 非良的，具有 C 语言链接的函数 g 有两个定义

}

int A::f() { return 98; };
```

---

### 10.6.2 对齐规范

1 对齐限定符可以应用于变量或类，但不应应用于位域、函数参数或异常声明（18.3）。

2 当对齐限定符为 `alignas(constant-expression)` 形式时：
   (2.1) 常量表达式求值
   (2.2) 如果表达式没有计算出对齐值（6.11），或者它扩展了对齐而实现不支持，则该程序是非良的。

3 形式为 `alignas(type-id)` 的实体对齐限定符与 `alignas(alignof(type-id))` (8.3.6) 的效果相同。

4 实体的对齐要求严格取决于其对齐限定符指定的非零对齐；否则。

5 声明中所有对齐限定符的组合效果不应比如果省略所有对齐限定符时对所声明实体所要求的对齐要弱。[示例：

```cpp
struct aligns(1) U {

struct aligns(16) {

 S;

};

// 错误：U 的对齐比如果省略 aligns(1) 时要弱
```

6 如果实体的定义具有对齐限定符，任何非定义声明的实体都应指定等效对齐或不指定对齐限定符。相反，如果实体的任何声明具有对齐限定符，则该实体的声明都应具有等效对齐。如果实体在不同的编译单元具有不同的对齐限定符，则需要进行诊断。[示例：

```cpp
// 编译单元 1：
struct S { int x; } s, *p = &s;

// 编译单元 2：
struct aligns(16) S;

extern S p;

// 错误：S缺少定义，不需要诊断
```

7 [示例：一个对齐为 A 且包含 N 个类型 T 元素的对齐缓冲区可以声明为：

`alignas(T) aligns(A) T[N];` 确保最终请求的对齐不会弱于 `alignof(T)`，并且

# ISO/IEC 14882:2017(E)

因此该程序将是非形式的 — 示例结束

+ 8 [示例:
`alignas(double) void f();`
`alignas(double) unsigned char c(sizeof(double));`
`extern unsigned char c(sizeof(double));`
`alignas(float)`
    `extern unsigned char c(sizeof(double));`
— 示例结束]

```
// error: alignment applied to function

// array of characters, suitably aligned for a double

// no alignment necessary

// error: different alignment in declaration
```

### 10.6.3 dependency [dcl.attr.dep]

+ 1 属性 `carries-dependency` 指定了依赖向函数内部和外部的传播。它在每个属性列表中最多可以出现一次，且不应存在属性参数子。该属性可以应用于函数声明或 lambda 表达式中参数声明的声明符标识，在这种情况下，它指定了参数的初始化携带依赖到该对象的 (4.7) 每一个值到值的转换 (7.1)。该属性也可以应用于函数声明的声明符标识，在这种情况下，它指定了返回值（如果有）携带依赖到函数表达式的求值。

+ 2 如果函数的任何声明都为其声明符标识指定了 `carries-dependency` 属性，则该函数的第一个声明应为其声明符标识指定 `carries-dependency` 属性。此外，如果一个函数的第一个声明为某个翻译单元中的参数指定了 `carries-dependency` 属性，且其其中一个参数在同一函数的第一个声明中被声明为 `carries-dependency` 属性，或者其其中一个参数在另一个翻译单元的第一个声明中未声明为 `carries-dependency` 属性，则该程序是非形式的，且不需要诊断信息。

+ 3 [注：`carries_dependency` 属性不会改变程序的含义，但可能会生成更高效的代码。 — 笔记结束]

+ 4 [示例:
/* 翻译单元 A. */

```
struct foo { int *a; int *b; };

::atomic<struct foo*> foo_head[10];

foo_array[10][10];

[[carries_dependency]] struct foo f(int i) {

    return foo_head[i].load(memory_order_consume);

}

int g(int* x, int* y [[carries_dependency]]) {

    return kill_dependency(foo_array[x][y]);

}
```

/* 翻译单元 B. */

```
[[carries_dependency]] struct foo f(int i);

int g(int* x, int* y [[carries_dependency]]);
```

```
int c = 3;

void h(int i) {

    struct foo *p;

p = f(i);

do_something_with(g(&c));
```

对函数 f 的依赖依赖意味着返回值携带一个离开 f 的依赖，因此实现不需要对 f 施加排序限制。f 的实现及其调用者可以保留依赖，而不是发出硬件内存顺序指令（即屏障）。函数 g 的第二个参数具有 `carries_dependency` 属性，但其第一个参数没有。此外，f 第一次调用 g 携带一个进入 g 的依赖，但其第二次调用则不携带。实现 可能会在第二次调用 g 之前插入一个屏障。 — 示例结束]

## 10.6 Deprecated 属性（弃用属性）

+ 1 属性标记 `deprecated` 可用于标记尽管仍在使用但由于某些原因不建议使用的名称和实体。[注：特别地，`deprecated` 最适用于被认为过时或不安全的名称和实体。 — 笔记结束] 属性参数子可以存在，如果存在，它应具有以下形式：
( string-literal )
[注：属性参数子中的字符串字面量可以用来解释弃用的理由和/或建议一个替换的实体。 — 笔记结束]

+ 2 该属性可以应用于类、类型定义名、变量、非静态数据成员、函数、命名空间、枚举成员或模板语句的声明。

+ 3 使用 `deprecated` 属性声明的名称或实体可以带有该属性重新声明，反之亦然。[注：在声明一个实体后，可以通过子声明将该属性标记为弃用。允许使用不同形式的属性进行重新声明。 — 笔记结束]允许使用不同形式的属性（带有或不带属性参数子）进行重新声明。 — 笔记结束][实现可以使用 `deprecated` 属性，在程序引用了该属性以外的名称或实体；或者指定了该属性的声明时，减少诊断信息。应用于名称或实体的任何 `deprecated` 属性的属性参数子。 — 笔记结束]

## 10.6.5 Fallthrough 属性（穿透属性）

+ 1 属性标记 `fallthrough` 可应用于空语句 (9.2)；此类语句为穿透语句。该语句在每个属性列表中最多出现一次，且不应存在属性参数子。穿透语句只能出现在 `switch` 语句中，其标签是该 `switch` 语句的 `case` 或 `default` 标签。如果没有这样的语句，程序可能是非形式的。

+ 2 [注：使用穿透语句目的是抑制实现可能对从另一个执行路径可的 `case` 或 `default` 标签发出的警告。 — 笔记结束]

```cpp
void f(int n) {

void g(int i);

switch (n) {

case 1:

case 2:

case 3:

case 4:

    i();

    [[fallthrough]];

}
```

## 10.6.6 Maybe unused 属性（可能未使用属性）

属性标记 `maybe_unused` 表示某个名称或实体是有意未使用的。它在每个属性列表中最多出现一次，且不应存在属性参数子。

该属性可以应用于类、类型定义名、变量、非静态数据成员、函数、枚举或枚举成员的声明。

[注：对于标记为 `maybe_unused` 的实体，实现不应发出关于该实体未使用的警告，或在存在该属性的情况下使用该属性的警告。 — 笔记结束]

未使用 `maybe_unused` 属性的名称或实体可以带有该属性重新声明，反之亦然。实体在第一个标记它的声明后即被视为已标记。

[示例]:

```
[[maybe_unused]] void func([[maybe_unused]] bool thing1,

    [[maybe_unused]] bool thing2 {

    [[maybe_unused]] bool b = thing1 && thing2;

    assert(b);

};
```

当 b 未使用时，无论是否定义了 DEBUG，实现都应正常工作。 — 示例结束

## 10.6.7 Nodiscard 属性（禁止忽略属性）

属性标记 `nodiscard` 可应用于函数声明中的*声明符标识*，或类或枚举的声明。它在每个属性列表中最多出现一次，且不应存在属性参数子。

[注：一个 `nodiscard` 是一个调用了先前声明为 `nodiscard` 的函数的表达式，或其返回类型是标记为 `nodiscard` 的可能求值的类或枚举。`nodiscard` 作为可能求值的表达式出现（不建议显式转换为类 S）。在这种情况下实现应发出警告。这通常是因为丢弃 `nodiscard` 的返回值会有意想不到的后果。 — 笔记结束]

[示例]:

```
struct { error_info { /* ... */ };

error_info enable_missile_safety_mode();

void launch_missiles();

void test_missiles();

missile_safety_mode(); // 鼓励警告

launch_missiles();

er_info foo(); // 不鼓励警告：因为该（引用）返回类型或函数都没有声明为 nodiscard
```

# ISO/IEC 14882:2017(E)

### 10.6.8 attribute-token noreturn

属性-token `noreturn` 指定函数不返回。它在每个 `attribute-list` 中最多出现一次，且不应存在 `attribute-argument-clause`。该属性可以应用于函数声明中的 `declator-id`。如果该函数的任何声明指定了 `noreturn` 属性，则该函数的第一次声明也应指定 `noreturn` 属性。如果在任何一个编译单元中声明函数时未带 `noreturn` 属性，则程序是格式错误的（ill-formed），不需要诊断。

如果调用函数 f，而 f 之前带有 `noreturn` 属性声明，且 f 最终返回了，则行为是未定义的。[注：该函数可能通过抛出异常来终止。] — 结束注释|注：如果标记为 [noreturn] 的函数可能返回，实现应当发出警告。 — 结束注释

+ 3 [示例：]

```cpp
[[noreturn]] void f() {
    throw "error";
    // OK
}

[[noreturn]] void q(int i) {
    // 如果使用的参数 <= 0，行为是未定义的
    if (i > 0)
        throw "positive";
}
```

— 结束示例

# ISO/IEC 14882:2017(E)

# 11 声明符 [dcl.decl]

声明符在声明中声明单一的变量、函数或类型。声明中出现的 *init-declarator-list* 是一个逗号分隔的声明符序列，每个声明符都可以有一个初始化器。
