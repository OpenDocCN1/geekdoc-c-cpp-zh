
The output is something like:

```
06/28/12, 15:38 (03:38PM)
```

The `strftime()` formatting characters almost constitute a small programming language:

*Section 43.6 Date and Time 1263*

## Date and Time Formatting

- `%a` — Abbreviated weekday name
- `%A` — Full weekday name
- `%b` — Abbreviated month name
- `%B` — Full month name
- `%c` — Date and time representation
- `%C` — The year divided by 100 and truncated to a decimal integer [00:99]
- `%d` — The day of the month as a decimal number [01:31]
- `%D` — Equivalent to `%m/%d/%y`
- `%e` — The day of the month as a decimal number [1:31]; a single digit is preceded by a space
- `%F` — Equivalent to `%Y-%m-%d`; the ISO 8601 date format
- `%g` — The last two digits of the week-based year as a decimal number [00:99]
- `%G` — The week-based year as a decimal number (e.g., 2012)
- `%h` — Equivalent to `%b`
- `%H` — The hour (24-hour clock) as a decimal number [00:23]
- `%I` — The hour (12-hour clock) as a decimal number [01:12]
- `%j` — The day of the year as a decimal number [001:366]
- `%m` — The month as a decimal number [01:12]
- `%M` — The minute as a decimal number [00:59]
- `%n` — A newline character
- `%p` — The locale’s equivalent of AM/PM for a 12-hour clock
- `%r` — 12-hour clock time
- `%R` — Equivalent to `%H:%M`
- `%S` — The second as a decimal number [00:60]
- `%t` — A horizontal-tab character
- `%T` — Equivalent to `%H:%M:%S`; the ISO 8601 time format
- `%u` — The ISO 8601 weekday as a decimal number [1:7]; Monday is 1
- `%U` — The week number of the year (the first Sunday is the first day of week 1) as a decimal number [00:53]
- `%V` — The ISO 8601 week number as a decimal number [01:53]
- `%w` — The weekday as a decimal number [0:6]; Sunday is 0
- `%W` — The week number of the year (the first Monday is the first day of week 1) as a decimal number [00:53]
- `%x` — The locale’s appropriate date representation
- `%X` — The locale’s appropriate time representation
- `%y` — The last 2 digits of the year as a decimal number [00:99]
- `%Y` — The year as a decimal number (e.g., 2012)
- `%z` — The offset from UTC in the ISO 8601 format `-0430` (4.5 hours behind UTC, Greenwich); no characters if no time zone is determinable
- `%Z` — The locale’s time zone name or abbreviation; nothing if no time zone is known
- `%%` — The character `%`

The locale referred to is the program’s global locale.

Some conversion specifiers can be modified by an `E` or `O` modifier, indicating alternative implementation-specific and locale-specific formatting. For example:

**Date and Time Format Modifier Examples**

- `%Ec` — The locale’s alternative date and time representation
- `%EC` — The name of the base year (period) in the locale’s alternative representation
- `%OH` — The hour (24-hour clock), using the locale’s alternative numeric symbols
- `%Oy` — The last 年份的两位数字，使用区域设置的替代数字符号。

`strftime()` 由 `put_time` 面（§39.4.4.1）使用。关于 C++ 风格的时间设施，参见 §35.2。

## 43.7 其他

在 `<cstdlib>` 中，我们可以找到：

**其他 `<stdlib.h>` 函数**

| 函数 | 含义 |
|---|---|
| `abort()` | “异常”终止程序。 |
| `exit(n)` | 以值 `n` 终止程序；`n==0` 表示成功终止。 |
| `system(s)` | 将字符串作为命令执行（依赖于系统）。 |
| `qsort(b,n,s,cmp)` | 使用比较函数 `cmp` 对从 `b` 开始、包含 `n` 个大小为 `s` 的元素的数组进行排序。 |
| `bsearch(k,b,n,s,cmp)` | 使用比较函数 `cmp` 在从 `b` 开始、包含 `n` 个大小为 `s` 的元素的已排序数组中搜索 `k`。 |
| `d=rand()` | `d` 是范围 `[0,RAND_MAX]` 内的伪随机数。 |
| `srand(d)` | 使用 `d` 作为种子开始一个伪随机数序列。 |

`qsort()` 和 `bsearch()` 使用的比较函数（`cmp`）必须是以下类型：

```
int (*cmp)(const void* p, const void* q);
```

也就是说，排序函数不知道任何类型信息，它们只是将数组参数“视为”字节序列。返回的整数是：

- 如果 `*p` 被认为小于 `*q`，则为负数
- 如果 `*p` 被认为等于 `*q`，则为零
- 如果 `*p` 被认为大于 `*q`，则为正数

