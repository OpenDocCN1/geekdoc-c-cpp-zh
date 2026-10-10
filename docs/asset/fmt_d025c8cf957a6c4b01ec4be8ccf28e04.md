
`valarray` 并不常见。不过，你可以在《Thinking in C++》中找到更多示例。[ 66 ]。

# 25 容器支持

## Telegram 章节

- *迭代器 (Iterator)*
  一种引用容器内元素的模型。

- *算法 (Algorithmus)*
  对容器内容的高级操作。

- *范围 (Range)*
  一种与迭代器相关的高级模型。范围表示一个可以独立存在的序列，但通常指容器。

- *视图 (View)*
  一种轻量级的范围，通常指一个范围或其部分。虽然范围作为一个概念存在，但视图是具体的实例，表示范围与操作或过滤器的组合。视图是 `lazy`（懒性）的，并且可以通过 `operator|` 组合成流水线。

- *范围适配器 (Range adapter)*
  一种创建视图的函数对象；即它在范围上定义了一个操作或过滤器。

- *范围工厂 (Range factory)*
  一种不基于范围而是将值作为范围本身生成的函数对象。

标准库中的算法是作用于迭代器的实用函数，通常的操作方式是：迭代器定义了算法所应用于容器的“`areas`（区域）”。因此，你经常会看到参数以迭代器对的形式出现——即 `begin` 和 `end`。

范围是这些迭代器对的继任者，它们与视图一起扩展了算法。所有来自 `std` 接收迭代器对的算法现在都可以在 `std::ranges` 中通过范围作为参数找到——标准称它们为受限算法（constrained algorithms）。我觉得这个名字具有误导性，因为 `std::ranges` 中的算法完全没有限制性，反而是被扩展了：

- 它们接受范围作为参数，但也与迭代器对配合。
- 它们通常返回范围，因此可以与视图直接组合。
- 它们一致地支持一个可选的投影参数（projection parameter），允许使用函数对象（functor）访问范围元素——例如通过指定成员函数。

因此，你可以预期范围算法将比经典算法更快被扩展。事实确实如此。例如，`ranges::starts_with()` 已经不再有 `std` 中对应的实现了。我在上一个关于容器的章节中提到了算法和范围，因为它们是相辅相成的。来自`<algorithm>`、`<numeric>` 和`<ranges>` 头文件的算法、范围和视图大部分都与容器一起。你也可以编写自己的算法和视图。

在本章中，我将尝试让你们熟悉算法、范围和视图。当我谈到算法时，我通常指的是 `std` 命名空间下 `<algorithm>` 中的函数——那些以迭代器为参数来描述容器内部区域的经典算法。视图和范围是 C++20 新引入，来自 `<ranges>` 头文件，并位于 `std::ranges` 和 `std::ranges::views` 命名空间中。特别是，视图通常也实现了算法，但从标准库的角度来看，它们不被视为算法。然而，它们也支持与容器配合。

## 算法、范围和视图的命名空间

对于范围，引入了 `std::ranges` 命名空间。非常常见将其缩写为 `rng = std::ranges`（或使用 `rg`）。`std::ranges::views` 命名空间包含视图。它有一个别名 `std::views`，并且通常使用 `vws = std::ranges::views`（或 `vs`）进行缩写。

有些东西在 `std` 和 `std::ranges` 中都有定义。例如，`size()`、`begin()` 和 `sort()`。在这种情况下，你应该优先选择新的命名空间，因为新的变体通常包含了额外的函数，并且解决了一些缺陷。

不要使用 `namespace std::ranges` 和 `using namespace std::views`！这会让事情变得不可团，并成为糟糕 Bug 的根源。在书中，我通常使用 `ranges`、`rng` 和 `rs` 别名，以及 `views` 和 `vs`。

## 25.1 算法

在标准库的上下文中，什么是算法？经典算法都是一个函数模板。从更广泛的角度来说，新的视图也是算法。这个函数或类做了一些有用的事情，而且它所做是以一种非常通用——泛型（generic）的方式实现的。算法函数和视图实际上是模板，这一事实恰是因为它们旨在泛泛地工作：它们应该在尽可能多的序列和具有尽可能多的元素类型上工作。

每个算法必须对其行为有详尽的文档说明。你需要能够阅读文档，并确切知道算法在处理你的数据时的行为如何。如果它执行了有害操作，例如消耗过多的内存或运行时间过长，那么这种情况也必须在文档中进行描述。

如果你需要解决一个已经解决、或者可以通过 `<algorithm>`、`<numeric>` 或 `<ranges>` 轻松解决的问题，那么你就应该使用它们：

- 这些函数和类经过了许多程序员的测试并持续持续维护。
- 算法和范围适配器是构建块，你可以将它们组装成复杂的任务。
- 因此，使用构建块编写代码更简单。
- 使用构建块制造的代码更容易调试。
- 使用模块（modules）制造的代码在稍后验证时尤为容易，且更易于修订。

