

```cpp
    return sHash(a.city_j);
}
int main() {
    unordered_multiset<Entry, Hash, EqEntry> directory({
        Entry("New York", 10001);
        Entry("New York", 10002);
        Entry("New York", 10003);
        Entry("Chicago", 60601);
        Entry("Chicago", 60602);
    });
    const Entry search("New York", // 搜索时忽略邮邮编码
    cout << "New York has " << directory.count(search) << " ZIP codes.\n";
    cout << "The ZIP codes of New York are:\n";
    auto (where, until) = directory.equal_range(search);
    while (where != until) {
        cout << where->zip_j << '\n';
    }
}
```

# **Listing 24.85** 你可以只使用对象的一部分作为键。

输出如下：

New York has 3 ZIP codes.
The ZIP codes of New York are:
10001
10002
10003

作为模板参数指定的 EqEntry 和 HashEntry 仿函数确保了所有 `city_name` 相同的条目都被视为相等的。仅定义哈希函数或仅定义相等性是不够的；这两个操作必须匹配，否则条目会混杂，无法进入正确的桶（buckets）。因此，你必须仔细选择并编写这两个仿函数。

例如，如果你在哈希函数中包含了比相等性中更多的元素，你将无法通过 `count(search)` 找到条目，只能通过 `count(Entry("New York", 10001))` 找到。这可能正是你想要的，但你的哈希函数并不是最优的，你应该包含 `zip_`：

```cpp
struct EqEntry {
    bool operator()(const EqEntry& a, const EqEntry& b) const {
        return tie(a.city_j, a.zip_j) == tie(b.city_j, b.zip_j); // 真的吗？
    }
};
struct HashEntry {
    std::hash sHash;
    size_t operator()(const HashEntry& a) const {
        return sHash(a.city_j);
    }
};
```

如果相等性涵盖的元素比哈希仿函数少，情况就会反过来：

```cpp
// https://godbolt.org/r/cve7BEEi7o
struct Entry {
    bool operator()(const Entry& a, const Entry& b) const {
        return a.city == b.city;
    }
};

struct HashEntry {
    std::hash<string> hash;
    std::hash<int> hash;
    size_t operator()(const Entry& a) const {
        return hash(a.city) ^ hash(a.zip); // 元素太多了
    }
};
```

现在你可能再找不到单个条目了。不同的 New York（实际上通过 `==` 是相等的）落在了不同的哈希桶中，分布在整个容器中。你仍然有机会找到特定的条目，如 `Entry("New York, 10001")`。然而，由于两个 New York 条目也可能落在同一个桶中，即使这一点也无法保证。结果就是数据垃圾。

# 初始化

关于模板参数，你声明 `unordered_multiset` 就像声明 `unordered_set` 一样，这意味着你需要指定条目或键类型，还可以指定哈希函数、键比较仿函数和分配器。

但是，从 C++17 开始，编译器通常可以通过构造函数参数推导出模板参数来帮助你。

通过构造函数初始化的与 `unordered_set` 类似，不同在于保留了重复项。在这里，除了拷贝构造函数外，所有选项都可以接受额外的参数来指定哈希表的初始大小：

- 不带参数的默认构造函数将容器初始化为空。
- 另一个另一个容器或流的迭代器对拷贝它们定义的范围。
- 在初始化列表中，你可以显式地指定初始元素。
- 你可以完全拷贝另一个 `unordered_multiset`。
- 从 C++23 开始，还有一个带有 `from_range` 标签的构造函数。

注意下面的示例，重复项被保留了。

```cpp
// https://cppbolt.com/z/bUf8Hse
#include <unordered_set> using unordered_multiset
#include <vector>
#include <iostream>
using unordered_multiset; using std::cout; using std::ostream;
template<typename E>
std::ostream& operator<<(std::ostream& os, const unordered_multiset<E>& data) {
    for (auto &e : data) { os << e << " "; }
    return os;
}
int main() {
    // 不带参数
    unordered_multiset empty(1000); // 哈希表的初始大小
    cout << empty; 
    // 初始化列表包含重复项：
    unordered_multiset data{1,1,2,2,3,4,4,5,5};
    cout << data; // 输出: 5 5 4 4 3 2 2 1
    // 拷贝
    unordered_multiset copy(data);
    cout << copy; // 输出: 5 5 4 4 3 2 2 1
    // 范围
    std::vector<int> vec{1,2,3,10,20,30,20,30,1,2,3};
    unordered_multiset range(vec.begin(),vec.end());
    cout << range; // 输出: 30 30 20 20 10
}
```

