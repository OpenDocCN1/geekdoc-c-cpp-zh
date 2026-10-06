

# ISO/IEC 14882:2017(E)

```cpp
// C++ 语言链接；参数类型为“指向 C 函数的指针”

FUNC_c mf2;
// 函数 mf2 的名称和该函数的类型具有
// C++ 语言链接

static FUNC_c* q;
// 数据成员 q 的名称具有 C++ 语言链接，且
// 数据成员的类型是“指向 C 函数的指针”

extern "C" {
class X {
    void mf2();
    void mf2(void(*())());
    // 函数 mf 的名称和该函数的类型具有
    // C++ 语言链接；
    // 函数 mf2 的名称具有 C++ 语言链接；
    // 参数类型为“指向 C 函数的指针”
};
// 示例结束;
```

5 如果两个声明将相同名称和参数列表（11.3-5）的函数声明为同一命名空间的成员，或将相同名称的对象声明为同一命名空间的成员，且声明提供了不同的语言链接，则该程序是非良的（ill-formed）。如果这些声明出现在不同的编译单元中，则不需要进行诊断。除 C++ 语言外，没有链接规范的函数不应出现在该函数的第一个链接规范之前。在看到链接规范之前，可以不带链接规范地声明一个函数；在早先声明中显式指定的链接不属于此类函数声明。

6 具有特定名称的函数最多有一个 C 语言链接。出现在不同命名空间中的具有相同名称和 C 语言链接（忽略其修饰的名称）的函数两个声明指向同一个函数。在全局作用域内具有相同名称且具有 C 语言链接的变量两个声明指向不同的变量，除非两个声明都表示同一个实体，否则该程序是非良的；全局作用域内应以相同名称声明实体，除非具有 C 语言链接的实体与具有 C 语言链接的实体名称相同（忽略各自修饰的名称）；如果声明出现在不同的编译单元中，则不需要进行诊断。*注意：对于具有 C 语言链接的给定名称，程序中最多出现一个定义（见 6.3）；这意味着一个实体不能在多个命名空间作用域中定义。* 节点结束；示例：

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

§ 10.5

©ISO/IEC 2017 保留所有权利

193

# ISO/IEC 14882:2017(E)

