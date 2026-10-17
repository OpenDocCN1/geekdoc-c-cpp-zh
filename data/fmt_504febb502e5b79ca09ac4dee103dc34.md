
+ 在线程间交互方面的要求不适用于只有一个线程执行的程序。

# 20.5.1 库的内容和组织 [organization]

+ `20.5.1.1` 描述 C++ 标准库中的实体和宏。`20.5.1.2` 列出了标准库头文件。`20.5.1.3` 规定了对 C++ 标准库的独立实现的要求。

## 20.5.1.1 库的内容 [contents]

C++ 标准库为标准库头文件 (`20.5.1.2`) 中描述的实体和宏提供了定义。

所有库实体 `operator new` 和 `operator delete` 都在 `std` 命名空间内定义。¹⁶⁶ 只要在标准库中定义的名称 `x` 被视为完全限定为 `std::x`，除非另有规定。全局命名空间中的定义。例如：如果库函数 `F` 被描述为调用库函数 `G`，则指的是 `std::G`。

¹⁶⁶ C++ 标准库头文件 (附录 D.5) 也在全局命名空间内定义。¹⁶⁷ 这使得实现者可以使用内联命名空间来支持多种配置。

§ ISO/IEC 2017 – 所有权利保留 454

# ISO/IEC 14882:2017(E)

## 20.5.1.2 头文件 [headers]

+ `1` C++ 标准库的每个元素都在头文件中（根据情况）声明或定义。¹⁶⁸
+ `2` 标准库提供了表 16 所示的 C++ 头文件。

表 16 — C++ 头文件

| `<algorithm>` | `<future>` | `<sstream>` |
| --- | --- | --- |
| `<any>` | `<initializer_list>` | `<optional>` |
| `<array>` | `<complex>` | `<system_error>` |
| `<atomic>` | `<iostream>` | `<thread>` |
| `<bitset>` | `<queue>` | `<type_traits>` |
| `<complexcvt>` | `<random>` | `<typeindex>` |
| `<condition>` | `<regex>` | `<typeinfo>` |
| `<condition_variable>` | `<allocator>` | `<unordered_map>` |
| `<deque>` | `<set>` | `<unordered_set>` |
| `<exception>` | `<list>` | `<shared_mutex>` |
| `<execution>` | `<local>` | `<utility>` |
| `<filesystem>` | `<map>` | `<valarray>` |
| `<forward_list>` | `<memory>` | `<variant>` |
| `<fstream>` | `<memory_resource>` | `<vector>` |
| `<functional>` | `<streambuf>` | |
| | `<string>` | |
| | `<mutex>` | `<string_view>` |

+ `3` 标准库的功能在表 17 所示的额外头文件中。¹⁶⁹

表 17 — 用于 C 功能的 C++ 头文件

| `<cassert>` | `<cstdio>` | `<cuchar>` |
| --- | --- | --- |
| `<complex>` | `<iso6449>` | `<stdexcept>` |
| `<cctype>` | `<limits>` | `<stdarg>` |
| `<string>` |
| `<cerrno>` | `<locale>` | `<cddb>` | `<cmath>` |
| `<cfloat>` | `<math>` | `<stddef>` | `<time>` |
| | `<setjmp>` | `<cint>` | `<cuchar>` |

=¹¹⁷⁰

+ `4` 除第 20 至 33 节和附录 D 注出的外，每个头文件的内容与 C 标准库（第 2 节）中相应名称的内容相同。在 C++ 标准库中，声明（除定义为宏外）位于标准命名空间的作用域 (`6.3.8`) 内。未规定这些名称（包括第 21 至 33 节和附录 D 中声明的任何重叠）是否先在全局命名空间声明，然后注入标准命名空间。

+ `5` 在 C 中定义为宏的名称如果 C 许可证允许此类实现，则在 C++ 标准库中定义。[备注：C 中定义为宏的名称包括：`assert`, `offset`, `stdarg`, `va_arg`, `end` 和 `var`。—— 结束节点]

+ `6` 在 C 中定义的头文件名称在 C++ 标准库中定义。¹⁷⁰)

