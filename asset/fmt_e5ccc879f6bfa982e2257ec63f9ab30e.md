
| `forward_list<T>` | 单向链表 |
| `deque<T>` | 双端队列 |
| `map<K,V>` | 关联数组 ($12.5) |
| `multimap<K,V>` | 一个键可以对应多个值的 map |
| `unordered_map<K,V>` | 使用哈希查找的 map ($12.6) |
| `unordered_multimap<K,V>` | 使用哈希查找的重映射 map |
| `set<T>` | 集合（一个只有键没有值的 map） |
| `multiset<T>` | 元素可以出现多次的集合 |
| `unordered_set<T>` | 使用哈希查找的集合 |
| `unordered_multiset<T>` | 使用哈希查找的重值集合 |

无序容器（`unordered containers`）针对使用值（通常是字符串）的查找进行了优化；换句话说，它们是哈希。

容器定义在 `std` 命名空间中，并在头文件 `<vector>`、`<list>`、`<map>` 等中 ($9.3)。此外，标准库提供了容器适配器 `queue<T>`、`stack<T>` 和 `priority_queue<T>`。如果需要，请查询它们。标准库还提供了专门的类容器类型，例如 `array<T,N>` ($15.3) 和 `bitset<N>` ($15.2)。

标准容器及其基本操作在符号表示上被设计得是简单的。此外，各种类型容器的操作含义是等价的。基本操作适用于其有意义且可以实现的容器：

| 操作 | 说明 |
|------|---|
| `p=c.begin()` | p 指向 c 的第一个元素；对于常量迭代器使用 `cbegin()` |
| `p=c.end()` | p 指向 c 最后一个元素之后的位置；对于常量迭代器使用 `cend()` |
| `k=c.size()` | k 是 c 中元素的数量 |
| `c.empty()` | c 是否为空？ |
| `k=c.capacity()` | k 是 c 在不进行新分配的情况下可以容纳的元素数量 |
| `c.reserve(k)` | 将容量增加到 k；如果 $k<c.capacity()$，则 `reserve(k)` 不起作用 |
| `c.resize(k)` | 将大小调整为 k |
| `c.push_back(k)` | 在 c 尾部添加元素 |
| `c.emplace_back(k)` | 在 c 尾部就地构造元素 |

- [17] `map` 通常实现为红黑树；§12.5。
- [18] `unordered_map` 是哈希表；§12.6。
- [19] 按引用传递容器并按值返回容器；§12.2。
- [20] 对于容器，对大小使用 0-初始化语法，对元素序列使用 0-初始化语法；§5.2.3, §12.2。
- [21] 优先使用紧凑且连续的数据结构；§12.3。
- [22] `list` 的遍历开销相对较大；§12.3。
- [23] 如果需要遍历数据，请使用无序容器（例如 `map` 和 `set`）；§12.6。
- [24] 如果需要按顺序遍历元素，请使用有序容器（例如 `map` 和 `set`）；§12.5。
- [25] 对于没有自然顺序（即没有合理的 `<`）的元素类型，请使用无序容器（例如 `unordered_map`）；§12.5。
- [26] 当你需要元素指针在容器大小变化时保持稳定时，请使用关联容器（例如 `map` 和 `list`）；§12.8。
- [27] 通过实验检查你是否有一个可接受的哈希函数；§12.6。
- [28] 通过异或运算符 (`*`) 组合元素的哈希函数而得到的哈希函数通常很好；§12.6。
- [29] 熟悉标准库容器的大小，并优先使用它们而非手工的数据结构；§12.8。
- [30] 如果你的应用程序受到与内存相关的性能问题影响，尽量减少 store 使用并/或考虑使用专门的分配器；§12.7。

# 13

# 算法

> 不要增加不必要的实体。

威廉·奥卡

- 引言
- 迭代器的使用
- 迭代器类型
  - 流迭代器
- 谓词的使用
- 算法概览
- 并行算法
- 建议

## 13.1 引言

数据结构（如 `list` 或 `vector`）本身并不很有用。要使用它们，我们需要基本的访问操作，如添加和删除元素（`list` 和 `vector` 提供了这些操作）。此外，我们很少仅仅将对象放在容器中。我们会对其进行排序、打印、提取子集、删除元素、搜索对象等。因此，标准库在提供最常用类型的同时，还提供了容器最常用的算法。例如，我们可以高效地对 `Entry` 的 `vector` 进行排序，并将每个唯一元素的拷贝放在 `list` 中：

点击此处查看代码图像

```cpp
void f(vector<Entry>& vec)
sort(vec.begin(),vec.end());
unique_copy(vec.begin(),vec.end(),lst.begin());

if use < order
// 不要拷贝相邻的相等元素
}
```

