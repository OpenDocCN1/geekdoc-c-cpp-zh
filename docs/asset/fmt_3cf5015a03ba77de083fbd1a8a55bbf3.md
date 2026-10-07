
注意，`insert_iterator` 会在每次调用 `insert()` 后修改传递给 `insert()` 的位置提示，因此该位置就是刚刚插入的元素。

## 移动迭代器 (Move Iterators)

第 10 章讨论了移动语义，在已知知道对象在赋值或构造后会被销毁的情况下，可以用来防止不必要的拷贝。有一种名为 `move_iterator` 的迭代器适配器。`move_iterator` 的解引用操作会自动将值转换为右值引用，这意味着值可以移动到新目标，而没有拷贝的开销。在使用移动语义之前，你需要确保你的对象支持它。接面的 `MoveableClass` 支持移动语义。更多细节请参阅第 10 章。

```cpp
class MoveableClass {
public:
  MoveableClass() {
    cout << "Default constructor" << endl;
  }
  MoveableClass(const MoveableClass& src) {
    cout << "Copy constructor" << endl;
  }
  MoveableClass(MoveableClass&& src) noexcept {
    cout << "Move constructor" << endl;
  }
  MoveableClass& operator=(const MoveableClass& rhs) {
    cout << "Copy operator" << endl;
    return *this;
  }
  MoveableClass& operator=(MoveableClass&& rhs) noexcept {
    cout << "Move assignment operator" << endl;
    return *this;
  }
};
```

构造函数和赋值运算符在这里没有做任何有用的操作，除了打印一条消息以便查看调用了哪一个。现在你有了这个类，你可以如下定义一个 vector 并在其中存储几个 `MoveableClass` 实例：

```cpp
vector<MoveableClass> vecSource;
MoveableClass mc;
vecSource.push_back(mc);
vecSource.push_back(mc);
```

代码的第二行使用默认构造函数创建了一个 `MoveableClass` 实例。此第一次 `push_back()` 调用拷贝构造函数将 `mc` 拷贝到 vector 中。在此操作之后，vector 有了容纳一个元素的空间，即 `mc` 的第一个拷贝。注意，此讨论是基于[原文文本似乎重复/损坏]。

另一种选择是省略迭代器，并返回一个指向输入序列的迭代器，用于遍历输入序列中所有匹配的元素。这将要求你编写自己的迭代器类。

下一个任务是编写实现。`find_all()` 算法遍历输入序列中的所有元素，对每个元素调用谓词，并将匹配的元素存储在输出序列中。以下是实现代码：

```cpp
template <typename InputIterator, typename OutputIterator, typename Predicate>
OutputIterator find_all(InputIterator first, InputIterator last, OutputIterator dest, Predicate pred)
{
    while (first != last) {
        if (pred(*first)) {
            *dest = first;
            ++dest;
        }
        ++first;
    }
    return dest;
}
```

与 `copy_if()` 类似，该算法只会覆盖输出序列中的现有元素，因此请确保输出序列足够大以容结果，或者像下面的代码所示使用 `back_inserter` 作为迭代器适配器。找到匹配元素后，代码计算了找到元素数量，即 `matches` 中迭代器的数量。然后，它遍历结果并打印每个元素：

```cpp
vector<int> vec = { 3, 4, 5, 5, 6, 5, 8 };
vector<vector<int>::iterator> matches;
find_all(vec.begin(), vec.end(), back_inserter(matches),
    [](int x) { return x == 5; });
cout << "Found " << matches.size() << " matching elements: " << endl;
for (auto it : matches) {
    cout << *it << " at position " << (it - vec.begin()) << endl;
}
```

输出如下：

```
Found 3 matching elements:
5 at position 2
5 at position 4
5 at position 6
```

# 迭代器属性 (Iterator Traits)

某些实现需要关于迭代器的额外信息。例如，它们可能需要知道迭代器所引用的元素类型以便存储临时值，或者想知道迭代器是双向的还是随机访问的。

C++ 提供了一个名为 `iterator_traits` 的类模板，允许你查找这些信息。你使用迭代器类型实例化 `iterator_traits` 类模板，并访问五个类型定义之一：`value_type`、`difference_type`、`iterator_category`、`pointer` 和 `reference`。例如，该函数模板声明了一个类型 `Iterator` 类型迭代器所引用的类型的临时变量。注意在迭代器行前使用了 `typename` 关键字。每当你基于一个或多个模板参数访问类型时，必须指定 `typename`。在这种情况下，模板参数 `IteratorType` 被用于访问 `value_type`：

