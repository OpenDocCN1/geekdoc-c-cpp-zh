
**转换难度：** 语义转换。如果拷贝需要 `volatile` 变量，则必须提供用户定义的构造函数或赋值。如果需要非 `volatile` 语义，可以使用显式的 `const` 转换。

**使用范围：**罕见。

3 **受影响的子句：** 11.4.10

更改：`int` 类型的位域是有符号的。

**原理：** 将符号位的选择交给实现会导致模板特化定义不一致。为了保持一致性，非依赖类型也消除了实现自由度。

对原始功能的影响：在 C 中该选择是由实现决定的，但在 C++ 中不是。

转换难度：语法转换。

使用范围：罕见。

4 **受影响的子句：** 11.4.11

更改：在 C++ 中，嵌套类的名称局部于其所属的类。在 C 语言中，嵌套类的名称与最外层所属类的名称属于同一作用域。

示例：

```c
struct X {
    struct Y { /* ... */ y };
    struct Y yy; // C 有效，C++ 无效
};
```

原理：C++ 类具有成员函数，其作用域机制将防止 C++ 程序员在类内部维护局部性。为 C++ 针对该规则制定一套一致的规则将非常复杂，C++ 程序员将无法可靠地预测许多涉及嵌套或局部函数的非平凡示例。

对原始功能的影响：更改了定义良好的功能的语义。

**转换难度：** 语义转换。要使结构体类型名称在所属结构体的作用域中可见，可以在结构体定义之前，在所属结构体的作用域中声明结构体标签。

```c
struct Y;
struct X {
    struct Y { /* ... */ y }; // struct Y 和 struct X 处于同一作用域
};
```

在其他结构体定义中引入的所属结构体外的结构体类型定义都可以导出到所属结构体的作用域。注意：这是作用域规则差异的结果，该差异在 6.4 中有所记载。

使用范围：罕见。

5 **受影响的子句：** 11.4.12

更改：在 C++ 中，`typedef` 名称在类定义中使用后，不可在类定义中重新声明。

示例：

```c
typedef int I;
struct S {
    I;
    tI; // C 有效，C++ 无效
};
```

原理：当 C 类变得复杂时，这种在类型使用后进行重新定义会让 C 程序员对 `I` 的真实含义产生困惑。

对原始功能的影响：删除了定义良好的功能。

转换难度：语义转换。

使用范围：罕见。

子句 21.5.3 描述了这些更改。

2 头文件 `<cw>` (21.5.4)：以下函数具有不同的声明：

- (2.1) — `wcschch`

- (2.2) — `wcspbrk`

- (2.3) — `wcschr`

- (2.4) — `wcsstr`

- (2.5) — `wemscr`

子句 21.5.4 描述了这些更改。

3 头文件 `<stddef>` (17.2.1) 除了 C 标准库中 `<stddef.h>` (D.10) 声明的名字外，还声明了名称 `null_ptr`。

## C.6.5 行为修改 [diff.mods.to.behavior]

### C.6.5.1 通用 [diff.mods.to.behavior.general]

1 头文件 `<cstdlib>` (17.2.2)：以下函数具有不同的行为：

- (1.1) — `atexit`

- (1.2) — `exit`

- (1.3) — `abort`

子句 17.13.3 描述了这些更改。

2 头文件 `<setjmp>` (17.13.3)：以下函数具有不同的行为：

- (2.1) — `longjmp`

子句 17.13.3 描述了这些更改。

## C.6.5.2 宏 offset(type, member-designator) [diff.offsetof]

1 定义在 `<stddef>` (17.2.1) 中的宏 `offset` 在 C++ 中接受一组受限的类型参数。子句 17.2.4 描述了该更改。

## C.6.5.3 内存分配函数 [diff.malloc]

函数 `aligned_alloc`、`calloc`、`malloc` 和 `realloc` 在 C++ 中受到限制。子句 20.10.12 描述了这些更改。

## 附录 D（规范性）

兼容性特性

### D.1 通用

本附录包含了 C++ 标准中为了与现有实现兼容而指定的特性。

这些是已弃用的（deprecated）特性，其中已弃用的定义为：对于当前 C++ 修订是规范的，但已被确定为从未来修订中移除的候选者。实现可以使用已弃用属性（9.12.4）声明在本节中描述的库名称和实体。

### D.2 枚举类型上的算术比较