对于这项工作，`Entry` 必须定义小于 (`<`) 和等于 (`==`)。例如：

点击此处查看代码图像

```cpp
bool operator=(const Entry& x, const Entry& y) // 小于
{
    return x.name==y.name; // 按名称对 Entries 排序
}
```

标准算法是用元素的（半开闭的）序列来表示的。序列由一对迭代器表示，指定第一个元素和最后一个元素之后的元素：

迭代器: `begin()`

元素: 

![](img/0bd2e25eba2737c3c5daca16fad1b65b_191_0.png)

在示例中，`sort()` 排序由迭代器对 `vec.begin()` 和 `vec.end()` 定义的序列，这正好是 `vector` 的所有元素。对于写入（输出），我们只需要指定要写入的第一个元素。如果写入了多个元素，随后的元素将被覆盖。为了避免错误，`lst` 的元素数量至少要与 `vec` 中唯一值的数量一样。

遗憾的是，标准库没有提供支持向容器进行范围检查写入的抽象。然而，我们可以定义：

点击此处查看代码图像

```cpp
template<typename C>
class Checked_iter {
public:
    using value_type = typename C::value_type;
    using difference_type = int;

    Checked_iter() { throw MissingConstructor(); } // 前向迭代器需要默认构造函数
    Checked_iter(const C& cc) : p(&cc) { pc(&cc) }
    Checked_iter(C::iterator pp) : p(pp) { pc(pp) }

    Checked_iter&operator++() { check_end(); ++p; return *this; }
    Checked_iter&operator++(int) { check_end(); auto t = *this; ++*p; return t; }
    value_type&operator*() const { check_end(); return *p; }

    bool operator==(const Checked_iter& a) const { return p==a.p; }
    bool operator!=(const Checked_iter& a) const { return p!=a.p; }
private:
    void check_end() const { if (p == p->end()) throw Overflow(); }
    C* pc; // 默认初始化为 nullptr
    typename C::iterator p = p->begin();
};
```

显然，这并不是标准库级别的质量，但它展示了。

点击此处查看代码图像

```cpp
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的，但它展示了
// 标准库级别的
```

## 13.2 迭代器的使用

对于容器，可以获取几个指向它的迭代器；`begin()` 和 `end()` 是最好的。此外，许多算法会返回迭代器。例如，标准算法 `find` 在序列中查找值并返回指向找到的元素的迭代器：

点击此处查看代码图像

```cpp
bool has_c(const string& s)
if(p!=s.end())
  return true;
else
  return false;
```

像标准算法一样，`find` 返回以指示“未找到”。等效的短短 `has_c` 定义为：

点击此处查看代码图像

```cpp
bool has_c(const string& s, char c)
{
  return find(s,c)==s.end();
}
```

更有趣的练习是查找字符串中所有字符的位置。我们可以使用 `vector<char>` 返回这些出现的情况。返回 `vector` 是高效的，因为 `vector` 提供了语义（6.2.1）。假设我们想要修改位置，我们传递一个非常字符串：

点击此处查看代码图像

```cpp
vector<char> find_all(string& s, char c) // 在 s 中查找所有 c c
{
  vector<char> res;
  for (auto p=s.begin(); p!=s.end(); ++p)
    if (*p=='c')
      res.push_back(*p);
  return res;
}
```

我们使用传统的循环遍历字符串，通过 `++` 将迭代器 `p` 向移动一个元素，并通过解引用运算符 查看元素。我们可以这样测试 `find_all()`：

点击此处查看代码图像

```cpp
void test()
{
  string m("Mary had a little lamb");
  for (auto p : find_all(m, a))
    if (*p=='a')
      cerr << "a bug in!";
}
```

对 `find_all()` 的调用可以这样图形化表示：

```cpp
find_all(m,'a');
```

| m:| M a r y | h a d | a | l i t t l e | l a m b | \00 |

迭代器和标准算法在每一个有意义的标准容器上工作都是等效。因此，我们可以推广 `find_all()`：

点击此处查看代码

```cpp
template<typename C, typename V>
vector<typename C::iterator> find_all(const C& c, V v)
{
    vector<typename C::iterator> res;
    for (auto p = c.begin();p!=c.end(); ++p)
        if (*p==v)
            res.push_back(p);
    return res;
}
```

它查找 `c` 中所有 `v` 的出现位置。

使用 `typename` 是为了告诉编译器 `C` 的迭代器（`iterator`）被认为是一个类型，而不是某个值类型（例如整数 7）。

或者，我们可以返回一个指向元素的普通指针版本：

点击此处查看代码

```cpp
template<typename C, typename V>
auto find_all(const C& c, V v)
{
    range_value_t<C>* res;
    for (auto& x : c)
        if (x==v)
            res.push_back(&x);
    return res;
}
```

