

for (const auto& i : l)
    std::cout << i << std::endl;

STL 包含简单和复杂的算法。它们都包含（通常深藏其中）与上述示例本质上等价的循环。

### 4.1.2.3 操作

<iterator> 库提供两个基本操作：advance 和 distance。操作 advance(it, n) 将迭代器 it 递增 n 次。这可能看起来像是表达 it+n 的一种麻烦方式，但存在两个根本区别：第二种表示法不会改变迭代器 it（这不一定是劣势），并且它仅适用于 RandomAccessIterator。函数 advance 可用于任何类型的迭代器。从这个意义上说，advance 就像 += 的一种实现，也适用于只能逐个步进的迭代器。

为了高效，该函数在内部针对不同的迭代器类别进行分发。我们已在 3.10.2 节中看到如何使用概念来实现这一点。现在我们演示以前是如何做到的：

### 清单 4-1：advance 中的函数分发

点击此处查看代码图像

```
template <typename Iter, typename Distance>
inline void advance_aux(Iter& i, Distance n,
                        input_iterator_tag)
{
    assert(n >= 0);
    for (; n > 0; --n)
        ++i;
}

template <typename Iter, typename Distance>
inline void advance_aux(Iter& i, Distance n,
                        bidirectional_iterator_tag)
{
    if (n >= 0)
        for (; n > 0; --n) ++i;
    else
        for (; n < 0; ++n) --i;
}
```

```
template <typename Iter, typename Distance>
inline void advance_aux(Iter& i, Distance n,
                        random_access_iterator_tag)
{
    i += n;
}
```

```
template <typename Iter, typename Distance>
inline void advance(Iter& i, Distance n)
{
    using cat = typename
    iterator_traits<Iter>::iterator_category;
    advance_aux(i, n, cat());
}
```

当函数 advance 用迭代器类型实例化时，该迭代器的类别由类型特性（§5.2.1）确定。该标签类型的对象决定调用辅助函数 advance_aux 的哪个重载。因此，当 Iterator 是随机访问迭代器时，advance 的运行时间为常数，否则为线性时间。双向迭代器和随机访问迭代器允许负距离。这种基于标签的函数选择也称为标签分发（Tag Dispatching）。

**C++17** 请注意，对于 advance_aux 的相应最后参数，仅指定了类型而未给出参数名。否则，编译器在 pedantic 模式下会发出警告，指出该参数未被使用。要抑制此警告，我们可以在 C++17 中使用属性 [[maybe_unused]] 声明这是有意为之，例如：

点击此处查看代码图像

```
template <typename Iter, typename Distance>
inline void advance_aux(Iter& i, Distance n,
                        input_iterator_tag tag
                        [[maybe_unused]]);
```

现代编译器足够智能，能够意识到 advance_aux 每个重载中的第三个参数未被使用，且标签类型是空类。因此，参数传递和标签类型对象的构造被优化掉了。因此，额外的函数层和标签分发不会造成任何运行时开销。例如，在 vector 迭代器上调用 advance 归结为仅生成 i += n 的代码。

`advance` 的对应操作是 `distance`：

```
int i = distance(it1, it2);
```

它计算两个迭代器之间的距离，即第一个迭代器必须递增多少次才能等于第二个迭代器。不言而喻，实现也通过标签（或概念）进行分发，因此随机访问迭代器的开销为常数，否则为线性。

## 4.1.3 容器

标准库中的容器涵盖了广泛的重要数据结构，易于使用，且效率相当高。在编写自己的容器之前，尝试标准容器绝对是值得的。

### 4.1.3.1 向量

`std::vector` 是最简单的标准容器，也是连续存储数据最高效的容器，类似于 C 数组。而大小在一定范围内的 C 数组存储在栈上，`vector` 始终位于堆上。向量提供下标运算符，可以使用数组风格的算法：

点击此处查看代码图像

```
std::vector<int> v = {3, 4, 7, 9};
for (int i = 0; i < v.size(); ++i)
    v[i] *= 2;
```

