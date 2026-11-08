
像迭代器这样的情形，其底层类型并未由标准规定，而只是通过其属性来描述。这时你必须使用别名，因为你无法（以可移植的方式）写出具体类型。

在这里清晰地应用这些术语并不总是容易的。对于 map，术语“值”（value）是有歧义的，因为它常被这样使用：“它把一个键映射到一个值”。但 map 的 `value_type` 实际上是共同定义为 `pair<key_type,mapped_type>`。因此，在这种情况下，我更愿意使用“目标”（target）这个术语。在本书中，我力求使用以下清晰的术语：

- *值*，或 `value_type` 的元素
- `key_type` 的 *键*
- 对于 `mapped_type`，指 *目标类型* 或 *映射类型* 的 *目标*

| 类型别名 | 含义 | `vector<int>` | `set<int>` | `map<int, string>` |
|---|---|---|---|---|
| `value_type` | 容器中的元素 | `int` | `int` | `pair<const int, string>` |
| `key_type` | 元素的键部分 | – | `int` | `int` |
| `mapped_type` | 元素的映射部分 | – | – | `string` |
| `size_type` | 大小或索引 | `size_t` | `size_t` | `size_t` |
| `reference` | 对元素的引用 | `int&` | `int&` | `pair<const int, string>&` |
| `iterator` | *可修改*容器中的迭代器 | 是 | 是 | 是 |
| `const_iterator` | *不可修改*容器中的迭代器 | 是 | 是 | 是 |
| `reverse_iterator` | 反向迭代器 | 是 | 是 | 是 |

**表 24.3** 容器最重要的类型别名概览。

即使你放弃使用 `auto`，也可以使用这些别名编写对每种容器类型看起来都相同的代码，或创建自己的模板。

```cpp
// https://godbolt.org/z/c97rq3M7
#include <vector>
#include <map>
#include <iostream>
using std::cout; using std::ostream;

template<typename K, typename T>
ostream& operator<<(ostream& os, std::pair<const K,T> value) {
    return os << '[' << value.first << ':' << value.second << ']';
}
int main() {
    {
        using Cont = std::vector<int>;
        Cont const cont{ 1, 2, 3, 4, 5, 6 };
        Cont::size_type sz = cont.size();
        cout << "size=" << sz << " content= ";
        for(Cont::const_iterator it = cont.begin(); it != cont.end(); ++it)
            cout << *it << ' ';
        cout << '\n';
    }
    {
        using Cont = std::map<int,char>;
        Cont const cont{ {1,'a'}, {2,'b'}, {3,'c'}, {4,'d'}, {5,'e'}, {6,'f'} };
        Cont::size_type sz = cont.size();
        cout << "size=" << sz << " content= ";
        for(Cont::const_iterator it = cont.begin(); it != cont.end(); ++it)
            cout << *it << ' ';
        cout << '\n';
    }
}
```

**代码清单 24.11** 类型别名有时比具体类型更清晰。

这里我使用了容器提供的别名 `size_type` 和 `const_iterator`。在这个简单情形中，`auto` 本来也能工作，但这里是为了演示这些别名。

### 插曲：“pair”与“tuple”

如表 24.3 所示，有些容器在内部使用 `pair`。随着本章的深入，你会遇到若干也返回 `pair` 作为返回类型的方法。这只不过是把两个数据类型及其值捆绑在一起——本质上就是：

```cpp
// https://godbolt.org/z/xcrbVMljz
struct PairInDouble {
    int first;
    double second;
};
int main() {
    PairInDouble p{ 2, 7.123 };
}
```

我在这里专门针对 `int` 和 `double` 所做的，可以用 `std::pair` 作为适用于任意类型的模板类来实现。你可以用 `first` 访问第一个元素，用 `second` 访问第二个元素。

pair 对任意数量元素的推广就是 tuple。例如，你可以使用 `get<3>(t)` 访问 `t` 的第四个元素。

对于本章关于 pair 和 tuple 的讨论，这应该足够了。关于这两种数据类型的完整讨论可以在第 28 章第 28.1 节找到。

## 24.6 顺序容器类

让我们逐一介绍顺序容器类（见表 24.4）：

