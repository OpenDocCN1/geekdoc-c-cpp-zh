
https://wg21.link/p2502
https://en.cppreference.com/w/cpp/header/generator

### C++23 多维下标运算符

第 6.13 节介绍了多维数组，并说明访问每个元素的一种方式是对每个维度分别使用 []——给定一个名为 values 的 int 二维数组，可以使用如下形式的表达式访问每个元素：

```
values[row][column]
```

遗憾的是，前面的语法不适用于自定义类，但程序员可以重载函数调用运算符 ()，它可以接受任意数量的参数。在表示二维数据的类中，可以使用如下表达式在名为 values 的对象上调用重载的 () 运算符：

```
values(row, column)
```

C++23 允许自定义类型通过接受任意数量以逗号分隔的参数来重载多维 [] 运算符，就像重载的 () 运算符一样。因此，前面的表达式可以用如下记法实现：

```
values[row, column]
```

### C++23 std::mdspan

第 7.10 节介绍了 std::span，用于创建数组、vector 和内置数组等容器中连续元素的视图。C++23 提供了 **std::mdspan**，用于创建**连续数据的多维视图**。它还支持选择该数据的子视图，称为**切片**。类 mdspan 实现了重载的多维 [] 运算符，用于访问 mdspan 视图中的元素。下面的代码片段使用一个 mdspan（第 2 行）将一个包含六个 int 元素的一维数组视为 2×3 数据，并按行显示元素：

```
1  std::array values{2, 3, 5, 7, 11, 13};
2  auto values2d{std::mdspan(values.data(), 2, 3)};
3
4  for (size_t row{0}; row != values2d.extent(0); ++row) {
5    for (size_t column{0}; column != values2d.extent(1); ++column) {
6      std::print("{:>2d} ", values2d[row, column]);
7    }
8
9    std::println("");
10 }
```

| 2 | 3 | 5 |
| --- | --- | --- |
| 7 | 11 | 13 |

有关 mdspan 的更多信息，请参见：

https://en.cppreference.com/w/cpp/container/mdspan

### C++23 容器增强

C++23 有多项容器增强：

- 现在可以从表示其他容器中元素范围的迭代器对初始化 stack 和 queue 容器适配器。例如，下面的代码片段从 int 的 vector 初始化一个 queue。有关更多信息，请参见 https://wg21.link/p1425。

  ```
  std::vector values{2, 3, 5, 7, 11, 13};
  std::queue myQueue(values.begin(), values.end());
  ```

- 关联容器（第 13.1.1 节）支持异构查找——可以使用兼容类型的值搜索键，而无需先将这些值转换为容器的键类型。例如，如果键是 std::string，可以向搜索函数传入 C 风格字符串或 std::string_views。现在，关联容器的成员函数 erase 和 extract 也支持这种异构查找能力。有关更多信息，请参见 https://wg21.link/p2077。

- `<flat_map>` 和 `<flat_set>` 头文件提供了容器适配器，用于将有序序列容器（默认是 vector）作为 map 和 set 来操作（第 13.1.1 节）。这些新的容器适配器比有序关联容器具有更好的性能特征。有关更多信息，请参见
  - https://www.sandordargo.com/blog/2022/10/05/cpp23-flat_map
  - https://en.cppreference.com/w/cpp/container/flat_map
  - https://en.cppreference.com/w/cpp/header/flat_set

### C++23 属性 `[[assume]]`

可以指出编译器应对源代码做出的假设，以便优化生成的目标代码。例如，下面代码片段中的第 2 行告诉编译器假定 denominator 不等于 0，因此编译器无需为除以 0 生成任何代码，这可能使代码更紧凑或更快：

```
int quotient(int numerator, int denominator) {
    [[assume(denominator != 0)]];
    return numerator / denominator;
}
```

有关更多信息，请参见

https://en.cppreference.com/w/cpp/language/attributes/assume

### C++23 `<stacktrace>` 头文件

第 12 章讨论了 C++ 的异常处理机制。Java、C# 和 Python 等各种编程语言允许在发生异常时以编程方式访问函数调用栈上有关函数的信息。新的 `<stacktrace>` 头文件为 C++ 增加了这些能力。有关更多信息，请参见

https://en.cppreference.com/w/cpp/header/stacktrace

### 为未来 C++ 版本考虑的特性

- 异步能力：提议的新特性包括三类组件——调度器、发送器和接收器——以及可自定义的**异步算法。** 要查看本文档的当前版本，请访问 https://wg21.link/P2300。

- **将列表初始化器传递给标准算法：** 在第 11.6 节中，我们演示了创建一个可以接收列表初始化器作为参数的函数。论文《P2248: Enabling List-Initialization For Algorithms》提出了新的标准库算法重载，它们接受初始化器列表作为参数。要查看本文档的当前版本，请访问 https://wg21.link/P2248。

### 视频参考资料

查看以下视频以了解更多 C++23 细节：

- Sy Brand，《C++23 有什么新特性》。
  - https://www.youtube.com/watch?v=mQzijnbnT04
- Timur Doumler，《C++23 如何改变我们编写代码的方式》。
  - https://www.youtube.com/watch?v=OH3PnMe02gs
- Marc Gregoire，《C++23——它能为你带来什么？》
  - https://www.youtube.com/watch?v=b0NkuoUkv0M

### 20.16 小结

在本章中，我们概述了其他 C++ 主题。我们展示了如何使用智能指针标准库类 shared_ptr 和 weak_ptr 来管理共享资源。我们演示了如何使用自定义删除器函数，使 shared_ptr 能够管理需要特殊销毁过程的资源。我们还解释了如何使用 weak_ptr 来防止循环引用数据中的内存泄漏。

接下来，我们介绍了另一种实现运行时多态的方法：通过 std::variant 类模板和标准库函数 std::visit 进行鸭子类型，处理彼此没有继承关系的类的对象。我们介绍了 protected 访问说明符——派生类的成员函数和派生类的友元可以访问基类的 protected 成员。

我们介绍了非虚接口（NVI）惯用法，其中每个基类函数只服务于一个目的——要么是客户端代码调用以执行任务的公有非虚函数，要么是派生类可以自定义的私有（或 protected）虚函数。你会看到，使用这种惯用法时，虚函数是隐藏于客户端代码的内部实现细节，使系统更易于维护和演进。

我们展示了如何继承基类构造函数，使编译器能够生成与基类构造函数匹配的派生类构造函数——当派生类构造函数只是调用相应的基类构造函数时，这尤其方便。我们演示了多重继承，讨论了它的潜在问题，并展示了虚继承如何解决这些问题。我们还解释了三种继承类型——public、protected 和 private——以及使用每种类型时基类成员在派生类中的可访问性。

我们讨论了存储类和存储期，以及它们如何影响对象生存期。我们展示了如何使用命名空间来避免命名冲突。你会看到，某些运算符符号可以表示为运算符关键字。

我们讨论了函数的尾置返回类型，并展示了 decltype 运算符使编译器能够在编译时确定表达式的类型。这两种能力在模板元编程（第 15 章）中被广泛使用。

我们介绍了 `[[nodiscard]]` 属性，用于指示不应忽略函数的返回值，并使用 C++20 对 `[[nodiscard]]` 的增强来指定为什么不应忽略返回值。如果你不使用 `[[nodiscard]]` 函数的返回值，编译器会在警告消息中显示原因。

最后，我们介绍了最近发布的 C++23 标准中的一些关键新特性。在下一章中，我们将实现各种搜索和排序算法。我们还将讨论用于表示算法效率的大 O 记法，并用它来比较各种流行搜索和排序算法的性能。
