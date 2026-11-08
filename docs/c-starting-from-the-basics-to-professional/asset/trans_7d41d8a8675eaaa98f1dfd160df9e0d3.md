

```cpp
int main()
{
    std::vector<std::string> names{"Frodo Baggins", "Gandalf the Gray",
        "Aragorn", "Samwise Gamgee", "Peregrin Took", "Meriadoc Brandybuck",
        "Gimli", "Legolas Greenleaf", "Boromir"};

    // Sort the names lexicographically
    std::sort(begin(names), end(names));
    std::cout << "Names sorted lexicographically:" << std::endl;
    for (const auto& name : names) std::cout << name << ", ";
    std::cout << std::endl;

    // Sort the names by length
    std::sort(begin(names), end(names),
        [](const auto& left, const auto& right) { return left.length() < right.length(); });
    std::cout << "Names sorted by length:" << std::endl;
    for (const auto& name : names) std::cout << name << ", ";
    std::cout << std::endl;
}
```

输出如下：

```text
Names sorted lexicographically:
Aragorn, Boromir, Frodo Baggins, Gandalf the Gray, Gimli, Legolas Greenleaf, Meriadoc
Brandybuck, Peregrin Took, Samwise Gamgee,

Names sorted by length:
Gimli, Aragorn, Boromir, Peregrin Took, Frodo Baggins, Samwise Gamgee, Gandalf the Gray,
Legolas Greenleaf, Meriadoc Brandybuck,
```

其他与排序相关的算法包括 `std::stable_sort()`（它保证不重排相等元素，例如 Ex20_15 中长度相等的字符串 "Peregrin Took" 和 "Frodo Baggins"）、`std::partial_sort()` / `partial_sort_copy()`（仅对前几个元素排序）以及 `std::is_sorted()`。从某种意义上说，`std::sort()` 的反面是 `std::shuffle()`，它以随机顺序排列元素。

## 并行算法

C++17 标准库最引人注目的新增内容之一，是大多数算法的并行版本。如今几乎每台计算机都有多个处理核心。就连最普通的手机现在也有多个处理核心。默认情况下，算法只使用其中一个核心。其他所有核心则可能闲置一旁，羡慕那个承担所有乐趣的核心。那真是可惜。处理大量数据时，如果算法能把工作分配给所有可用核心，运行速度会快得多。在 C++17 中，做到这一点变得易如反掌。例如，在 Ex20_15 中，要并行地对护戒小队排序，你只需告诉算法使用所谓的 `parallel execution policy`，如下所示：

```cpp
std::sort(std::execution::par, begin(names), end(names));
```

`std::execution::par` 常量由 execution 模块定义，所以必须先导入该模块。（该模块还提供其他执行策略，但这里不讨论。）

当然，护戒小队只有九名成员，你不太可能注意到任何差别。不过，如果换成萨鲁曼或索伦要对他们的军队名字排序，并行执行就合理得多。

几乎所有算法都可以通过这种方式并行化。这几乎不费什么成本，而收益可能很显著。因此，在处理较大的数据集时，请始终牢记这个选项。

> **提示**  `<algorithm>` 模块还定义了 `for_each()` 算法，你现在可以用它来并行化许多常规的基于范围的 for 循环。不过务必注意，循环的每次迭代都必须能够独立执行，否则就会遇到数据竞争。然而，数据竞争以及并发编程的其他方面超出了本书范围。

> **注意**  我们接下来讨论的基于范围的算法（目前还？）没有并行化重载。因此，要并行化算法执行，你仍然必须求助于我们在这里讨论的传统基于迭代器对的算法。

## 范围和视图

回顾迭代器模式的优点——简单、健壮、高效、灵活、可维护、可调试——你可能注意到，我们没有包括“能带来紧凑而优雅的代码”。确实如此：任何 C++ 开发者都会证明，使用迭代器对可能导致有些冗长和笨拙的代码。它或许比直接操作底层数据结构要好，但仍不如你所希望的那样紧凑和优雅。这正是 C++20 的范围和视图的用武之地。它们在迭代器之上增加了一层强大的额外抽象，使你能够比以往更舒适、更优雅地操作数据范围。