```cpp
extern "C" int h() { return 97; } // 具有 C 语言链接的函数 h 的定义
// A::h 和 h 指向同一个函数
// 示例结束[]

- 7 直接包含在链接规范中的声明，在确定所声明名称的链接以及其是否为定义时，被视为包含了 `extern` 限定符 (10.1.1)。此类声明不应指定存储类型。[示例：
extern "C" double f(); // 错误
static double f();
extern "C" int i; // 声明
{
} // 定义
extern "C" static void g(); // 错误
// 示例结束[]]

- 8 [注意：由于链接语言是函数类型的一部分，通过 C 函数的指针进行间接引用时，结果值被视为一个 C 函数的。— 注意结束]
9 从 C++ 到其他语言定义的对象，以及从其他语言到 C++ 对象的链接取决于实现并取决于语言。只有当两种语言的对象布局策略足够相似时，才能实现此类链接。

## 10.6 属性 [dcl.attr]

## 10.6.1 属性语法和语义 [dcl.attr.grammar]

- 1 属性为各种源构造结构（如类型、变量、名称、块或编译单元）指定附加信息。
attribute-specifier-seg:
attribute-specifier-seq_opt attribute-specifier
attribute-specifier:
[[ attribute-using-prefix_opt attribute-list ]]
alignment-specifier:
alignment-specifier:
alignas (type-id, ...opt)
alignas (constant-expression ...opt)
attribute-using-prefix:
using attribute-namespace :
attribute-list:
attribute-list_opt
attribute-list , attribute_opt
attribute:
attribute , ...
attribute-list , attribute ...
attribute:
attribute-token attribute-argument-clause_opt
attribute-token:
identifier
attribute-scoped-token:
attribute-scoped-token:
attribute-namespace :: identifier

attribute-namespace:
identifier

attribute-argument-clause:
balanced-token-seq-opt ]

balanced-token-seq:
balanced-token
balanced-token-seq-balanced-token

balanced-token:
 { balanced-token-seq-opt }
 { balanced-token-seq-opt }
 圆括号、中括号或大括号以外的任何字符

- 2 如果 attribute-specifier 包含 attribute-using-prefix，则 N 不应包含 attribute-scoped-token，且 attribute-list 中的每个 attribute-token 都被视为其标识符带有缀 N；N 是 attribute-using-prefix 中指定的 attribute-namespace。（注意：此规则不限制 attribute-using-prefix 如何影响 attribute-clause 中的标记。— 注意结束）示例：

```cpp
using CC: opt(1), [[debug]]
void f() {
using CC: opt(1)) [[CC::debug]] // 等于 [[CC:opt(1)] [[CC::debug]]
using G: opt(1));
// 错误：不能结合 using 和 scoped attribute-token
}
```

- 3 对于每个 attribute-list，只有当指定了 balanced-token-seq 的形式时，允许出现省略号。— 注意结束

- 4 在 attribute-list 中，省略号 (17.3.3)。不包含任何属性的 attribute-specifier 无影响。attribute-token 在 attribute-list 中出现的顺序并不重要。如果考虑了关键字（5.11）或替代方案（5.10），则对 attribute-token 中包含的任何标识符不执行查找（6.4），它被视为。

- 5 不包含任何属性的 attribute-specifier 被认为属于某个实体，如果 attribute-specifier-seq 属于某个实体，且 attribute-specifier 不适用于该实体，则该程序是非良的。attribute-specifier 决定了 attribute-argument-clause。

- 6 具有相同名称且具有 C 语言链接的函数两个声明（忽略其修饰的名称）出现在不同的命名空间中指向同一个函数。全局作用域内具有相同名称且具有 C 语言链接的变量两个声明指向不同的变量，除非两个声明都表示同一个实体，否则该程序是非良的；全局作用域内应以相同名称声明实体，除非具有 C 语言链接的实体与具有 C 语言链接的实体名称相同（忽略各自修饰的名称）；如果声明出现在不同的编译单元中，则不需要进行诊断。*注意：对于具有 C 语言链接的给定名称，程序中最多出现一个定义（见 6.3）；这意味着一个实体不能在多个命名空间作用域中定义。* 示例：

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

§ 10.5

©ISO/IEC 2017 保留所有权利

193

# ISO/IEC 14882:2017(E)

```cpp
extern "C" int h() { return 97; } // 具有 C 语言链接的函数 h 的定义
// A::h 和 h 指向同一个函数
// 示例结束[]
```

- 7 直接包含在链接规范中的声明，在确定所声明名称的链接以及其是否为定义时，被视为包含了 `extern` 限定符 (10.1.1)。此类声明不应指定存储类型。[示例：
extern "C" double f(); // 错误
static double f();
extern "C" int i; // 声明
{
} // 定义
extern "C" static void g(); // 错误
// 示例结束[]]

- 8 [注意：由于链接语言是函数类型的一部分，通过 C 函数的指针进行间接引用时，结果值被视为一个 C 函数的。— 注意结束]
9 从 C++ 到其他语言定义的对象，以及从其他语言到 C++ 对象的链接取决于实现并取决于语言。只有当两种语言的对象布局策略足够相似时，才能实现此类链接。

## 10.6 属性 [dcl.attr]

## 10.6.1 属性语法和语义 [dcl.attr.grammar]

- 1 属性为各种源构造结构（如类型、变量、名称、块或编译单元）指定附加信息。
attribute-specifier-seg:
attribute-specifier-seq_opt attribute-specifier
attribute-specifier:
[[ attribute-using-prefix_opt attribute-list ]]
alignment-specifier:
alignment-specifier:
alignas (type-id, ...opt)
alignas (constant-expression ...opt)
attribute-using-prefix:
using attribute-namespace :
attribute-list:
attribute-list_opt
attribute-list , attribute_opt
attribute:
attribute , ...
attribute-list , attribute ...
attribute:
attribute-token attribute-argument-clause_opt
attribute-token:
identifier
attribute-scoped-token:
attribute-scoped-token:
attribute-namespace :: identifier

attribute-namespace:
identifier

attribute-argument-clause:
balanced-token-seq-opt ]

balanced-token-seq:
balanced-token
balanced-token-seq-balanced-token

balanced-token:
 { balanced-token-seq-opt }
 { balanced-token-seq-opt }
 圆括号、中括号或大括号以外的任何字符

- 2 如果 attribute-specifier 包含 attribute-using-prefix，则 N 不应包含 attribute-scoped-token，且 attribute-list 中的每个 attribute-token 都被视为其标识符带有缀 N；N 是 attribute-using-prefix 中指定的 attribute-namespace。（注意：此规则不限制 attribute-using-prefix 如何影响 attribute-clause 中的标记。— 注意结束）示例：

```cpp
using CC: opt(1), [[debug]]
void f() {
using CC: opt(1)) [[CC::debug]] // 等于 [[CC:opt(1)] [[CC::debug]]
using G: opt(1));
// 错误：不能结合 using 和 scoped attribute-token
}
```

- 3 对于每个 attribute-list，只有当指定了 balanced-token-seq 的形式时，允许出现省略号。— 注意结束

- 4 在 attribute-list 中，省略号 (17.3.3)。不包含任何属性的 attribute-specifier 无影响。attribute-token 在 attribute-list 中出现的顺序并不重要。如果考虑了关键字（5.11）或替代方案（5.10），则对 attribute-token 中包含的任何标识符不执行查找（6.4），它被视为。

- 5 不包含任何属性的 attribute-specifier 被认为属于某个实体，如果 attribute-specifier-seq 属于某个实体，且 attribute-specifier 不适用于该实体，则该程序是非良的。attribute-specifier 决定了 attribute-argument-clause。

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

## 10.6.2 对齐规范

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

alignas(T) aligns(A) T[N]; 确保最终请求的对齐不会弱于 alignof(T)，并且

