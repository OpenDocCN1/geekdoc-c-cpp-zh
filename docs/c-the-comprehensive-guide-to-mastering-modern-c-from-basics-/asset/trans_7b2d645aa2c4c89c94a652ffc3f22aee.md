
- ○ 也有例外。在图 11.2 中，`const.hpp` 具有整合集中声明的作用。可能每个头文件都需要这些，因此将它们放在一个地方（即单个文件中），而不是分散在多个文件中，是很好的。

- ○ 避免循环依赖：

  - 一个 *.cpp 文件无论如何必须包含“自己的” *.hpp 文件。

  - 一个 *.cpp 文件可以使用该层级上的任何其他 *.hpp 文件。`teil2.cpp` 可以包含 `teil1.hpp`，如图 11.2 所示。图 11.2 中的 `teil1.cpp` 同时使用 `teil2.hpp` 也没有任何问题。

  - 这不适用于 *.hpp 文件。仅在特殊情况下包含同一层级的其他头文件。如果这样做，请务必严格保持单方向。在图中，`teil1.hpp` 可以使用 `teil2.hpp`，但反之则不然。

如果你尽可能地遵循这些规则，你将能够避免循环依赖。分层模型也有助于保持后期模块中所需的包含文件数量较低。它不是万灵药，但它是迈向正确方向的一步。

![](img/290cf954dfcaad53865de6b98cca8e6f_436_0.png)

**图 11.2** 将程序的组件划分为层以避免循环依赖。

## 模块化与 OOP

当你使用类和传统的面向对象进行整洁的工作时，每个类创建一个“模块”是一种自然的划分方式。在第 12 章中，将开始介绍 C++ 面向对象编程 (OOP)，在第 14 章，你将看到一个将项目拆分为类类模块的实际示例。

## 11.4 一个模块化示例项目

在 www://www.rheinwerk-computing.com/5927，你可以在 15p-unittest-200 目录下找到该项目。它包含了下表列出的文件和目录。为了方便实验，我将所有代码文件放在了一个 Compiler 链接中：https://godbolt.org/z/zj91TShny。

| 文件/目录 | 描述 |
|---|---|
| README.md | 项目描述 |
| Makefile | 主 Makefile——例如，用于 `make all` |
| all.mk | 所有 Makefiles 的定义 |
| include/ | 随库交付的包含文件 |
| - qwort/ | 库的所有公共包含文件 |
| - qwort.hpp | 库的主包含文件 |
| src/ | 所有实现文件 |
| - lib/ | 库的实现文件 |
| - Makefile | 库的 Makefile |
| - qwort.cpp | qwort 类的实现 |
| - - impl_multimap.hpp | 辅助类的定义 |

| 文件/目录 | 描述 |
| --- | --- |
| - impl_multimap.cpp | 辅助类的实现 |
| - prog/ | 可执行程序 |
| - Makefile | 程序的 Makefile |
| - query.cpp | 示例程序 |
| - dictfile.cpp | 示例程序 |
| - pg40185.txt | 用于索引的示例文本 |

**表 11.1** 示例项目的结构。

我稍后在第 14 章关于优秀代码的内容中还会使用这个项目来演示单元测试。

该项目包含一个我假设交付给客户的库。出于测试和演示目的，我想为客户提供两个小型示例程序，展示如何使用该库。这些示例程序是以源代码形式提供给客户，还是仅作为完成的程序提供并不重要。客户将收到头文件和编译后的库，但不会收到源代码。

这个示例库应主要由一个实现索引的类组成。它的功能类似于字典：顺序添加多个条目，然后构成索引。通过这种方式，你可以使用搜索模式查询索引以检查特定条目是否存在。精确搜索很无趣，所以我们进行“近似”搜索。搜索应该返回最佳匹配项。

我不想告诉客户更多信息。什么是“最佳匹配项”应该是一个实现细节。在这里，我想使用 q-grams 进行搜索，我将 q 的语言选择为 3。这意味着搜索将找到一个搜索模式中绝大多数三字符子串与条目匹配的条目。

如果索引包含例如 `Graumaus` 和 `Nagetierstamm`，那么通过 `Anagramm` 查询，你将找到后者，因为它们都包含 NAG 和 AMM，而前者与 Anagram 没有任何共同的三字母组。我不想在这里作为示例再多说关于算法的内容，因为这在这一章中确实是一个次要问题。（在翻译这一章时，我发现德语是做 q-grams 的极佳语言！）

如果在主目录下调用 `all`，那么 `src/lib/` 中的 `qwort.a` 库和 `src/prog/` 中的程序将连续构建。

这里的库只包含一组最小的文件：一个随库交付的头文件，以及实现文件。这些文件又包含两个 *.cpp 文件 `qwort.cpp` 和 `impl_multimap.cpp`，以及一个内部的 *.hpp 文件 `impl_multimap.hpp`，后者不用于交付。因此，它位于 `src/lib/`。如果你想支持动态链接，它也在 `qwort.hpp` 中。

### 头文件必须与文件匹配

```cpp
#ifndef QORT_H
#define QORT_H

#include <string>
#include <memory>
namespace qwort {
    namespace impl_multimap {
        class index_impl;
    }
    class index {
    public:
        index();
        index(const index&);
        index& operator=(const index&);
        index(index&&);
        index& operator=(index&&);
        void add(const std::string& arg);
        size_t size() const;
        std::string getMatch(const std::string& query);
        std::string normalize(std::string arg);
    private:
        std::unique_ptr<impl_multimap::index_impl> pimpl;
    };
} // namespace qw
#endif // QORT_H
```

**列表 11.1** qwort.hpp 的主头文件。

类的 `add` 和 `getMatch` 方法是库的实际接口：

- 首先，你通过默认的 `index()` 创建一个空索引。
- 然后，你使用 `add(const string&)` 逐个添加条目。
- 完成后，你可以随限制使用 `getMatch(const string&)` 进行查询。

所有导出库的内容定义在自己的命名空间中。因此，头文件以 `qw` 命名空间开始，所有的声明和定义都包含在其中。

随后是 `impl_multimap::index_impl` 类的声明。也为它开启了一个命名空间。所有可能的隐藏的内部库组件都包含在其中。然而，索引类在后续使用的 `index_impl` 类名称在这里是需要的。

### 使用命名空间切换实现

顺便说一下，该命名空间命名为 `impl_multimap` 是因为它包含了多种实现。在另一个目录下，你将看到 15p-unittest-100 项目，它定义了一个 `impl_simple_map` 命名空间，其中包含一个 `index_impl` 类。这是索引实现的另一种更简单的版本。

从原理上讲，你可以运行两个命名空间并在主类中轻松切换实现。然而，这只是一个建议，这就是为什么我只以粗略的方式展示。如果充分开发，这...

现在是索引类实际的主类。它的核心包含一个 index_impl 类的 pimpl 字段（作为指针）。通过这种“技巧”，可以更好地分离索引接口类的实现细节。为了避免类的类的用户被实现细节困扰（或保持其秘密），类的所有方法都进行了声明。

通常情况下，如你在第 17 章中看到的，你不需要定义析构函数、拷贝构造函数、移动构造函数、赋值运算符或移动运算符（“五大函数”）。编译器会为你优化地生成它们。遗憾的是，在这里是不可能的：编译器需要 `index_impl` 类的定义才能执行操作，否则它如何知道如何处理

