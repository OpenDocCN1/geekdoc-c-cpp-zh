
emplace()，它在容器内部直接创建对象。
范围变体从 C++23 起可用。

- push_front() push_back() emplace_front() emplace_back()
使用这些方法向序列容器添加单个元素。在这里，vector 也很很快。

- assign() assign_range() swap() merge()
`assign()` 允许你重新初始化容器。通过 `swap()`，你可以非常高效地交换两个相似且已排序的容器的全部内容。`merge()` 合并两个相似且已排序的容器。`assign_range()` 从 C++23 起可用。

- prepend_range() append_range()
从 C++23 开始，你还可以将整个范围插入到序列容器中。

- erase() extract()
使用 `erase()` 单个元素或范围。
通过 `extract()`，你移除一个元素并打算将其插入到其他地方。

- find() count() contains()
在关联容器中查找特定元素或统计其出现次数。从 C++20 开始，还有 `contains` 方法。

像 `c.size()` 这样的方法（也可以作为自由函数如 `size(c)` 可用）允许编写更通用的代码。
你不再需要修改现有的容器类型（可能来自第三方），而是可以重载自由函数并在那里实现功能。

## 24.5 标准容器类概览

首先，容器可以大致分为四组：

- 序列容器（Sequence-based containers）
这些容器中的访问和插入按顺序进行，或者以数字作为索引逐个元素进行。`vector` 和 `array` 就是示例。通常你在末端或两端删除和添加元素。某些支持通过 `[int]` 或 `at(int)` 进行高效直接元素访问。

- 有序关联容器（Associative ordered containers）
这些容器使用任何数据类型进行访问，而不是数字。例如，通过编写 `cities["Berlin"] = 1000` 将城市名称与其历史德国邮编关联。在此类容器中，你可以在任意位置插入元素。关联容器根据其键永久排序。与序列容器一样，你可以按顺序读取所有元素——因为键总是排序的，所以当你迭代时，获取的元素是有序的。关联容器上的所有操作在资源消耗上都有保证的上界，无论你向容器中输入什么数据。

- 无序关联容器（Associative unordered containers）
从外部看，无序关联容器看起来像普通的关联容器，并且具有几乎相同的接口。区别在于，它们最重要的操作通常更快，但不保证。它们基于哈希而不是排序。这种哈希可能会下降并显著降低性能。我建议在普通情况下使用有序关联容器，仅在特殊情况下刻意切换到无序变体。

- 容器适配器（Container adapters）
现有的序列容器和关联容器如此强大且配备了丰富的接口和良好的性能保证，以至于你可以将它们用于更简单的容器。例如，`vector` 拥有 `stack` 需要的所有方法。为 `stack` 提供一个不支持迭代的独立容器是没有必要的。为此，有一组小型的适配器，它们在内部持有另一个容器，但在外部提供简化或稍微重新设计的接口。

## 24.5.1 容器的类型别名

在后文中，知道我们正在讨论的是哪种类型有时是重要的。容器处理多种类型。当然还有容器类型本身。它由一个模板组成，在你编写它并带有模板参数时就会实例化。通过至少一个模板参数，你指定了存储在容器中的元素类型。例如，具有 `int` 元素类型的 `vector` 容器变为 `vector<int>`，从而成为容器的类型。

除了数据和方法外，所有容器还包含一些类型别名。我将最重要的别名汇总在表 24.3 中。一方面，当我向你介绍容器时会使用这些术语；另一方面，你可以使用这些类型别名为不同容器类型编写一致的代码——也许以后在你自己的模板中也使用它们。在某些情况下，该类型真的只是另一个（或不那么简单）的类型的别名；例如，`vector<int>` 的 `value_type` 是 `int` 的别名。在其他情况下（如 `iterator`），底层类型未由标准指定，仅通过其属性描述。这时你必须使用别名，因为你无法（可移植地）编写具体类型。

在这里清晰地应用这些术语并不总是容易的。对于 `map`，“value”一词是歧义的，因为它通常被用于“它将一个键映射到一个值”。但 `map` 的 `value_type` 实际上定义为 `pair<key_type,mapped_type>`。因此，在这种情况下，我倾向于使用“target”一词。我力求在书中使用以下清晰的术语：

- `value_type` 的 value 或 element
- `key_type` 的 key
- `target type` 的 target 或 `mapped_type` 的 mapped type

| 类型别名 | 含义 | vector<int>... | set<int>... | map<int, string>... |
| :--- | :--- | :--- | :--- | :--- |
| value_type | 容器的元素 | int | int | pair<const int, string> |
| key_type | 元素的键部分 | - | int | int |
| mapped_type | 元素的映射部分 | - | - | string |
| size_type | 大小或索引 | size_t | size_t | size_t |
| reference | 引用 | int& | int& | pair<const int, string>& |
| iterator | 可修改容器中的迭代器 | 是 | 是 | 是 |
| const_iterator | 不变容器中的迭代器 | 是 | 是 | 是 |
| reverse_iterator | 反向迭代器 | 是 | 是 | 是 |

**表 24.3** 容器类型别名概览。

即使放弃使用 `auto`，你也可以使用这些别名编写适用于每个容器的代码。

```cpp
// https://cppbolt.org/z/c93
#include <vector>
#include <map>
#include <iostream>
using std::cout;
using std::ostream;

template<typename K, typename T>
ostream& operator<<=(ostream& os, const std::pair<const K, T>& value) {
    return os << value.first << ', ' << value.second << ']';
}

int main() {
    using Cont = std::vector<int>;
    Cont cont1 = {1, 2, 3, 4, 5, 6};
    Cont::size_type sz = cont1.size();
    cout << "size: " << sz << " content: " << "\n";
    for(Cont::const_iterator it = cont1.begin(); it != cont1.end(); ++it) {
        cout << *it << ",";
    }
    cout << "\n";

    using Cont = std::map<int,char>;
    Cont cont2 = {{1,'a'}, {2,'b'}, {3,'c'}, {4,'d'}, {5,'e'}, {6,'f'}};
    Cont::size_type sz = cont2.size();
    cout << "size: " << sz << " content: " << "\n";
    for(Cont::const_iterator it = cont2.begin(); it != cont2.end(); ++it) {
        cout << *it << ", ";
    }
    cout << "\n";
}
```

**列表 24.11** 类型别名有时比具体类型更清晰。