我想通过一个例子来来说明最后三点。

```cpp
// https://godbolt.org/z/icWvThn3a

std::vector v{0,1,3,5,7,9,2,4,6,8};

bool flag = true;

for(size_t i=1; (i < v.size()) && flag; ++i) {

    flag = false;

    for(size_t j=0; (j < v.size()-1); ++j) {

        if(v[j+1] < v[j]) {

            std::swap(v[j+1], v[j]);

            flag = true;

        }

    }

}

for(int i:v) std::cout << i << ' ';
```

### 列表 25.1 做了某些事情

```cpp
// https://godbolt.org/z/icWvThn3a

std::vector v{0,1,3,5,7,9,2,4,6,8};

bool flag = true;

for(size_t i=1; (i < v.size()) && flag; ++i) {

    flag = false;

    for(size_t j=0; (j < v.size()-1); ++j) {

        if(v[j+1] < v[j]) {

            std::swap(v[j+1], v[j]);

            flag = true;

        }

    }

}

for(int i:v) std::cout << i << ' ';
```

### 列表 25.1 做了了某些事情

```cpp
// https://godbolt.org/z/EIJTPPv7

std::vector v{0,1,3,5,7,9,2,4,6,8};

std::sort(v.begin(), v.end());

for(int i:v) std::cout << i << ' ';

// 或者使用范围：

std::ranges::sort(v);

for(int i:v) std::cout << i << ' ';
```

### 列表 25.2 输入向量将被排序！

如果你看 25.1，你可能会说：“那可能实现了冒泡排序。”但对于 25.2，你可以立即说：“那在排序。”而且这完全不是：你多久才能确定两者都是正确的？为什么 25.1 有时在循环中使用 `i=1; (i < v.size())` 而其他时候使用 `j=0; (j < v.size()-1)`？空向量或单个元素的情况如何？让我告诉你：列表是正确的，而且——是的——它实现了冒泡排序。但你肯定理解我的意思。获得 25.1 需要更多的时间（或经验）。

## 25.2 迭代器与范围

关于迭代器的详细介绍参见第 24 章第 2 节。范围和视图如何工作的参见第 24 章第 1.7 节。在这里，我将总结对算法工作重要的事情。

每个算法和每个范围适配器对其接收的迭代器或范围施加某些要求。在 C++20 之前，迭代器分类非常重要；现在它们被真正的概念（concepts）所取代。分类和迭代器概念是相互构建的。规则是：分类越高，对迭代器的要求越多；它必须支持更多的操作。

每个容器类型的迭代器与其相应的分类相关联。这允许你看到哪些容器与算法是兼容的。别忘了流也提供了迭代器，因此可以与许多算法配合。

我将为你展示迭代器分类的层级结构。在 C++20 中，分类名称被赋予了 Legacy 前缀，我在这里省略了它。例如，如果一个算法要求迭代器遵循 Forwarditerator 分类，这意味着可以进行多次赋值 `it = begin`、自增 `++it` 以及读取 `*it`：

- 迭代器：仅需要自增；只能遍历一次

* `OutputIterator`（输出迭代器）：类似于 Iterator 且支持写入
* `InputIterator`（输入迭代器）：类似于 Iterator 且支持读取
* `ForwardIterator`（前进迭代器）：类似于 InputIterator 且支持多次遍历
* `BidirectionalIterator`（双向迭代器）：类似于 ForwardIterator 且支持反向遍历
* `RandomAccessIterator`（随机访问迭代器）：类似于 BidirectionalIterator 且支持随机访问
* `ContiguousIterator`（连续迭代器）：类似于 RandomAccessIterator 且元素在内存中是连续的

从 C++20 开始，这些已经被实际的概念（concepts）所取代。这些概念也是相互构建的，但概念的数量与迭代器的数量大致对等。最重要的概念对应于各个类别。例如，有一个 `input_iterator` 概念，对应于 `InputIterator` 类别。我就不再进行显式的列举了。

更为重要的是范围概念（range concepts）。它们也与迭代器类别对齐。所以——你猜对了，有 `range::input_range`，它表示范围是由 `input_iterator` 构建的。原理如此简单。几乎如此。因为有一些范围概念超越了迭代器类别：

- `view`（视图）
  该范围是一个视图，所以与容器不同，它可以被高效地拷贝。

- `borrowed_range`（借用范围）
  该范围提供的迭代器在范围失效后仍然有效。请注意，这些迭代器所引用的容器必须仍然有效。

- `sized_range`（有尺寸范围）
  可以指定元素的数量。

- `common_range`（通用范围）
  哨兵（sentinel）是一个迭代器，因此 `begin()` 和 `end()` 具有相同的类型。这对于所有容器和许多视图都是的，但例如对于 `take_view`、`drop_view` 或 `iota_view` 则不成立。