在其中一个为枚举类型而另一个为不同枚举类型或浮点类型的操作数上使用通常的算术比较（7.4）的能力是已弃用的。

> 注意 1：此类操作数之间的三路比较（7.68）是格式不正确的（ill-formed）。

示例 1:

```
enum E1 { };
enum E2 { };
bool b = e <= 3.7; // 已弃用
int k = f - e; // 已弃用
auto cmp = e <> f; // 错误
```

### D.3 *this* 的隐式引用

为了与 C++ 之前的版本兼容，带有默认捕获 (7.5.5.3) 的 lambda 表达式会隐式通过引用捕捉 *this*。

```
示例 1:
struct X {
int x;
void foo(int n) {
auto f = [*]{ x = n; }; // 已弃用：x 表示 this->x，而不是其拷贝
auto g = [this]{ x = n; }; // 推荐的替换
}
```

### D.4 下标表达式中的公共运算符

作为下标表达式（7.6.1.2）的 `expr-or-braced-init-list`（或初始化列表）出现的逗号表达式（7.6.20）是已弃用的。

> 注意 1：带括号的逗号表达式不是已弃用的。

示例 1:

```
void foo(int *s, int b, int c) {
{a,b,c}; // 已弃用
a(a,b,c); // OK
}
```

### D.5 数组比较

两个数组类型操作数之间的相等和关系比较（7.6.10, 7.6.9）是已弃用的。

> 注意 1：此类操作数之间的三路比较（7.6.8）是格式不正确的。

示例 1:

```
int arr1[5];
int arr2[5];
bool same = arr1 == arr2; // 已弃用，同 arr1[0]
auto cmp = arr1 <> arr2; // 不比较内容
    // 错误
```

### D.6 已弃用的 volatile 类型

`volatile` 修饰的后缀 `++` 和 `--`（7.6.6）以及前缀 `++` 和 `--`（7.6.3）是已弃用的。

示例 1:

```
volatile int volatileclator;
++volatileclator; // 已弃用
```

- 2 左操作数为 `volatile` 修饰类型的赋值是已弃用的。

示例 2:

```
int neck, tail;
volatile int brachioscular;
brachioscular = neck; // OK
tail = brachioscular; // OK
brachioscular = tail; // 已弃用
brachioscular += neck; // 已弃用
```

- 3 带有 `volatile` 修饰参数或返回类型的函数类型（9.3.4）是已弃用的。

示例 3:

```
volatile struct jurassic(); // 已弃用
void(volatile struct left_arm, volatile struct right_arm); // 已弃用
void(volatile struct right_arm); // OK
```

- 4 `volatile` 修饰类型的结构化绑定（9.6）是已弃用的。

示例 4:

```
struct lenkys { short };
void(lenkys);
volatile auto what_is_this = alvarez; // 已弃用
```

### D.7 static constexpr 的重声明

- 1 为了与 C++ 之前的版本兼容，`constexpr` 成员可以在类外带有初始化重声明。

示例 1:

```
struct A {
    static constexpr int n = 5; // C++14 定义
};
constexpr int A::n; // 重复声明 (C++14)
```

### D.8 实体的非局部使用

非局部声明（6.6）是已弃用的。

> 注意 1：可导入模块中的此类声明是格式不正确的。

示例 1:

```
namespace {
  struct A {
    void f() {}
  };
  A h(); // 已弃用：非内部链接
  inline void g(A f){} // 已弃用：非内部链接
```

### D.9 拷贝函数的隐式声明

如果类有拷贝赋值运算符或用户定义的析构函数，拷贝构造函数（11.4.5.3）的隐式定义是已弃用的。如果类有用户定义的构造函数，拷贝赋值运算符（11.4.6）的隐式定义是已弃用的。

## D.10 C 头文件

### D.10.1 通用

为了与 C 库兼容，C++ 标准库提供了表 147 中的 C 头文件。

表 147：C 头文件

| | | |

| :--- | :--- | :--- |

| `<assert.h>` | `<inttypes.h>` | `<stdio.h>` |

| `<complex.h>` | `<iso646.h>` | `<signal.h>` |

| `<stdlib.h>` | `<stdalign.h>` | `<wchar.h>` |

| `<ctype.h>` | `<limits.h>` | `<string.h>` |

| `<errno.h>` | `<locale.h>` | `<stdbool.h>` |

| `<fenv.h>` | `<math.h>` | `<stddef.h>` |

