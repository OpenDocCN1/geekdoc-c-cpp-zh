
字面量指示所需的链接。除 "C" 或 "C++" 以外的字面量是条件支持的，由实现定义。

> 注 2：对于实现未知的字面量的链接声明需要声明。（等待，此处 OCR 乱码，根据标准 C++ 规则修正：对于实现未知的字面量的链接声明需要声明。）

> 注 3：建议字面量的拼写取自定义语言。例如，Ada（ADA）和 Fortran（FORTRAN），取决于实现。 — 注结束

每个实现应为 C 语言编写的函数提供链接，“C”，并为 C++ 函数提供链接。

[示例
```cpp
complex(complex);

extern "C" {

  double(double);

} // 默认 C 链接
```

声明不直接包含在链接声明中。在非 "C++" 链接的声明中出现的声明是条件支持的，具有实现语义。链接声明可以嵌套。当链接声明嵌套时，最内部的决定语言链接。链接声明仅发生在命名空间作用域内 (6.4)。在链接声明中，指定的语言链接适用于所有声明的函数、具有外部链接的函数名以及链接声明内的变量名。

[示例
```cpp
extern "C" void f1(*pf)(int)); // pf 是 C 函数的指针

extern "C" typedef void FUNC(); // f2 名称具有 C++ 链接

extern "C" FUNC f3; // 变量 pf2 的名称及其函数类型具有 C++ 语言链接

void (*pf2)(FUNC*); // pf2 是一个一个 C++ 函数指针

extern "C" {

  static void f4(); // f4 名称具有内部链接（非 C 链接）

} // 函数类型具有语言链接。
```

```cpp
extern "C" void f5() {

    extern void f4();

    // OK：名称链接（内部）和函数链接（C 语言链接）
    // 来自之前的声明。

}
```

```cpp
extern void f4();

// OK：名称链接（内部）和函数链接（C 语言链接)
// 来自之前的声明。 
```

```cpp
void f6() {

    extern void f4();

    // OK：名称链接（内部）和函数链接（C 语言链接)
    // 来自之前的声明。

}

// 示例结束
```

在确定成员名称和类成员函数类型的语言链接时，忽略 C 语言链接。

示例 3:
```cpp
extern "C" typedef void FUNC_c;

class C {

    void mf1(FUNC_c*);

    // 函数 mf1 名称和成员函数类型具有
    // C++ 语言链接；参数是“C 函数的指针”

    FUNC_c mf2;

    // 函数 mf2 名称和成员函数类型具有
    // C++ 链接

    static FUNC_c* q;

    // 数据成员 q 名称具有 C++ 链接，且
    // 数据成员类型是“C 函数的指针”

};

extern "C" {

class X {

    void mf1();

    // 函数 mf1 名称和成员函数类型具有
    // C++ 语言链接

    void mf2(void());

    // 函数 mf2 名称具有 C 语言链接
    // 参数是“C 函数的指针”

};

// 示例结束
```

# ISO/IEC 14882:2020(E)

[示例 4:
```cpp
int x;

namespace A {

    extern "C" int f();

    extern "C" int g() { return 1; }

    extern "C" int h();

    extern "C" int x(); // : 与全局空间对象 x 重名

}

namespace B {

extern "C" int f();

    extern "C" int g() { return 1; } // : C 语言链接的函数 g 有两个定义

}

int A::f() { return 98; }
```
```cpp
extern "C" int h() { return 97; } // C 语言链接的函数 f 的定义
A::h 和 h::h 指向同一个函数
```

- 结束示例

包含在链接规范（linkage-specification）中的声明被处理为其包含了 `extern` 标识符 (9.2.2)，目的是确定所声明名称的链接类型以及其是否为定义。此类声明不应指定存储类。

[示例 5:
```cpp
extern "C" double f();
    static double f();
    extern "C" int i; // 错误
    int i; // 定义
    extern "C" static void g(); // 错误
```

- 结束示例

> 注意 5：由于链接是函数类型的一部分，间接引用一个指向 C 函数的指针，则调用值所引用的函数被视为 C 函数。 — 结束注

从 C++ 到其他语言定义的对象的链接，以及从其他语言到 C++ 定义对象的链接是实现定义的且依赖于语言的。当只有两种语言的对象布局策略足以实现此类链接时，可以实现链接。

## 9.2 特性 [dcl.attr]

### 9.2.1 特性语法与语义 [dcl.attr.grammar]

+ 1 属性为各种源代码构造结构（如类型、变量、名称、块或翻译单元）指定额外的信息。

```
attribute-specifier-seq:
    attribute-specifier-seq_opt attribute-specifier
attribute-specifier:
    [ attribute-using-prefix_opt attribute-list ]
alignment-specifier:
alignment:
    alignas ( type-id ..._opt )
    alignas ( constant-expression ..._opt )
attribute-using-prefix:
    using:attribute-namespace :
attribute-list:
    attribute_list_opt
    attribute_list, attribute_opt
    attribute ...
    attribute-list, attribute ...
attribute:
    attribute-token-argument-clause_opt
```

©ISO/IEC 2020 – 版权所有 239

attribute-token:

identifier

attribute-scoped-token

attribute-scoped-token:

attribute-namespace: identifier

attribute-argument-clause:

( balanced-token-seq_opt )

balanced-token-seq:

balanced-token

balanced-token-seq balanced-token

balanced-token:

( balanced-token-seq_opt )

( balanced-token-seq_opt )

( balanced-token-seq_opt), 或大括号

y 任何属性以外的标记

+ 2 如果属性指定符（attribute-specifier）包含属性前缀（attribute-prefix），则该属性前缀后的属性列表（attribute-list）不应包含属性范围标记（attribute-scoped-token），且该属性列表中的每个标记都被处理为其标识符带有 `N::` 前缀；其中 `N` 是属性前缀中指定的属性空间。

> 注意 1：此规则限制了属性前缀如何影响属性参数句（attribute-argument-clause）中的标记。

示例 1:
```cpp
[[CC: opt(1), debug]] // 等同于 [[CC: opt(1), CC:debug]]
void f {}
[[CC: opt(1)] [[CC:debug]]] // 等同于 [[CC: opt(1)] [[CC:debug]]]
[[CC: opt(1)] [[CC:debug]]]
```

+ 3：如果属性指定符（attribute-specifier）包含属性前缀，该属性前缀后的属性列表（attribute-list）不应包含属性范围标记（attribute-scoped-token），且该属性列表中的每个标记都被处理为其标识符带有 `N::` 前缀；其中 `N` 是属性前缀中指定的属性空间。

> 注意 1：此规则限制了属性前缀如何影响属性参数句中的标记。

示例 1:
```cpp
[[CC: opt(1), debug]] // 等同于 [[CC: opt(1), CC:debug]]
void f {}
[[CC: opt(1)] [[CC:debug]]] // 等同于 [[CC: opt(1)] [[CC:debug]]]
[[CC: opt(1)] [[CC:debug]]]
```