- `viewable_range`（可视范围）
  可以通过 `views::all` 转换为视图。

- `constant_range`（常量范围）
  元素不被修改，类似于 `const_iterator`。

当我稍后列出算法时，我将使用表 25.1 中的术语。你可以看到哪些迭代器要求需要哪些操作。表格还提供了符合要求的容器示例。例如，你可以看到双向迭代器的要求被 `vec`、`list` 和 `set` 满足，但 `unordered_set` 不满足。我将 `vector` 缩写为 `vec`，`unordered_set` 缩写为 `u-set`，并仅作为示例提及。

| Requirement | Abbr. | Possible Parameters | vec | list | set | u-set |
|---|---|---|---|---|---|---|
| Input | in | in, fw, bi, ra, ct | Yes | Yes | Yes | Yes |
| Output | out | out, fw, bi, ra, ct | Yes | Yes | Yes | Yes |
| Forward | fw | fw, bi, ra, ct | Yes | Yes | Yes | Yes |
| Bidirectional | bi | bi, ra, ct | Yes | Yes | Yes | - |
| Random access | ra | ra, ct | Yes | - | - | - |
| Contiguous | ct | ct | Yes | - | - | - |

**表 25.1** 迭代器要求与示例容器的兼容性。

## 25.3 迭代器适配器

迭代器是标准库的核心部分，并且主要是一种概念。通过进一步的抽象，可以在不干扰设计理念的情况下，使用迭代器适配器意外地频繁修改算法的行为。这些适配器中的许多可以在 `<iterator>` 中找到。我无法在算法的解释列表中涵盖所有可能的组合，但为了给你的想象一些刺激，这里有一些示例：

- 使用 `move_iterator`，你可以将算法的所有拷贝操作转换为移动操作。
- 使用 `back_inserter`，你不需要预先存在的目标范围；相反，每次拷贝都会转换为 `push_back`。
- `front_inserter` 执行相同的操作，但它调用的是 `push_front`。
- 灵活的是 `inserter`，它会在特定位置连续调用 `insert`。
- `ostream_iterator` 向流中的输出端进行拷贝。
- `istream_iterator` 执行相同的操作，但它将值从流中拷贝到容器中。
- `reverse_iterator` 将每次 `++` 操作转换为 `--`。

## 25.4 标准库中的算法

本章语境下的所有算法、范围和视图都是来自 `<algorithm>` 和 `<ranges>` 头文件的函数模板或类。有些来自 `<numeric>`，我会单独提到。通常，算法与容器协同工作，并使用迭代器作为手段。这反过来导致算法也可以与流一起工作，因为流也提供了迭代器。

所有算法都实现为模板，这意味着算法代码可以被编译器自动作为内联（inline）即时使用。与具有潜在虚拟方法会阻止内联的对象层次结构不同，这提供了可能获得的最高性能。对于标准库算法而言，在通用实现范围内达到最大速度是其顶级设计原则之一。

![](img/290cf954dfcaad53865de6b98cca8e6f_1274_0.png)

**图 25.1** 容器并不直接与算法工作，而是通过迭代器与它们“通信”。

## 算法不删除或插入

算法和范围适配器始终只在现有的范围上工作。如果它们产生输出，目标范围必须已经存在。算法*从不插入自己*。然而，你可以通过迭代器适配器来实现这一点。

此外，被移除的算法和范围适配器从不真正删除自己。它们通过重新排列元素来模拟这种行为，并告知你未使用元素所在的位置。你作为用户，负责实际的删除。算法无法假设元素是否以及如何被真实地删除或销毁。这一组中最明显的代表是 `remove`（以及 `ranges::unique`），但它们只是将“被移除的”元素移动到指定范围的末。这些函数的返回值是一个 `iterator`。你实际上会删除元素，例如通过 `cont.erase(it, cont.end())`。

这些函数总是通用的且非常抽象的。有时你必须跳出固有思维来思考如何组合算法以完成复杂任务。例如：你知道 `cat data.txt | sort | uniq` 命令序列吗？它移除了文件 `data.txt` 中所有重复行。如果你以正确的方式组合它们，C++ 算法也可以实现相同的操作。

```cpp
// https://godbolt.org/z/9xrPBEhvd

#include <algorithm>
```

```cpp
#include <vector>
#include <iostream>

void sort_uniq(std::vector<int> &data) { // sorting
    std::ranges::sort(data);
    auto to_delete = std::ranges::unique(data); // move to the back
    data.erase(to_delete.begin(), to_delete.end()); // actually delete
}

int main() {
    std::vector<int> ns{1,5,2,3,9,2,2,2,1,5,2,3,1,1,2,2,1};
    sort_uniq(ns);
    std::ranges::for_each(ns, [](auto x) {
        std::cout << x << ' ';
    });
    std::cout << '\n'; // Output: 1 2 3 5 9
}
```