或者，我们可以使用迭代器：直接使用，或在基于范围的 for 循环中隐式使用：

```
for (auto& x : v)
    x *= 2;
```

不同的遍历形式效率应当相似。向量可以通过在末尾添加新条目来扩大：

```
std::vector<int> v;
for (int i = 0; i < 100; ++i)
    v.push_back(my_random());
```

其中 `my_random()` 返回随机数，如同 4.2.2 节中的生成器一样。STL `vector` 通常会预留额外空间，如图 4-2 所示，以加速 push_back。

![](img/5682e787fc967e93d7e33e8bac5f58a0_344_0.png)

### 图 4-2：vector 的内存布局

因此，追加条目可以：

- 要么非常快，只需填充已预留的空间，或
- 要么相当慢，当必须分配更多内存并复制所有数据（或至少逐元素移动）时。

可用空间由成员函数 capacity 提供。当 vector 数据被扩大时，额外空间的量通常与 vector 大小成正比，因此 push_back 的渐近时间为对数时间。典型实现会在 vector 大小加倍时执行一次或两次内存分配（即，每次重新分配时从 s 扩大到 2s 或 sqrt(2)s）。图 4-3 说明了这一点：第一张图是一个完全填满的 vector，添加新条目需要新分配，如第二张图所示。之后，我们可以继续添加条目，直到额外空间也被填满，如第三张图所示。然后必须分配新内存并复制所有条目（或逐元素移动），如第四张图所示；只有之后才能添加新条目。因此，该 vector 的所有迭代器可能都会失效。为保险起见，你不应该使用在插入或删除条目之前创建的 vector 迭代器。

![](img/5682e787fc967e93d7e33e8bac5f58a0_345_0.png)

### 图 4-3：追加 vector 条目

方法 `resize(n)` 将 vector 缩小或扩大到大小 `n`。新条目会被默认构造（或对于内置类型设置为 `0`）。使用 `resize` 缩小 vector 不会释放内存。这可以在 C++11 中使用 `shrink_to_fit` 完成，它将容量减小到 vector 的实际大小。

=> c++11/vector_usage.cpp

C++11 以下简单程序说明了如何使用 C++11 特性设置和修改 `vector`：

点击此处查看代码图像

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main ()
{
    using namespace std;
    vector<int> v = {3, 4, 7, 9};
    auto it= find (v.begin(), v.end(), 4);
    cout << "After " << it << " comes " << *(it+1) << '\n';
    auto it2= v.insert(it, 5); // insert value 5 at pos. 2
    v.erase(v.begin()); // delete entry at pos. 1
    cout << "Size = " << v.size() << ", capacity = "
    << v.capacity() << '\n';
    v.shrink_to_fit(); // drop extra entries
    v.push_back(7);
    for (auto i : v)
    cout << i << ",";
    cout << '\n';
}
```

附录 A.7.1 显示了如何在旧的 C++03 中实现相同的功能。

可以在任意位置添加和删除条目，但这些操作代价高昂，因为后面的所有条目都必须移动。然而，它并没有我们许多人想象的那么昂贵。

C++11 vector 中的其他新方法是 emplace 和 emplace_back，例如：

点击此处查看代码图像

```
vector<matrix> v;
v.push_back(matrix(3, 7)); // add 3 by 7 matrix, built outside
v.emplace_back(7, 9); // add 7 by 9 matrix, built in place
```

使用 push_back 时，我们必须先构造一个对象（如示例中的 3 x 7 矩阵），然后将其复制或移动到 vector 的新条目中。相比之下，emplace_back 直接在 vector 的新条目中构造一个新对象（这里是 7 x 9 矩阵）。这节省了复制或移动操作，并可能节省一些内存分配/释放。类似的方法也在其他容器中引入。

C++11 如果 vector 的大小在编译时已知且之后不再更改，我们可以改用 C++11 容器 array。它位于栈上，因此效率更高（除了移动和交换等浅拷贝操作）。

### 4.1.3.2 双端队列