它查找 `c` 中所有 `v` 的出现位置。

顺便，我还通过使用 range-for 循环和标准库的 `range_value_t` (§16:4) 来命名元素类型简化了这一点。`range_value_t` 的简化版本可以这样定义：

点击此处查看代码

```cpp
template<typename T>
using range_value_type_t = T::value_type;
```

使用 `find_all()` 的任一版本，我们可以编写：

点击此处查看代码

```cpp
void test()
{
    string m = "Mary had a little lamb";
    for (auto p : find_all(m, 'a'))
        if (*p == "a")
            cerr << "string bug";
}
```

`p` 是一个 `string::iterator`

-   `list<int> id {1, 2, 3, 1, -11, 2}`;

for (auto p : find_all(id,1))

    if (*p!=1)

        cerr << "list bug";

`p` 是一个 `list<int>::iterator`

```cpp
vector<string> vs = {"red"};
```

`p` 是一个 `vector<string>::iterator`

```cpp
cerr << "vector bug\n";

for (auto p : find_all(vs))
```

迭代器被用于分离算法和容器。算法通过迭代器对其数据进行操作，并且对存储元素的容器一无所知。相反，容器对操作其元素的算法也一无所知；它所做的只是根据请求提供迭代器（例如 `begin()` 和 `end()`）。这种存储与算法分离的模型提供了非常通用的软件设计。(img/0bd2e5eba273c5d16fad65b195_0)

## 13.3 迭代器类型

迭代器究竟是什么？任何特定的迭代器都是某种类型的对象。然而，有许多迭代器类型——迭代器需要持有为特定容器工作的信息。这些迭代器类型可以与它们所服务的容器一样不同。例如，`vector` 的迭代器可以是一个普通指针，因为指针是引用`vector` 元素的合理方式：img/0bd2e5eba273c5d16fad65b195_2)

使用这样的迭代器允许进行范围检查。`list` 迭代器必须比指向元素的简单指针更复杂，因为通常情况下，`list` 并不知道下一个元素在哪里。因此，`list` 迭代器可能是一个指针：`iterator`:

| list: | link | link | ... |
| --- | --- | --- | --- |
| elements: | P | i | t |

所有迭代器的共同点是它们的语义以及对操作的命名。例如，将 `++` 应用于任何迭代器都指向下一个元素。同样，`*` 产生迭代器指向的元素。事实上，迭代器（*Iterator*）是一个通用的概念 (§8.2)，并且不同类型的迭代器作为标准库概念可用，例如正向迭代器（`forward_iterator`）和随机访问迭代器（`random_access_iterator`）（§14.5）。此外，用户需要知道特定迭代器的类型；每个容器“知道”其迭代器类型并以传统的名称 `iterator` 和 `const_iterator` 提供它们。例如，`list<Entry>::iterator` 是 `list<Entry>` 的通用迭代器类型。在某些情况下，迭代器不是成员类型，因此标准库提供了 `iterator_t<X>` 在 X 的迭代器定义的地方工作。

### 13.3.1 流迭代器

迭代器是处理容器中元素的通用且用的概念。然而，容器并不是查找元素序列的唯一地方。例如，输入流产生值序列，我们将值序列写入输出流。因此，迭代器的概念可以很好地应用于输入和输出。

要制作 `ostream_iterator`，我们需要指定使用哪种流以及写入它的对象类型。例如：点击此处查看代码

```cpp
ostream_iterator<string> oo (cout); // 将字符串写入 cout
```

使用 `++oo` 的效果是将赋值的值写入 `cout`。例如：点击此处查看代码

```cpp
int main() {
  oo = "Hello, ";
  ++oo;
  oo = "world!\n";
  cout << "Hello, ";
}
```

这是将规范消息写入标准输出的另一种方法。`++oo` 是通过指针模拟写入。通过这种方式，我们可以在流上使用算法。例如：点击此处查看代码

```cpp
vector<string> v("Hello", "World!\n"); copy(v, oo);
```

同样，`istream_iterator` 允许我们把输入流视为只读容器。再次，我们必须指定使用的流和期望的值类型：点击此处查看代码

```cpp
istream_iterator<string> ii(cin);
```

输入迭代器成对使用以表示序列，我们必须提供一个 `istream_iterator` 来指示输入的结束。这个默认值是 `istream_iterator`：

```cpp
istream_iterator<string> eos();
```

通常，`istream_iterator` 和 `ostream_iterator` 不直接使用，它们作为算法的参数提供。例如，我们可以写一个简单的程序来读取文件、排序单词、去重并将结果写入另一个文件：点击此处查看代码