- **`array<ElementType,Size>`**
  这里存储固定数量的元素。添加和删除只能通过覆盖来完成。元素在内存中直接相邻存储。因此，array 既适合少量巨大的元素类型，也适合大量微小的元素类型，因为它几乎没有内存开销。

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_671_0.png)

  **图 24.2** “array”既不能增长也不能收缩，但它很紧凑。

- **`vector<ElementType>`**
  这个多面手会自动增长。你可以在任意位置插入，但只有在尾部插入才高效。

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_671_1.png)

  **图 24.3** “vector”的示意图。

  元素的读取可以向前、向后顺序进行，也可以通过索引随机进行。此外，vector 将其元素在内存中直接相邻存储，这使它既适用于少量大元素，也适用于大量小元素。使用最优时，它几乎没有内存开销；在非最优情况下，它仍然可以接受，因为它不会使内存碎片化。

- **`deque<ElementType>`**
  你可以轻松地向 vector 的末尾添加元素，但向开头添加就不那么容易，因为所有现有元素都必须向右移动一位。*双端队列* deque 适合在两端快速添加元素。缺点是，它不会将其元素直接相邻存储，但通常仍比 list 更紧凑。如果可能，优先使用 vector。

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_672_0.png)

  **图 24.4** “deque”可以在两端扩展，但元素在内存中不连续。

- **`list<ElementType>`**
  list 比 vector 更简单，非常适合在中间频繁插入。然而，元素在内存中并不连续，而是在内部链接起来。你无法使用索引访问。如果你想遍历范围，它很快。

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_672_1.png)

  **图 24.5** “list”可以向前和向后遍历。插入很容易。

- **`forward_list<ElementType>`**
  这种奇特的类型模仿 C 语言中链表的基本结构，因此需要极少的额外资源。然而，它的接口与所有其他容器略有不同。甚至插入的工作方式也有所不同。你只能向前迭代。list 和 forward_list 都是*拼接*的专家——也就是说，将某个列表中的一些连续元素或全部元素转移到另一个列表。

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_672_2.png)

  **图 24.6** “forward_list”的元素只知道它们的后继。

当你在编译时知道容器应容纳多少个元素时，就使用 `array`；另一方面，`vector` 具有动态大小；你可以向其中添加或删除元素。

表 24.5 列出了区分各基于序列的容器的主要属性。以下说明适用于用星号 * 标记的条目：

- **键类型**
  对于运算符 `[]` 和 `at`，你只能使用 `size_t`。`Key` 在这里并不是完全合适的术语，因为移动元素会改变键与容器元素的关联。不过，我在这里纳入这个属性，是为了与关联容器进行比较。

- **vector 每个元素的开销**
  在最优情况下，vector 除了其管理的元素本身之外，几乎没有任何额外的内存消耗。如果你事先知道将存储 1,000 个元素，可以用 `reserve(1000)` 将 vector 准备到这个确切大小，然后再添加元素。你将在时间和内存消耗方面获得最优性能。如果你不预先保留大小，vector 会略大于所需大小，并且在添加元素时不得不时不时分配新空间。不过，内部算法保证，平均而言，你花费的时间或内存至多是不预先保留时的两倍。

- **高效插入 `forward_list`**
  与所有其他容器不同，当你向 `forward_list` 插入时，并不是插入到你指示的位置，而是插入到其后一个元素的位置。为什么会这样，将在后面的示例中展示。因此，这个容器不同于任何其他容器（array 除外），它没有 `insert`，而是有 `insert_after`。这种不便源于希望每个元素占用尽可能少的内存。

- **list 和 `forward_list` 的拼接**
  与所有其他容器相比，这两个容器具有独特性质：你可以极快地合并两个相同类型的容器。将两个容器合为一个不会对这两个容器中包含的元素进行任何一次复制操作，而且需要更改的管理信息与列表中的元素数量无关。

- **内存布局**
  在许多场合，容器的元素需要紧密地打包在一起，才能以最优方式使用它们。例如，写入硬盘时，将所有要写入的数据作为一个大块传递给操作系统是有利的。其他 C 函数也难以处理复杂的 C++ 数据结构。它们需要一个内存起点和一个长度（你好，`span`！）。在所有容器中，只有 array 和 vector 以这种方式存储元素，从而使这类数据交换可以工作；其中 array 是唯一一个只能使用栈、不需要用 `new` 请求堆空间的容器。
