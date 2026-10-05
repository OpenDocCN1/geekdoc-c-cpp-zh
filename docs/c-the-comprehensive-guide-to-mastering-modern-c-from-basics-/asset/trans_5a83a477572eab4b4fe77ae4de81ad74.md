
# 访问

没有基于索引的访问。最好使用迭代器工作。直接访问元素仅适用于列表的末端：

- 直接访问元素
  `front()` 和 `back()` 分别提供指向列表第一个和最后一个元素的引用。确保列表不空；否则这种访问是无效的。
- 迭代器访问
  `begin()` 和 `c()` 返回一个指向第一个元素的双向迭代器，`end()` 和 `cend()` 指向列表的末尾——即最后一个元素之后。按照惯例，使用 `++it` 和 `--it` 对其进行递增和递减。你也可以使用 `<iterator>` 头文件的 `next(it)` 和 `prev(it)`。
- 反向遍历
  同样，通过 `rbegin()` 你可以获得一个指向最后一个元素的迭代器 `it`。如果你用 `++` 将其递增一次（是的，递增，不是递减），它将指向倒数第二个元素，依此类推。

注意，对于 `list`，移动迭代器若干位置的操作是昂代价的，这意味着它们需要 O(n) 时间。这些操作包括 `prev(it, n)`、`next(it, n)` 和 `advance(it, n)`，当迭代器之间的距离为 n 时，还有 `distance(it1, it2)`。

对于这一点——与 `vector` 和其他连续容器不同——当从容器中删除或插入元素时，迭代器仍然保持有效。

# 插入

`list` 的所有插入操作都是最优高效的，每个新元素的复杂度为 O(1)。与在 `vector` 头部和中间进行插入相比时，这一点尤为真实：

- 在末尾插入
  你可以使用 `push_back`、`emplace_back` 和 `append_range` 高效地向列表添加元素。
- 在头部插入
  这也适用于头部，使用 `push_front`、`emplace_front` 和 `prepend_range`。
- 在任意位置插入
  如果你在提供插入位置的同时还提供了一对源迭代器，`insert` 可以在任何地方插入单个元素或整个区域。从 C++23 开始，还有 `insert_range`。`emplace` 通过将调用参数转发给元素构造函数，在不拷贝的情况下在指定位置插入单个元素。

插入操作不会使引用该列表的其他迭代器失效。

# 删除

你可以使用 `clear()` 删除所有元素，并使用 `erase` 删除一个或多个元素，就像 `vector` 一样。

`list` 中的删除是最优快速的，每个删除元素的复杂度为 O(1)。这同样适用于头部或任意位置的删除。

当元素删除时，引用容器中其他位置的迭代器仍然有效。

# 特性：list 操作

你不能使用 `std::sort <algorithm>` 对列表排序，因为这需要随机访问迭代器。在这里使用 `list` 的 `sort` 方法。

同样也适用于某些无法通过自由函数处理 `list` 的算法，因为它们想要删除元素、将元素移动到末尾并随机交换。这些是 `remove`、`remove_if` 和 `unique`。`reverse` 和 `merge` 也作为 `list` 方法存在用于随机访问。以方法形式存在的特殊实现与 `<algorithm>` 中的对应版本一样高效。然而缺点是，这些方法始终对整个列表进行操作，因为它们不接收迭代器形式的范围标记参数。

然而，一个特别之处是 `splice` 方法：`list` 与所有其他容器（`forward_list` 除外）的本质允许列表合并为一。无论 `a` 和 `b` 中有多少元素，在执行 `a.splice(a.end(), b)` 之后，`b` 中的所有元素都在 `a` 中，而这只需要 O(1)。

```cpp
// https://godbolt.org/z/soGebb4M
#include <list>
#include <iostream>
using std::list; using std::cout; using std::ostream;

ostream& operator<<(ostream& os, const list<int>& data) {
    for (auto &de:data) os << de << ' ';
    return os << '\n';
}

int main() {
    list<int> numa = {1, 3, 5, 7, 9};
    list<int> numb = {2, 4, 6, 8};
    auto w = numa.begin();
    numa.insert(w, numb); // 在 O(1) 内插入
    cout << numa; // 输出: 1 2 3 4 5 6 7 8 9
    cout << numb; // 输出: (无)
    numa.sort(); // 作为方法排序，而不是来自 <algorithm>
    cout << numa; // 输出: 1 2 3 4 5 6 7 8 9
}
```

列表 24.41 "splice" 是 "list" 的特性，并能高效地连接两个列表。

注意我在列表 24.12 之后方框中对 `<<` 的注释。

通过 `splice` 的其他重载，你可以转移单个元素或一个范围的元素。效率是 O(n)。一个经常被忽略的方法是 `merge`。通过它，你可以将两个有序列表合并为一个。
