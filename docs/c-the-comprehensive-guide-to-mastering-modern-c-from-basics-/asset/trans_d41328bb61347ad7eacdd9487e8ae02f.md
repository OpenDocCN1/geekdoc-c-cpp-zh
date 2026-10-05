

| 属性 | set | map | multiset | multimap |
|---|---|---|---|---|
| 迭代器/范围 | 随机 | 随机 | 随机 | 随机 |
| 算法 | 所有 | 所有 | 所有 | 所有 |

**表 24.7** 有序关联容器的属性。星号的含义将在后文解释。

## 24.7.2 有序关联容器的方法

为了节省空间并提高清晰度，我这里的函数签名并不总是非常精确或详细。如果我没有在方法后加上括号，通常意味着有多个重载：

- 构造函数：C(), C(Compare), C{}, C(It, It), **C(from_range, rg)**
  默认构造函数 `C()` 创建一个空容器。通过来自另一个容器的迭代器对，你可以拷贝其内容。你可以指定一个初始化列表来填充你的容器。对于 `map`，这意味着你需要指定嵌套的 `{...}`，因为每个元素必须初始化一个 `pair`——例如，`map<int,string>{ {2,"two"}, {3,"three s"} }`。从 C++23 开始，有一个 `from_range` 构造函数。

- 拷贝与移动：C(const&), C(&), C& op=(const C&), C& op=(&&)
  你可以将 `const T&` 作为参数传递给拷贝和移动构造函数及运算符。所有关联容器都实现了高效的 `swap(Cont& other)`。**注意：** 与序列容器相比，关联容器没有 `assign_range`。

- 析构函数：~Cont())
  所有容器都有用于移除包含元素的析构函数。如果你将原始指针封装到容器中，此规则不适用。

- 正向迭代：begin(), end(); 以及反向迭代：rbegin(), rend()
  你可以像使用顺序容器一样在这里迭代。有序容器保证在迭代时元素是经过排序的。`map` 变体的迭代器引用的是一个 `pair<K,T>`。

- 元素访问：T& operator[](Key), T& at(Key)
  只有 `map` 拥有这些方法。如果键在 `at` 中不存在，将抛出 `out_of_range` 异常。通过 `operator[](Key]`，你可以在 map 中进行读写。如果未找到键，它不会失败。例如，如果你写 `auto v = mymap[key]`，在必要时会在 `mymap[key]` 中创建一个新的（默认构造的）目标值。只有这样它会被返回给 `v`。这非常实用且重要。

- 大小：size(), empty(), max_size()
  通过 `size()`，你可以获取容器中元素的当前数量；如果数量为零，`empty()` 返回 true。通过 `max_size()`，你可以获取特定特定容器的最大大小。

- 修改：clear(), erase, insert, insert_or_assign, emplace 以及 insert_range
  这些方法的工作方式与顺序容器中的类似。在 `map` 中，元素由 `pair<K,T>` 组成，你可以通过 `insert` 和 `emplace` 插入它。只有 `map` 还拥有 `insert_or_assign`。从 C++23 开始提供了 `insert_range`。

- 搜索：count, find, lower_bound, upper_bound, equal_range, contains
  通过这些方法，你可以获取容器中键的信息。`count` 返回某个键出现的次数；`find` 返回指向找到的键（可能是多个中的一个）的迭代器，如果没有找到则返回 `end()`。`lower_bound` 和 `upper_bound` 的操作类似，但它们分别搜索第一个和最后一个键。如果未找到任何内容，它们会返回指向搜索键应被插入的位置的迭代器，这与 `find` 不同。`equal_range` 同时执行这两个操作，并返回一对包含所有匹配搜索键的迭代器（这与 `ranges` 库无关）。在非 `multiset` 变体中，逻辑上中间最多有一个元素，而 `multiset` 变体可能有多个。`contains` 从 C++20 开始可用。

- 传输：merge
  通过 `merge`，将元素从一个容器传输到另一个。在 `multiset` 变体中，所有元素都会被传输；而在非 `multiset` 变体中，只有目标容器不存在的元素会被传输，重复项留在源容器。

所有有序关联容器都以树结构存储其元素（见图 24.9 和图 24.10）。为了确保容器的效率，它始终保持平衡状态。这意味着在每次插入或删除操作中，节点都会被巧妙地重新排列，使得树的所有叶都被拉到（几乎）相同的高度。这种额外的管理工作是值得的，因为它保证了任何搜索在大多数 log n 步内都能找到元素或确认其不存在。无论你放入什么数据，无论是否存在频繁的插入和删除，这一点始终成立。

对于 `set`，存在以下主要用例：

### 24.7.3 "set" 去重

你想存储一个对象集合，并忽略重复项。由于 `set` 每个键只存储一次，因此在读取时所有重复项已经被去除了。

### 排序

当你交替进行存储、搜索、存储、搜索等操作时，对象集合应该保持排序状态。如果你先存储一个对象集合，然后在稍后的独立阶段想要进行快速搜索，那么 `vector` 通常更合适。如果没有两个明确分离的阶段，推荐使用 `set`。

如果你不需要这种顺序常数的保证，例如，你在两个独立的阶段访问 `set`——填充阶段和读取阶段——那么请使用 `vector`。

```cpp
#include <iostream>
#include <set>
#include <vector>
#include <string>

using namespace std;

template <typename T, typename Comp>
std::ostream& operator<<(std::ostream& os, const set<T, Comp>& s) {
    for (const auto& e : s) {
        os << e << " ";
    }
    return os;
}

int main() {
    set<int> s = {3, 1, 2, 3};
    cout << "Set elements: " << s << endl;
    return 0;
}
```

```cpp
map<int,string> mymap = {{2, "two"}, {3, "three"}};
auto v = mymap[4]; // 如果不存在则创建键 4 的默认值
```

