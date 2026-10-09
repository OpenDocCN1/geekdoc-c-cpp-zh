
```
（注：由于原文示例 1 结尾存在重复行，此处按原文保留）

+ 3：如果属性指定符（attribute-specifier）包含属性前缀（attribute-prefix），则该属性前缀后的属性列表（attribute-list）不应包含属性范围标记（attribute-scoped-token），且该属性列表中的每个标记都被处理为其标识符带有 `N::` 前缀；其中 `N` 是属性前缀中指定的属性空间。

（注：我发现你提供的文本中，最后的内容似乎有些乱。我将直接翻译最后一段话）。

Linkage from C++ to objects defined in other languages and objects defined in C++ from other languages is implementation-defined and language-dependent. Where only the object layout strategies of two languages are implementations enough such linkage be achieved.
```

# ISO/IEC 14882:2020

```cpp
alignas(double) unsigned char c[sizeof(double)]; // array of characters, suitably aligned for a double

extern char c[sizeof(double)]; // no alignment necessary

alignas(float)

extern char c[sizeof(double)]; // error: different alignment in declaration

// end example
```

## 9.12.3 Carries dependency 属性 [dcl::attr::depend]

- 1 属性标记 `carries_dependency` 指定了进入和离开函数的依赖传播。它在每个属性列表中最多只能出现一次，且不应存在属性参数句。该属性可以应用于函数声明或 lambda 表达式中参数的声明符标识（declarator-id），如果它指定了参数的初始化具有指向该对象的 (6.9.2) 左值到引用的函数 (7.3.2) 的依赖。该属性也可以应用于函数声明，如果它指定了返回值（如果有）具有指向该函数表达式的依赖。

- 2 如果该函数的任何声明指定了 `carries_dependency` 属性，则该函数的声明会为其声明符标识指定 `carries_dependency` 属性。此外，如果该函数的任何声明指定了某个参数的 `carries_dependency` 属性，则该函数的第一个声明会为该参数指定 `carries_dependency` 属性。如果一个函数或其参数之一在一个翻译单元的声明中使用 `carries_dependency` 属性声明，而在另一个翻译单元中声明相同的函数或参数时未使用 `carries_dependency` 属性，则该程序是格式错误的（ill-formed），不需要诊断。

- 3 注意：`carries_dependency` 属性不会改变程序的含义，但可以导致生成更高效的代码 —— 注意

- 4 示例：
```cpp
/* 单元 A.
```
```cpp
struct foo { int* a; int* b };
std::atomic<struct foo*> foo_head[10];
int foo_array[10];

[[carries_dependency]] struct foo* f(int i) {
  return foo_head[i].load(memory_order::consume);
}
```
```cpp
int g(int* x, int* y) [[carries_dependency]] {
  return kill_dependency(foo_array[*x][*y]);
}
```
```cpp
/* 单元 B.
```
```cpp
[[carries_dependency]] struct foo* f(int i);

int g(int* x, int* y) [[carries_dependency]];
```
```cpp
void h(int i) {
  struct foo* p;
  p = f(i);
  d_something_with(&c, p->a);
  d_something_with(g(p->a, &c));
}
```
函数 `f` 上的 `carries_dependency` 属性意味着返回值带有离开 `f` 的依赖，因此实需要在从 `f` 返回时约束排序。`f` 及其调用者的实现可以在发射硬件内存排序操作（即屏障）时保持标识性。函数 `g` 的第二个参数带有 `carries_dependency` 属性，但其第一个参数没有。因此，函数 `h` 第一次调用 `g` 带有进入 `g` 的依赖，但第二次调用没有。实现可能需要在第二次调用 `g` 之前插入一个屏障。 —— 示例

## 9.12.4 Deprecated 属性

属性标记 `deprecated` 可用于标记仍允许使用但由于某些原因不建议使用的名称和实体。

> 注意 1：特别地，`deprecated` 适用于被认为过时或不安全的名称和实体。注意

它在每个属性列表中最多只能出现一次。可以存在属性参数句，如果存在，则

```
(string-literal)
```

> 注意 2：属性参数句中的字符串字面量（string-literal）可用于解释弃用的理由和/或建议替换的别名。 —— 注意

该属性可以应用于类、类型名称（typed-name）、变量、非静态数据成员、函数、命名空间、枚举成员或模板特化的声明。

未使用 `deprecated` 属性声明的名称或实体稍后可以使用该属性进行声明，反之亦然。

> 注意 3：因此，最初未使用该属性声明的实体可以通过后续重新声明进行标记。然而，如果一个实体已被标记，随后的重新声明不会取消该实体的标记。注意