| `<float.h>` | `<setjmp.h>` | `<time.h>` |

| | `<stdint.h>` | `<uchar.h>` |

### D.10.2 头文件 `<complex.h>` 摘要

```
#include <complex>
```

C++ `<complex.h>` 的行为类似于包含了头文件 `<complex>` (26.4.2)。

> 注意 1：`<complex>` 在命名空间中引入的名字被 `<complex.h>` 放在全局范围内。

### D.10.3 头文件 `<iso646.h>` 摘要

C++ 头文件 `<iso646.h>` 是空的。

> 注意 1：`and`, `and_eq`, `bit`, `bitor`, `compl`, `not_eq`, `not`, `or_`, `xor`, `and x_eq` 是 C++ 中的关键字（5.11）。

### D.10.4 头文件 `<stdalign.h>` 摘要

```
#define _alignas_is_defined 1
```

C++ 头文件 `<stdalign.h>` 的内容与 C 标准库头文件 `<stdalign.h>` 相同，更改如下：头文件 `<stdalign.h>` 没有定义宏 `alignas`。

另见：ISO C 7.15

### D.10.5 头文件 `<stdlib.h>` 摘要 

```
#define __bool_true_false_are_defined 1
```

C++ 头文件 `<stdlib.h>` 的内容与 C 标准库头文件 `<stdlib.h>` 相同，更改如下：头文件 `<stdlib.h>` 没有定义宏 `name`、`true` 或 `false`。

另见：ISO C 7.18

### D.10.6 头文件 `<tgmath.h>` 摘要 

```
#include <cmath>
#include <complex>
```

`<tgmath.h>` 的行为类似于包含了头文件 `<cmath>` (26.8.1) 和 `<complex>` (26.4.2)。

- `<cmath>` 和 `<complex>` 提供的重载是“充分的”。

- 由 `<cmath>` 在命名空间中引入的名字被 `<tgmath.h>` 放在全局范围内。

### D.10.7 其他头文件

- 除了 `<complex.h>` (D.10.2)、`<iso646.h>` (D.10.3)、`<stdalign.h>` (D.10.4)、`<stdlib.h>` (D.10.5) 和 `<tgmath.h>` (D.10.6) 之外，每个头文件都有一个 `<name.h>`，其行为类似于标准库，除了 26.8.6 中描述的函数和在全局命名空间定义的函数外。

- 示例 1：头文件 `<cstdlib>` 在命名空间 `std` 中提供了声明。也可以在全局范围内提供这些名称。头文件 `<stdlib.h>` 在全局命名空间提供了声明，如 C 所示。

### D.11 Requires 段落

除了 16.3.2.4 中的元素外，函数语义描述可能还包含一个 `Requires` 元素来表示调用函数的的前提条件。

违反函数 `Requires` 中指定的任何前提条件会导致未定义行为，除非函数抛出异常。元素指定在违反条件时抛出异常。

### D.12 关系运算符

头文件 `<utility>` (20.2.1) 有以下新增：

```
namespace std { {
template<class T> bool operator==(const T x, const T y);
template<class T> bool operator>(const T x, const T y);
template<class T> bool operator<(const T x, const T y);
template<class T> bool operator>=(const T x, const T y);
}
```

为了避免重复定义 `operator!=` 或 `operator==` 以及 `>`, `<=` 和 `>=`, 库提供了以下：

```
template<class T> bool operator=(const T x, const T y);
```

- 需要：类型 T 为 Cpp17EqualityComparable（表 25）

- 返回：`(!x == y)`.

```
template<class T> bool operator<(const T x, const T y);
```

- 需要：类型 T 为 Cpp17LessThanThanComparable（表 26）

- 返回：`y < x`.

```cpp
template<class T> bool operator<==(const T& x, const T& y);
```

要求：类型 T 为 Cpp17LessThanComparable（表 26）。

返回：(x < y)。

```cpp
template<class T> bool operator<==(const T& x, const T& y);
```

要求：类型 T 为 Cpp17LessThanComparable（表 26）。

返回：(x < y)。

## D.13 char streams

### D.13.1 Header<iostream> 概述

头文件 `<iostream>` 定义了将流与字符数组对象关联并辅助读读写对象的类型。

```cpp
namespace std {
    class strstreambuf;
    class istream;
    class ostream;
    class stringstream;
};
```

## D.13.2 Class strstreambuf

### D.13.2.1 General