```cpp
#include <iterator>
template <typename IteratorType>
void TraitsTest(IteratorType it)
{
    typename std::iterator_traits<IteratorType>::value_type temp;
    temp = *it;
    cout << temp << endl;
}
```

可以使用以下代码对此函数进行测试：

```cpp
vector<int> v[ 5 ];
iteratorTraitsTest(begin(v));
```

通过此测试，`iteratorTraitsTest()` 函数中的变量 `temp` 将是 `int` 类型。输出如下：

5

在这个示例中，可以使用 `auto` 来简化代码，但这无法向你展示如何使用 `iterator_traits` 模板。

# 编写 STL 容器

C++ 标准包含了一系列要求，任何容器为了成为 STL 容器必须满足这些要求。

此外，如果你希望你的容器是顺序的（如 `vector`）、关联的（如 `map`）或无序关联的（如 `unordered_map`），它必须符合补充要求。

我在编写新容器时的建议是：先遵循通用规则编写基础容器（例如将其作为一个类模板），但不必过度担心 STL 合规性的特定细节。开发出基础实现后，你可以添加迭代器方法，使其能够与 STL 框架工作。本章将开发一个哈希映射。

# 基础哈希映射 (A Basic Hash Map)

C++11 增加了对无序关联容器（也称为哈希表）的支持。这些将在第16章中讨论。然而，Pre-C11并不包含哈希表。与 STL `map` 和 `set` 不同（后者在平均情况下提供对数级的插入、查找和删除时间），哈希表并不按顺序存储元素，而是通过哈希或映射将每个元素映射到特定的桶（bucket）。只要存储的元素数量不显著大于桶的数量，且哈希函数在桶之间均匀地分布元素，插入、删除和查找操作均可在常数时间内运行。

> 注意：本节假设你熟悉哈希数据结构。如果不熟悉，请参阅第16章（其中包含了哈希表的讨论），或附录 B 中列出的标准数据结构书籍。

本节实现了一个简单但功能齐全的 `hash_map`。与 `map` 类似，`hash_map` 存储键值对。事实上，它提供的操作几乎与 `map` 提供的相同，但具有不同的性能特征。

此 `hash_map` 实现使用了链哈希（也称为开放哈希），并且没有提供重哈希（rehashing）等高级功能。第16章解释了无序关联容器中链哈希的概念。

> 注意：建议使用标准的 C++ 无序关联容器（也称为哈希表），而不是自己实现。这些在第16章解释的无序关联容器被称为 `unordered_map`。

# 哈希函数

编写哈希映射时的第一个选择是如何处理函数。回想起句谚言：“良好的抽象让简单的情况变得简单，让困难的情况变得可能”，以下实现如下：

```cpp
template <typename T>
class hash {
    public:
        size_t operator()(const T& key) const;
};
```

该函数的实现非常复杂，因为它必须适用于任何类型的键。以下实现通过简单将键视为字节序列来计算一个整数大小的哈希值：

```cpp
template <typename T>
size_t hash<T>::operator()(const T& key) const
{
    size_t size = sizeof(key);
    size_t res = 0;
    for (size_t i = 0; i < size; ++i) {
        unsigned char b = *(unsigned char*))(&key + i);
        res += b;
    }
    return res;
}
```

遗憾的是，当对字符串使用这种哈希方法时，函数计算的是字符串的哈希，而不是实际文本的哈希。实际文本可能在堆上，字符串对象只包含长度指向文本的指针。即使引用相同的文本，指针也会不同。结果是具有相同文本的字符串对象将生成不同的哈希值。为字符串提供 `hash` 模板的特化是一个好主意，通常来说，对于任何动态分配内存的类也是如此。模板特化将在第11章中详细讨论：

```cpp
// 字符串的哈希特化
template <>
class hash<std::string>
{
public:
    size_t operator()(const std::string& key) const;
};
// 通过求加所有字符的 ASCII 值计算哈希。
size_t hash<std::string>::operator()(const std::string& key) const
{
    size_t sum = 0;
    for (size_t i = 0; i < key.size(); ++i) {
        sum += (unsigned char)key[i];
    }
    return sum;
}
```

如果你想使用其他类型或对象作为键，你应该为这些类型编写自己的哈希特化。

# 哈希 Map 接口