属性标记 `deprecated` 表示名称或实体可能是过时的。

## 9.12.5 Fallthrough 属性

属性标记 `fallthrough` 可用于指示执行应继续进入下一个 case label。它在每个属性列表中最多只能出现一次，且不应存在属性参数句。该属性可以应用于 switch 语句中的标签（label）。

推荐实践：只有在有意图让执行落到下一个 case label 时，才允许使用 `fallthrough`。

示例 1：
```cpp
void f(int n) {
  switch (n) {
    case 1:
      g(1);
      [[fallthrough]];
    case 2:
      g(2);
      break;
    case 3:
      g(3);
      [[fallthrough]];
    case 4:
      g(4);
      break;
  }
}
```

## 9.12.6 Likelihood 属性

- 1 属性标记 `likely` 和 `unlikely` 可以应用于标签。它们在每个属性列表中最多只能出现一次，且不应存在属性参数句。

- 2 推荐实践：使用 `likely` 属性是为了允许实现在包含该路径的路径比任何替代路径更频繁的情况下进行优化。使用 `unlikely` 属性是为了允许实现在包含该路径的路径比任何替代路径更少的情况下进行优化。

## 9.12.7 Maybe unused 属性

- 1 属性标记 `maybe_used` 表示名称或实体可能未被使用。它在每个属性列表中最多只能出现一次，且不应存在属性参数句。

- 2 该属性可以应用于类、类型定义（typedef-name）、变量（包括绑定声明）、非静态数据成员、函数或枚举成员的声明。