下文我们先从基础开始，即传统基于迭代器对算法的新*基于范围*替代方案。

### 基于范围的算法

到现在为止，你写过多少次 `begin(container), end(container)`？可能还没多到像我们一样对它厌烦，但也足以明白要点：这没必要地繁琐。例如 Ex20_15，你写了：

```
std::sort(begin(names), end(names));
```

直觉上，你想对 names 排序。你想对一个容器排序。一个值范围。必须不断在这种意图和迭代器对之间转换，很快就会令人乏味。而且这会导致代码笨拙而冗长。迭代器对很强大，但它们太细碎、太底层。

在 C++20 中，`std` 命名空间中的大多数算法因此在 `std::ranges` 命名空间中获得了等价的模板，使你能够直接处理范围，而不是迭代器对。得益于此，我们之前的 `std::sort()` 语句现在可以更优雅地写成如下形式：

```
std::ranges::sort(names);
```

有效的范围包括容器、静态大小的数组、字符串、字符串视图、`std::span`（见第 9 章）等——基本上任何支持 `begin()` 和 `end()` 的东西。在内部，基于范围的算法仍然使用迭代器，但作为库的用户，你不再需要不断接触它。本就该如此：一个好的、易于使用的 API 会隐藏实现细节（例如迭代器）。

在 §20.11A、§20.12A、§20.13B、§20.14A 和 §20.15A 中，你可以找到之前所有的算法示例，但这次是使用基于范围的算法而不是基于迭代器对的算法来表达的。

坦率地说，如果 C++20 中的范围所能提供的仅此而已，我们就已经欣喜若狂了。但还有更多更多：`<ranges>` 模块提供了一种全新且非常强大的范围，称为视图。不过，在我们继续讨论视图之前，先简单说说许多基于范围的算法的一个额外好特性，称为*投影*。

> **注意**  就像迭代器一样（见前文），范围也有不同种类：前向范围、双向范围、随机访问范围等。它们的分类在很大程度上与底层迭代器的分类相对应。不过，只有在阅读基于范围的算法规范时，这种区分才变得重要。例如，`std::ranges::sort()` 只适用于随机访问范围。因此，你不能将这个基于范围的算法应用于，比如说，一个 `std::list`。

### 投影

与 `std` 命名空间中的对应算法不同，许多（即使不是大多数）`std::ranges` 算法支持一个额外特性，称为*投影*。假设你想对一个 Box 序列排序，并且想按高度而不是体积排序。在 C++17 中，你可以按如下方式实现：

```
std::sort(begin(boxes), end(boxes),
    [](const Box& one, const Box& other) { return one.getHeight() < other.getHeight(); });
```

然而，在 C++20 中，你可以将其替换为以下内容：

```
std::ranges::sort(boxes, std::less{}, [](const Box& box) { return box.getHeight(); });
```

在元素被传递给比较函数之前，它会先经过一个投影函数。在这个例子中，投影函数先将所有 Box 转换为它们的高度，然后再交给通用的 `std::less{}` 函子。换句话说，`std::less{}` 函子总是接收两个 double 类型的值，却全然不知我们实际上是在对 Box 排序，而不是对 double 排序。

可选的投影参数甚至可以是指向（无参数）成员函数的指针，或指向（公有）成员变量的指针。这一点纯粹的优雅最好用一个例子来说明：

```
std::ranges::sort(boxes, std::less{}, &Box::getHeight);
// Or std::ranges::sort(boxes, std::less{}, &Box::m_height); should m_height be public
```

随后，投影要么通过在每个对象上调用给定的成员函数来实现，要么通过从每个对象读取给定成员变量的值来实现。

² 链表容器确实提供了 `sort()` 成员函数，你可以改用它们。