`hash_map` 支持三种基本操作：插入、删除和查找。当然，它还提供了一个构造函数。本文中讨论的实现略略了拷贝构造函数、移动构造函数，以及拷贝和移动赋值运算符。如果你想要拷贝、移动或赋值 `hash_map`，则这些操作是必要的。可下载的源码包含了这些构造函数和运算符的实现，以防你感兴趣。以下是 `hash_map` 类模板的公共部分：

```
template <typename Key, typename T, typename Compare = std::equal_to<Key>>
class hash_map {
public:
    using key_type = Key;
    using mapped_type = T;
    using value_type = std::pair<const Key, T>;
    virtual ~hash_map(); // 虚析构函数
    // 如果桶的数量非法，则抛出 invalid_argument 异常。
    explicit hash_map(const Compare& comp = Compare(), size_t n_buckets = 101, const Hash& hash = Hash());
    // 插入键/值对 x。
    void insert(const value_type& x);
    // 如果存在，则删除键为 k 的元素。
    void erase(const key_type& k);
    // find 返回键为 k 的元素的指针。
    // 如果元素不存在，则返回 nullptr。
    value_type* find(const key_type& k);
    const value_type* find(const key_type& k) const;
    // operator[] 查找键为 k 的元素，如果不存在则插入
    // 一个该键的元素。返回与该键对应的值的引用。
    T& operator[](const key_type& k);
private:
    // 此处未显示实现细节
};
```

如你所见，key 和 value 都是模板参数，就像 STL `map` 一样。`hash_map` 将 `pair<const Key, T>` 作为容器中的实际元素。`insert()`、`erase()`、`find()` 和 `operator()` 方法非常直观。然而，该接口的某些方面需要说明。

## 模板参数 Compare

与 `map`、`set` 以及其他容器一样，`hash_map` 允许客户端指定比较作为参数，并在构造函数中比较该类型的特定对象。与 `map` 和 `set` 不同，`hash_map` 不按键对元素排序，但必须比较键的相等性。它没有使用 `less` 作为默认值，而是使用 `equal_to`。比较对象用于检测尝试向容器中插入重复键的行为。

## 模板参数 Hash

你应该能够更改哈希函数，使其更适合你想要存储在 `hash_map` 中的元素类型。

因此，`hash_map` 模板接受四个模板参数：键的类型、值的类型、比较类型和哈希类型。

## 别名

`hash_map` 类模板定义三个类型别名：

```
using key_type = Key;
using mapped_type = T;
using value_type = pair<const Key, T>;
```

特别是是 `value_type`，用于引用更复杂的 `pair<Key, T>`。正如你将看到的，标准也要求 STL 容器必须包含这些别名。

## 实现

在确定了 `hash_map` 接口之后，你需要选择实现方法。基本的哈希表结构通常由固定数量的桶（buckets）组成，每个桶可以存储一个或多个元素。桶应该根据桶 ID（键的哈希结果）在常数时间内访问。因此，`vector` 是存放桶最合适的容器。每个桶必须存储一个元素列表，可以使用 STL `list` 作为桶的类型。最终结构是 `pair<const Key, T>` 列表的 `vector`。以下是 `hash_map` 类的私有成员：

```
private:
using ListType = std::list<value_type>;
std::vector<ListType> mbuckets;
size_t mSize;
Compare mComp;
Hash mHash;
```

如果没有类型别名，声明 `mbuckets` 将像这样：
`std::vector<std::list<pair<const Key, T>>> mbuckets;`

`mComp` 和 `mHash` 分别存储比较和哈希对象，`mSize` 存储容器中的元素数量。

## 构造函数

构造函数初始化所有桶并调整 `mbuckets` 的大小。遗憾的是语法有些复杂，请参考第 1 章。

```cpp
// 调整桶的大小。
template <typename Key, typename T, Compare, typename Hash>
hash_map<Key, T, Compare, Hash>
hash_map(
  const Compare& comp, size_t numBuckets, const Hash& hash)
  : mSize(0), mComp(comp), mHash(hash)
{
  if (numBuckets == 0) {
    throw std::invalid_argument("Number of buckets must be positive");
  }
  mbuckets.resize(numBuckets);
}
```

查找操作至少一个桶。`find` 方法需要查找键为 k 的元素。因此，有一个私有的辅助方法是有帮助的。`findElement` 首先计算哈希值并确定确定桶。接口的实现需要说明：

```cpp
template <typename Key, typename T, Compare, typename Hash>
hash_map<Key, T, Compare, Hash>::findElement(const key_type& k, size_t& bucket)
{
  bucket = mHash(k) % mbuckets.size();