> \170} 头文件不是源文件，头文件中通过 `<` 和 `>` 定义的序列也不是有效的源文件名 (`19.2`)。^{169} 故意 `<statomic.h>`, `<stdretturn.h>`, `<threads.h>` 中的任何一个头文件都没有 C++ 头文件^{170} 这禁用了了 C 中在函数原型之外提供掩码宏的做法。在 C++ 中实现等效内联行为的唯一方法是提供内联函数的定义。

# ISO/IEC 14882:2017(E)

在 C++ 中作为关键字或运算符的标识符不应在 C++ 标准库头文件中被定义为宏。171

D.5 “标准库头文件”描述了在 C++ 程序中使用 `name.h` (C 头文件) 形式的效果。172

该标准的附录 K 描述了大量的函数以及关联的类型和宏，这些函数、类型和宏比许多传统的 C 头文件更有效地“促进更安全、更可靠的编程”。函数的名称带有后缀 `_s`：它们大多数提供了与带有无符号名称相同的 C 库函数相同的行为，前提是它们多了一个作为结果大小的额外参数。如果包含了任何 C++ 头文件，则这些名称中是否有在全局命名空间中声明是由实现定义的。（其中一个声明在 `std` 命名空间中）。

表 18 列出了在某些头文件中可能定义的 Annex K 名称。这些名称也受 `20.5.4.3.2` 条的限制。

# 表 18 — 标准 Annex K 名称

| `abort_handler_s` | `strncat_s` | `vsscanf_s` |
| `astime_s` | `memccpy_s` | `vsprintf_s` |
| `bsearch_s` | `memmove_s` | `strtok_s` | `vwscanf_s` |
| `constraint_handler_s` | `memset_s` | `swprintf_s` | `wctomb_s` |
| `ctime_s` | `printf_s` | `wscanf_s` | `wcscat_s` |
| `errno_s` | `SIZE_MAX` | `tmpfile_s` | `wcscpy_s` |
| `fopen_s` | `rsize_t` | `TMP_MAX` | `wcsnc_s` |
| `fprint_s` | `scanf_s` | `vsprintf_s` | `wcscanf_s` |
| `freopen_s` | `set_constraint_handler_s` | `vscanf_s` | `wctorbs_s` |
| `scancf_s` | | `vsprintf_s` | `wctstok_s` |
| `vsprintf_s` | `snprintf_s` | `vprintf_f` | `wctstbs_s` |
| `vsscanf_s` | | `vprintf_f` | `wctombs_s` |
| `getenv_s` | `scancf_s` | `vsscanf_s` | `wmemmove_s` |
| `gmtime_s` | `strcat_s` | `vsprintf_s` | `wprintf_s` |
| `ignore_handler_s` | `strcpy_s` | `vsscanf_s` | |
| `L_tmpnam_s` | `strerror_s` | `vsnprintf_s` | |
| `locale_s` | `strrlen_s` | `vsscanf_s` | |
| `shartowcs_s` | `strlen_s` | `vsprintf_s` | |

### 20.5.1.3 实现环境 [compliance]

定义了两种实现：托管的 (`hosted`) 和无托管的 (`freestanding`) (`4.1`)。对于托管实现，文档描述了可用头文件的集合。

无托管实现具有由实现定义的头文件集合。该集合应至少包含表 19 所示的头文件。

提供的 `<stddef>` 头文件至少声明函数 `abort`、`atxit`、`quick_exit_` 和 `quick_exit` (`21.5`)。表中的其他头文件应满足与托管实现相同的要求。

171 特别是，使用标准头 `<iso64.h>` 或 `<iso66>` 没有效果。
172 “b” 类头文件将所有名称导出到全局命名空间，而较新的形式将名称保留在 `std` 命名空间中。因此，对于所有旨在严格遵守 C 的 C++ 程序外，较新的形式是首选形式。

20.5.1.3 ©ISO/IEC 2017 – 版权所有 456

# ISO/IEC 14882:2017(E)

# 表 19 — 无托管实现所需的 C++ 头文件

| 子类 | 头文件(s) |
| --- | --- |
| 21.2 | 类型 | `<ciso64>` |
| 21.3 | 实现属性 | `<float>` `<limits>` `<climits>` |
| 21.4 | 整数类型 | `<cint>` |
| 21.5 | 开始与终止 | `<cstdlib>` |
| 21.6 | 动态内存管理 | `<new>` |
| 21.7 | 类型识别 | `<typeinfo>` |
| 21.8 | 异常处理 | `<exception>` |
| 21.9 | 初始化列表 | `<initializer_list>` |
| 21.10 | 其他运行时支持 | `<carg>` |
| 23.15 | 类型特质 | `<type_traits>` |
| 32 | 原子操作 | `<atomic>` |
| D.4.2, D.4.3 | 弃用的头文件 | `<stdalign>` `<cdbool>` |