[Example 1:
[[maybe_unused]] void f([[maybe_unused]] bool thing1,
    [[maybe_unused]] bool thing2) {
    [[maybe_unused]] bool b = thing1 && thing2;
    assert(b);
}

实现中不应使用未使用的变量 b，无论是否定义了 NDEBUG。

## 9.12.8 Nodiscard 属性 [dcl.attr.nodiscard]

属性标记 `nodiscard` 可以应用于函数声明中的声明标识符（declar-id），也可以应用于类或枚举的声明。它在每个属性句（attribute-clause）中最多出现一次。可以存在属性参数句（attribute-argument-clause），并且应包含以下内容：

```
string-literal
```

使用 `nodiscard` 属性声明的名称或实体可以使用该属性重新声明，反之亦然。

> [Note 1：因此，任何未使用该属性声明的实体可以通过随后的重新声明标记为 nodiscard。然而，在实体被标记为 nodiscard 之后，随后的重新声明不会移除该实体的 nodiscard 属性。—note]

允许使用不同形式的属性（带有或不带属性参数句，或带有不同的属性参数句）进行重新声明。

`nodiscard` 类型是在可达声明中的（可能带有 cv 修饰的）`nodiscard` 类类型或枚举类型。`nodiscard` 调用是指：

-   函数调用（7.6.1.3），其调用了可达声明中的 `nodiscard` 函数，
    或者其返回类型为 `nodiscard` 类型，或

-   显式转换（7.6.4.1, 7.6.4.9, 7.6.3），其通过可达声明中定义的 `nodiscard` 构建对象，或初始化一个 `nodiscard` 类型的对象。

推荐做法：不鼓励将 `nodiscard` 调用作为潜在评估的丢弃值表达式（7.2）出现，除非显式强制转换为值。在以下情况下，实现中应发出警告：

> [Note 2：这通常是因为返回 nodiscard 用的值会产生意想不到的后果。—end]

nodiscard 属性参数句中的字符串字面量应用于警告信息中，说明为什么不应丢弃结果。

[Example 1:
struct [[nodiscard]] my_scopeguard { /* ... */ };
struct my_unique = default {
    [[nodiscard]] my_unique(int fd) { /* ... */ } // 不获取资源
    ~my_unique() noexcept { /* ... */ } // 获取资源
    /* ... */ }; // 释放资源，如果有
};
struct [[nodiscard]] error_info { /* ... */ };
error_info enable_missile_safety_mode();
void launch_missiles() {
    void test_missiles() {
        my_scopeguard(); // 不鼓励警告
        (void)my_scopeguard(); // 不鼓励警告，强制转换为 void
        launch_missile(); // 逗号运算符，语句继续
        my_unique(42); // 不鼓励警告
        my_unique(); // 不鼓励警告
    }
    enable_missile_safety_mode(); // 不鼓励警告
    launch_missiles();
}
error_info &foo();
void f( ) { foo(); }; // 不鼓励警告：不是 nodiscard 调用，因为
// （引用）返回类型或函数均未声明为 nodiscard

## 9.12.9 Norturn 属性

属性标记 `norturn` 指定函数不返回。它应在每个属性列表（attribute-list）中最多出现一次，且不存在属性参数句。该属性可以应用于函数声明中的声明标识符。如果该函数的任何声明指定了 `norturn` 属性，则该函数的首次声明也应指定 `norturn` 属性。如果函数在一个翻译单元中被声明为 `norturn` 属性，而在另一个翻译单元中声明为不带 `norturn` 属性，则程序是格式错误的（ill-formed），不需要诊断。

如果调用的函数 f 在之前曾被声明为带有 `norturn` 属性，且 f 最终返回了，则其行为是未定义的。

> Note 1：函数可以通过抛出异常来终止。 — end note

推荐做法：如果标记为 `[[norturn]]` 的函数可以返回，实现应发出警告。

Example 1:
```c
void f() {
    throw "error";
}
void q(int i) {
    // 如果传入的参数 <= 0，行为是未定义的
    if (i > 0)
        throw "positive";
}
``` — end example

## 9.12.10 No unique address 属性

属性标记 `no_unique_address` 指定非静态数据成员是一个潜在重叠的子对象（6.2）。它应在每个属性列表中最多出现一次，且不应存在属性参数句。该属性可以适用于位字段外的非静态数据成员。

非静态数据成员可以共享另一个非静态数据成员或基类的地址，且在对象末尾可能插入任何填充都可以重用作其他成员的存储。

Example 1:
```cpp
template<typename Key, typename Value,
         typename Hash, typename Pred, typename Allocator = std::allocator<void>>
class hash_map {
```

## 10. 模块 (Modules)

### 10.1 模块单元与范围

module-declaration:

module-name:

module-qualifier:

module-partition:

module-qualifier:

1 模块要么是命名模块，要么是全局模块。声明按如下方式附加到模块：

-   如果声明

-   (7.1) 是可替换定义的全局分配或释放函数（17.6.2, 17.6.3），或

-   (7.2) 是具有外部链接的命名空间定义，或

-   (7.3) 出现在链接规范中，

它附加到全局模块。

8 不包含 `export` 关键字且不包含模块分区的模块声明隐式地暗示该模块的主接口单元，如同通过模块导入声明一样。

Example 2:

```
Translation unit #1
module B:Y;
int y(); // 不隐式导入 B
```

Translation unit #2:

```
export module B;
import Y;
int n = y(); // OK，不创建接口依赖
```

Translation unit #3:

```
module B:X1;
int &a = n; // 不隐式导入 B
// 错误：n 不可见
```

Translation unit #4:

```
module B:X2;
import B;
int &b = n; // 不隐式导入 B
```

Translation unit #5:

```
module B;
int &c = n; // 隐式暗示 B
// OK
```

## 10.2 导出声明 (Export declaration) [module.interface]

export-declaration:

export declaration

export { declaration-seq }

export-keyword module-declaration

1 导出声明应仅出现在命名空间范围，且仅出现在模块接口单元的范围内。导出声明不应直接或间接地出现在匿名命名空间内或私有模块片段中。导出声明具有其声明、声明序列（如果有）或模块导入声明的声明效果。导出声明不建立作用，其声明或声明序列不应包含导出声明或模块声明。

2 声明是导出的，如果它是：

-   (2.1) 导出声明内部的命名空间声明，或

# ISO/IEC 14882:2020(E)

(2.2) — 一个包含导出声明的命名空间定义，或

(2.3) — 头文件 (10.3) 内的引入至少一个名称的声明。

3 一个不是模块导入声明的导出声明应当声明至少一个名称。如果该声明不在头文件单元内，则它不应声明具有内部链接性（internal linkage）的名称。

4 [示例 1: "a.h":]

源文件 "a.h":

```
export int x;
```

翻译单元 #1:

module;

#include "a.h" // x 的声明不在其中

export module M // 模块接口单元的作用范围

export namespace { // 错误：未引入任何名称

int a1; // 错误：导出具有内部链接的名称

namespace {

export int a2; // 错误：导出具有内部链接的名称

export static int b; // 错误：b 显式为 static

export int f0(); // OK

export namespace N { // OK

export using namespace N; // 错误：未声明名称

}

end example;

5 如果该声明是一个使用声明 (9.9) 且不在头文件单元内，则所有使用声明符最终引用的实体（如果有的话）应当已以具有外部链接性（external linkage）的名称被引入。

[示例 2: "b.h":]

源文件 "b.h":

```
int f0();
```

可导入头文件 "c.h":

```
int g0();
```

翻译单元 #1:
