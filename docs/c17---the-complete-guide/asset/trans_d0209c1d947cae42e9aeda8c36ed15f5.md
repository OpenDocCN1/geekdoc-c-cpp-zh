
请注意，对于迭代器，我们需要全局或静态对象，因为在编译时我们不能获取栈上对象的地址：

```
constexpr static std::array arr{0, 8, 15, 42};
constexpr auto pos = std::next(arr.rbegin());  // OK
static_assert(*pos == 15);                      // OK and doesn't fail
```

## 28.6 noexcept 扩展与修复

与自 C++11 以来每个新 C++ 版本的情况一样，在一些地方添加和/或修复了对 noexcept 的支持。

最重要的修复如下：

- 对于 std::vector<> 和 std::string（std::basic_string<>），C++17 保证不抛出异常
  - 在默认构造函数中（前提是分配器的默认构造函数不抛出异常）
  - 在移动构造函数中
  - 在接受分配器的构造函数中

- 对于所有容器（包括 std::string/std::basic_string<>），C++17 保证不抛出异常
  - 在移动赋值运算符中（前提是分配器可互换）
  - 在 swap() 函数中（前提是分配器可互换）

## 对向量重新分配的影响

请注意，noexcept 修复中有一个非常特殊且引人注目：现在只有向量和字符串保证在移动构造函数中不抛出异常。其他容器仍可能抛出异常。

如果这些类型用于向量中，这会产生重大影响，因为在重新分配时，只有当元素的移动构造函数保证不抛出异常时，向量才能使用移动语义。

换句话说：

- 现在保证重新分配 string/vector 的向量是快速的。
- 重新分配其他容器类型的向量可能会很慢。

这是将向量作为默认容器的又一个充分理由，除非你有充分的理由不这样做。

## 28.7 后记

std::uncaught_exceptions() 的动机最初由 Herb Sutter 在 http://wg21.link/n3614 中提出。该特性的最终接受措辞由 Herb Sutter 在 http://wg21.link/n4259 中制定。

扩展共享指针以支持数组类型并添加 reinterpret_pointer_cast 最初由 Peter Dimov 在 http://wg21.link/n3640 中提出。该特性的最终接受措辞由 Jonathan Wakely 在 http://wg21.link/p0414r2 中制定。

获取共享指针的弱指针类型的问题最初由 Arthur O’Dwyer 在 http://wg21.link/n4537 中提出。该特性的最终接受措辞由 Arthur O’Dwyer 在 http://wg21.link/p0163r0 中制定。

weak_from_this 最初由 Jonathan Wakely 和 Peter Dimov 在 http://wg21.link/p0033r0 中提出。该特性的最终接受措辞由 Jonathan Wakely 和 Peter Dimov 在 http://wg21.link/p0033r1 中制定。

数值 GCD 和 LCM 函数最初由 Walter E. Brown 在 http://wg21.link/n3845 中提出。它们成为第一个 Library Fundamentals TS 的一部分。对于 C++17，它们随后按照 Walter E. Brown 在 http://wg21.link/p0295r0 中的提议被采纳。

std::hypot() 的三参数重载最初由 Benson Ma 在 http://wg21.link/p0030r0 中提出。该特性的最终接受措辞由 Benson Ma 在 http://wg21.link/p0030r1 中制定。

添加特殊数学函数最初由 Walter E. Brown 于 2003 年在 http://wg21.link/n1422 中提出。通过采用国际标准 IS 29124:2010 使它们在 C++17 中成为强制性的提议由 Walter E. Brown、Axel Naumann 和 Edward Smith-Rowland 在 http://wg21.link/p0226r1 中提出。

chrono 扩展最初由 Howard Hinnant 在 http://wg21.link/p0092r0 中提出。该特性的最终接受措辞由 Howard Hinnant 在 http://wg21.link/p0092r1 中制定。

为 chrono 添加 constexpr 最初由 Howard Hinnant 在 http://wg21.link/p0505r0 中提出并被接受。该特性的最终接受措辞由 Howard Hinnant 在 http://wg21.link/p0092R1 中制定。

在其他多个地方添加 constexpr 的提议由 Antony Polukhin 在 http://wg21.link/p0031r0 和 http://wg21.link/p0426r1 中提出并被接受。

noexcept 的修复最初由 Nicolai Josuttis 在 http://wg21.link/4002 中提出。该修改的最终接受措辞由 Nicolai Josuttis 在 http://wg21.link/n4258 中制定。

## 第五部分

## 专家工具