## 20.5.2 使用库 [using.overview]

### 20.5.2.1 概述

1 这描述了 C++ 程序如何获取 C++ 标准库设施的权限。`20.5.2.2` 描述了第 4 阶段的效果，`20.5.2.3` 描述了第 8 阶段的效果 (`5`)。

### 20.5.2.2 头文件 [using.headers]

1 C++ 标准库中的实体定义在头文件中，当翻译单元包含 `include` 指令时，其内容是可用的 (`2`)。
2 翻译单元可以任何顺序包含库头文件（第 5 节）。可以包含多次，不会产生影响，但 `<cassert>` 或 `assert` 的效果每次取决于 `NDEBUG`。
3 翻译单元应在任何声明或定义之后包含头文件，并且应在词法上在该翻译单元中对任何实体的第一次引用之前包含它。不需要诊断信息。

### 20.5.2.3 链接 [using.linkage]

1 C 标准库中的实体具有外部链接 (`6.5`)。除非另有说明，否则对象和函数具有默认的 `"C"` 链接 (`10.5`)。
2 带有外部链接声明的标准库实体具有 `"C"` 还是 `"C++"` 链接是由实现定义的。建议使用 `"C"` 链接（修正: 带有外部链接声明的标准库实体具有 `"C"` 还是 `"C++"` 链接是由实现定义的。建议使用 `"C"` 链接）。
*注：原文此处似乎存在重复或逻辑混乱，根据上下文翻译。*

# ISO/IEC 14882:2017(E)

3 `swap(t, u)` 和 `swap(u, t)` 中的上下文被评估以确保通过重载解析 (`16.3`) 在一个候选集上选择一个名为 `"swap"` 的二进制非成员函数，该候选集包括：

(3.1) 在 `<utility>` (`23.2`) 中定义的两个 `swap` 模板，以及

(3.2) 由参数定义查找 (`argument-defined lookup`, `6.4.2`) 产生的查找集。

> [注意：如果 T 和 U 都是基本类型或基本类型的数组，且来自 `<utility>` 头文件的它们相相等，则上述描述的查找集等同于表达式 `std::swap(t, u)` 或 `std::swap(u, t)` 的限定名查找（视情况而定）。]

> [注意：未指定具有可交换性（swappable requirement）的库组件是否包含了 `<utility>` 头文件以确保适当的评估上下文。]

一个值如果是可交换的，如果它与类型为 `T*` 的任意值都是可交换的，则对应的它是可交换的。

迭代器 (`27.2`) 的任意一个如果对于任何类型为 `X` 的可解引用对象，`*` 是可交换的，则满足 `ValuesSwappable` 的要求。

> [示例：用户代码可以在以下条件下确保 swap 调用的评估在适当的上下执行：
`#include <utility>`

```
// 要求：std::forward<T>(t) 应当与 std::forward<U>(u) 是可交换的。
template <class T, class U>
void swap(T&& t, U&& u) {
  using std::swap(std::forward<T>(t), std::forward<U>(u)); // OK：在满足条件下使用了 "swappable"
} // 适用于右值和左值
```

```
// 要求：T 的值应该是可交换的。
template <class T>
void lv_swap(T& t1, T& t2) {
  using std::swap; // OK：针对...使用了可交换条件
  swap(t1, t2);
}
```

```cpp
namespace N {
  struct A { int m; };
  struct Proxy { A* a; };
  Proxy(A& a) : a(&a) {}
  void swap(A x, Proxy p) { // OK：使用了等于可交换的上下文
    // 基本类型的条件
  }
  void swap(Proxy p, A& x) { swap(x, p); } // 满足对称性约束
}
```

```cpp
int main() {
  int i = 1, j = 2;
  lv_swap(i, j);
  assert(i == 2 && j == 1);
  N::A a1 = { 5 }, a2 = { -5 };
  value_swap(a1, proxy(a2));
}
```

```cpp
assert(a1.m == -5 && a2.m == 5);
// 示例结束|
```