这与使用传统 `<` 的 `sort()` 不同。请注意，`exit()` 和 `abort()` 不会调用析构函数。如果你希望为已构造的对象调用析构函数，请抛出异常（§13.5.1）。类似地，`<csetjmp>` 中的 `longjmp()` 是一种非局部 `goto`，它会展开堆栈，直到找到匹配的 `setjmp()` 的结果。它不会调用析构函数。如果 `throw` 从程序的同一点抛出时本应调用析构函数，则其行为是未定义的。永远不要在 C++ 程序中使用 `setjmp()`。

有关更多 C 标准库函数，请参阅 [Kernighan,1988] 或其他权威的 C 语言参考书。

## 不是 C

## 建议

# 兼容性

> 你遵循你的习俗，我遵循我的。
> —— C. 纳皮尔

## 44.1 引言

本章讨论标准 C++（由 ISO/IEC 14882-2011 定义）与早期版本（如 ISO/IEC 14882-1998）、标准 C（由 ISO/IEC 9899-2011 定义）与早期版本（如经典 C）之间的差异。其目的是：

- 简要列出 C++11 中的新内容
- 记录可能导致程序员遇到问题的差异
- 指出处理这些问题的方法

大多数兼容性问题出现在人们尝试将 C 程序升级为 C++ 程序、尝试将 C++ 程序从旧版本 C++ 移植到较新版本（例如，C++98 到 C++11），或尝试使用旧编译器编译采用现代特性的 C++ 时。这里的目标不是枚举每一个可能的兼容性问题，而是列出最常出现的问题并提出它们的标准解决方案。

在考虑兼容性问题时，一个关键问题是程序需要在多大的实现范围内工作。对于学习 C++ 来说，使用最完整、最有帮助的实现是有意义的。对于交付产品，为了最大化产品可以运行的系统数量，采取更保守的策略可能是合适的。在过去，这曾是避免使用被认为新颖的 C++ 特性的一个原因（而且往往只是一个借口）。然而，实现正在趋同，因此跨平台的可移植性需求不再像过去那样需要极度谨慎。

## 44.2 C++11 扩展

首先，我列出为 C++11 标准添加到 C++ 中的语言特性和标准库组件。接下来，我讨论处理旧版本（特别是 C++98）的方法。

### 44.2.1 语言特性

查看语言特性列表可能会让人感到困惑。记住，语言特性并不意味着孤立使用。特别是，C++11 中的大多数新特性，如果脱离旧特性所提供的框架，就没有意义。顺序大致按照它们在本书中首次出现的先后排列：

- [1] 使用 {}-列表的统一和通用初始化（§2.2.2，§6.3.5）
- [2] 从初始化器进行类型推导：`auto`（§2.2.2，§6.3.6.1）
- [3] 防止窄化（§2.2.2，§6.3.5）
- [4] 通用且有保证的常量表达式：`constexpr`（§2.2.3，§10.4，§12.1.6）
- [5] 范围 `for` 语句（§2.2.5，§9.5.1）
- [6] 空指针关键字：`nullptr`（§2.2.5，§7.2.2）
- [7] 有作用域且强类型的 `enum`：`enum class`（§2.3.3，§8.4.1）
- [8] 编译时断言：`static_assert`（§2.4.3.3，§24.4）
- [9] {}-列表到 `std::initializer_list` 的语言映射（§3.2.1.3，§17.3.4）
- [10] 右值引用（支持移动语义；§3.3.2，§7.7.2）
- [11] 以 `>>` 结尾的嵌套模板参数（`>` 之间无空格；§3.4.1）
- [12] Lambda 表达式（§3.4.3，§11.4）
- [13] 可变参数模板（§3.4.4，§28.6）
- [14] 类型别名和模板别名（§3.4.5，§6.5，§23.6）
- [15] Unicode 字符（§6.2.3.2，§7.3.2.2）
- [16] `long long` 整数类型（§6.2.4）
- [17] 对齐控制：`alignas` 和 `alignof`（§6.2.9）
- [18] 在声明中使用表达式类型作为类型的能力：`decltype`（§6.3.6.1）
- [19] 原始字符串字面量（§7.3.2.1）
- [20] 广义 POD（§8.2.6）
- [21] 广义 `union`（§8.3.1）
- [22] 局部类作为模板参数（§11.4.2，§25.2.1）
- [23] 后缀返回类型语法（§12.1.4）
- [24] 属性语法和两个标准属性：`[[carries_dependency]]`（§41.3）和 `[[noreturn]]`（§12.1.7）
- [25] 防止异常传播：`noexcept` 说明符（§13.5.1.1）
- [26] 测试表达式中是否可能发生 `throw`：`noexcept` 运算符（§13.5.1.1）
- [27] C99 特性：扩展整数类型（即可选更长整数类型的规则；§6.2.4）；窄/宽字符串的连接；`__func__` 和 `__STDC_HOSTED__`（§12.6.2）；`_Pragma(X)`（§12.6.3）；可变参数宏和空宏参数（§12.6）
- [28] 内联命名空间（§14.4.6）
- [29] 委托构造函数（§17.4.3）
- [30] 类内成员初始化器（§17.4.4）
- [31] 控制默认函数：`default`（§17.6）和 `delete`（§17.6.4）
- [32] 显式转换运算符（§18.4.2）
- [33] 用户定义字面量（§19.2.6）
- [34] 对 `template` 实例化更显式的控制：`extern templates`（§26.2.2）
- [35] 函数模板的默认模板参数（§25.2.5.1）
- [36] 继承构造函数（§20.3.5.1）
- [37] 覆盖控制：`override` 和 `final`（§20.3.4）
- [38] 更简单且更通用的 SFINAE 规则（§23.5.3.2）
- [39] 内存模型（§41.2）
- [40] 线程局部存储：`thread_local`（§42.2.8）