本书的这一部分介绍了普通应用程序程序员通常不需要了解的新语言和库特性。它涵盖了为基础库程序员设计的特性，以及可能用于处理特殊问题（例如修改堆内存的处理方式）的特性。

此页有意留空

## 第 29 章

## 多态内存资源（PMR）

自 C++98 以来，标准库一直支持配置类分配其内部（堆）内存的方式。因此，标准库中几乎所有分配内存的类型都有一个分配器参数。这允许你配置容器、字符串和其他类型在需要比栈上分配的空间更多时分配其内部内存的方式。

分配此内存的默认方式是从堆中分配。然而，有多种原因需要修改这种默认行为：

- 你可以使用自己的内存分配方式来减少系统调用的次数。
- 你可以确保内存连续分配，以利用 CPU 缓存。
- 你可以将容器及其元素放入可供多个进程使用的共享内存中。
- 你甚至可以将这些堆内存调用重定向到先前在栈上分配的内存。

因此，修改默认行为可能有性能和功能上的原因。

然而，在 C++17 之前，（正确地）使用分配器在许多方面既棘手又笨拙（由于一些缺陷、过于复杂以及为了向后兼容所做的修改）。

C++17 现在为预定义和用户自定义的内存分配方式提供了一种相当易于使用的方法，可用于标准类型和用户自定义类型。

因此，本章讨论：

- 使用标准库提供的标准内存资源
- 定义自定义内存资源
- 为自定义类型提供内存资源支持

如果没有 Pablo Halpern、Arthur O’Dwyer、David Sankel 和 Jonathan Wakely 的大力帮助，本章是不可能完成的。

1 分配器最初的用途是为了能够处理不同大小的指针（“近”指针和“远”指针）。

### 29.1 使用标准内存资源

本节介绍标准内存资源及其使用方式。

### 29.1.1 动机示例

让我们首先比较使用和不使用标准内存资源时的内存消耗。

#### 为容器和字符串分配内存

假设在你的程序中，有一个由一些字符串组成的向量，你用相当长的字符串初始化它：

```
```cpp
#include <iostream>
#include <string>
#include <vector>
#include "../lang/tracknew.hpp"

int main()
{
	TrackNew::reset();
	std::vector<std::string> coll;
	for (int i=0; i < 1000; ++i) {
		coll.emplace_back("just a non-SSO string");
	}
	TrackNew::status();
}
```
```

请注意，我们使用一个跟踪所有 ::new 调用的类来跟踪内存分配次数，该类通过以下循环执行：

```
```cpp
std::vector<std::string> coll;
for (int i=0; i < 1000; ++i) {
	coll.emplace_back("just a non-SSO string");
}
```
```

会有大量分配，因为向量在内部使用内存来存储元素。此外，字符串元素本身可能会在堆上分配内存来保存其当前值（对于通常实现的小字符串优化，这通常仅在字符串超过 15 个字符时发生）。

程序的输出可能类似于以下内容：

1018 次分配，共 134,730 字节

这意味着每个元素一次分配，加上向量内部 18 次分配，因为向量分配了 18 次（更多）内存来容纳其元素。²

这种行为可能会变得至关重要，因为内存（重新）分配需要时间，并且在某些上下文中（例如嵌入式系统），分配堆内存本身可能就是一个问题。

我们可以要求向量提前预留足够的内存，但一般来说，除非你提前知道要处理的数据量，否则无法避免重新分配。如果你不确定要处理多少数据，你总是需要在避免重新分配和不浪费太多内存之间找到折衷方案。而且你至少需要 1001 次分配（一次分配用于容纳向量中的元素，以及每个不使用小字符串优化的字符串各一次分配）。

#### 不为容器分配内存

我们可以通过使用多态分配器轻松改善这种情况。首先，我们可以使用 std::pmr::vector，并允许向量在栈上分配其内存：

pmr/pmr1.cpp

```
#include <iostream>
#include <string>
#include <vector>
#include <array>
#include <cstdlib>  // for std::byte
#include <memory_resource>
#include "../../lang/tracknew.hpp"

int main()
{
    TrackNew::reset();

    // allocate some memory on the stack:
    std::array<std::byte, 200000> buf;

    // and use it as initial memory pool for a vector:
    std::pmr::monotonic_buffer_resource pool{buf.data(), buf.size()};
    std::pmr::vector<std::string> coll{&pool};

    for (int i=0; i < 1000; ++i) {
        coll.emplace_back("just a non-SSO string");
    }

    TrackNew::status();
}
```

2 重新分配的次数可能因平台而异，因为重新分配更多内存的算法不同。如果当前内存容量不足，一些实现会将其扩大 50%，而另一些实现会将内存大小加倍。