**List 24.86** 这些是初始化 "unordered_multiset" 的方法。当然，输出中元素的顺序随系统而异。

# 赋值

对于所有其他容器，你都可以使用 `operator=` 拷贝或移动另一个 `unordered_multiset`。此外，`swap` 用于快速交换。

# 插入

`unordered_multiset` 中的插入操作就像 `multiset` 一样。与 `unordered_set` 不同，每次插入都是成功的，因为存储了重复项：

- 使用 `insert` 自动定位并将单个元素插入容器，而使用 `emplace` 在原位创建。
- 使用迭代器 `insert` 插入单个元素，可以节省哈希值的计算和桶内元素的遍历。位置提示应该指向相同的元素。如果你没有提供正确的元素，这种优势就会丢失，但元素会进入正确的位置。
- 使用迭代器对 `insert` 插入多个元素。从 C++23 开始，还有 `insert_range`。通过 `merge` 从另一个容器检索所有元素，包括重复项。

如果你使用了 `reserve` 准备，必须假设插入后指向容器的迭代器已失效。

# 访问

你可以使用正向迭代器，如表 24.2 所示：

- 通过 `begin()` 和 `end()` 以及 `cbegin()` 和 `cend()` 迭代器访问容器的开头和结尾。
- 通过 `find` 访问任何匹配元素，如果没有则返回 `end()`。对于多变类型，`count` 和 `equal_range` 方法很有意义：通过 `count` 可以计算元素的数量，通过 `contains` 可以检查存在性。`equal_range` 方法返回所有匹配元素的迭代器对。

这是一个访问 `unordered_multiset` 的示例：

```cpp
// https://cppreference.com/w/cpp/unordered_multiset
#include <unordered_set> // unordered_multiset
#include <iostream>
#include <string>

using std::unordered_multiset; using std::cout; using std::string;
int main() {
  const string in = "She sells shells by the seashore.";
  unordered_multiset<int> cs(in.begin(),in.end()); // string 作为容器
  cout << cs.count('s') << " times\n"; // 输出: 7 times
}
```

**Listing 24.87** 对于 "multi" 变，`count` 很有意义。如果创建键的开销很大且你只需要进行搜索，请考虑 `unordered_multiset`。这允许你在不创建完整键的情况下进行搜索。

# 删除

删除时，未删除元素之间的相对顺序仍然有效，因为迭代器引用了这些元素：

- `clear()` 删除所有元素。
- 使用值 `erase` 删除或转移单个元素删除该元素的所有出现处。返回值是删除元素的数量。如果你指定一个迭代器，该位置的元素被删除。返回值是下一个元素的位置。通过 `extract`，你可以删除一个通常会插入到别处的元素。
- 使用迭代器对 `erase` 多个元素，可以删除多个元素。这对于无序容器实际上只有在范围包含所有元素（等同于 `clear()`）或包含 `equal_range` 的全部部分元素时才有意义。这都是可能的，但在实践中可能很少见。删除也适用于包含不同元素的区域，但对于无序容器，很难预测位于之间的元素。

# 特性：通过桶

你可以通过 `bucket_count()`、`bucket_size` 和 `bucket` 以及 `begin(int)` 和 `end(int)` 的 int 变体获取 `unordered_multiset` 内部工作的详细见解。

# 特性：预留空间

为了防止插入时哈希表重新导致的意外中断，可以使用 `load_factor`、`max_load_factor`、`rehash` 和 `reserve` 方法操作哈希机制。

> `unordered_map` 可以完成 24.8.7 “unordered_multimap 可以做的事”（节 24.7.6），但作为一种无序关联容器，它还有一个与 `unordered_multiset`（节 24.8.6）密切相关的接口。

键被映射到目标值，这通常需要 O(1) 时间，但在特殊情况下也需要 O(n)。键不是使用小于号，而是使用 `==` 和哈希函数进行比较。

一个键可以插入多次，每次都引用目标值。

# 元素属性

对于所有类似 map 的容器，`unordered_multimap` 的元素类型都是 `pair<const Key, Target>`。这意味着如果你有一个元素或 Target 的引用，你可以为 Target 分配一个新值。Key 是 `const`，在任何情况下都不得更改；否则容器会产生混乱。

[ 62 ]

对于键，必须检查相等性 `==` 且必须可计算哈希值。这可以通过自由函数 `operator==` 和仿函数 `std::hash<Key>` 实现，也可以通过模板参数指定你自己的仿函数。