我并没有试图列出 C++11 中每一个对 C++98 的微小更改。关于这些特性的历史视角可以在 §1.4 中找到。

### 44.2.2 标准库组件

C++11 对标准库的补充有两种形式：新组件（如正则表达式匹配库）和对 C++98 组件的改进（如容器的移动构造函数）。

- [1] 容器的 `initializer_list` 构造函数（§3.2.1.3，§17.3.4，§31.3.2）
- [2] 容器的移动语义（§3.3.1，§17.5.2，§31.3.2）
- [3] 单向链表：`forward_list`（§4.4.5，§31.4.2）
- [4] 哈希容器：`unordered_map`、`unordered_multimap`、`unordered_set` 和 `unordered_multiset`（§4.4.5，§31.4.3）
- [5] 资源管理指针：`unique_ptr`、`shared_ptr` 和 `weak_ptr`（§5.2.1，§34.3）
- [6] 并发支持：`thread`（§5.3.1，§42.2）、互斥量（§5.3.4，§42.3.1）、锁（§5.3.4，§42.3.2）和条件变量（§5.3.4.1，§42.3.4）
- [7] 更高级别的并发支持：`packaged_task`、`future`、`promise` 和 `async()`（§5.3.5，§42.4）
- [8] `tuple`（§5.4.3，§28.5，§34.2.4.2）
- [9] 正则表达式：`regex`（§5.5，第 37 章）
- [10] 随机数：`uniform_int_distribution`、`normal_distribution`、`random_engine` 等（§5.6.3，§40.7）
- [11] 整数类型名称，例如 `int16_t`、`uint32_t` 和 `int_fast64_t`（§6.2.8，§43.7）
- [12] 固定大小的连续序列容器：`array`（§8.2.4，§34.2.1）
- [13] 异常的复制和重新抛出（§30.4.1.2）
- [14] 使用错误码进行错误报告：`system_error`（§30.4.3）
- [15] 容器的 `emplace()` 操作（§31.3.6）
- [16] `constexpr` 函数的广泛使用
- [17] `noexcept` 函数的系统化使用
- [18] 改进的函数适配器：`function` 和 `bind()`（§33.5）
- [19] `string` 到数值的转换（§36.3.5）
- [20] 有作用域的分配器（§34.4.4）
- [21] 类型特征，例如 `is_integral` 和 `is_base_of`（§35.4）
- [22] 时间工具：`duration` 和 `time_point`（§35.2）
- [23] 编译时有理数运算：`ratio`（§35.3）
- [24] 放弃进程：`quick_exit`（§15.4.3）
- [25] 更多算法，例如 `move()`、`copy_if()` 和 `is_sorted()`（第 32 章）
- [26] 垃圾收集 ABI（§34.5）
- [27] 低级并发支持：`atomic`（§41.3）

关于标准库的更多信息，可以在以下地方找到：

- 第 4 章、第 5 章和第 IV 部分
- 实现技术示例：`vector`（§13.6）、`string`（§19.3）和 `tuple`（§28.5）
- 新兴的专门讨论 C++11 标准库的文献，例如 [Williams,2012]
- 简要的历史视角可以在 §1.4 中找到。

### 44.2.3 已弃用的特性

通过弃用某个特性，标准委员会表达了希望该特性会消失的愿望（§iso.D）。然而，委员会没有授权立即移除一个使用广泛的特性——无论它多么冗余或危险。因此，弃用是对避免使用该特性的强烈提示。它可能在未来消失。编译器很可能会对弃用特性的使用发出警告。

- 对于带有析构函数的类，拷贝构造函数的生成和拷贝赋值的生成已被弃用。
- 不再允许将字符串字面量赋给 `char*`（§7.3.2）。
- C++98 异常规范已被弃用：
