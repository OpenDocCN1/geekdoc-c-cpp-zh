
这段代码还表明非成员函数（如 `std::cbegin()` 和 `std::cend()`）正按预期工作。

# 关于分配器的说明

正如本章早些提到的，STL 容器允许你指定自定义的内存分配器。一个“良好公民”`hash_map` 实现也应该这样做。然而，这些细节被省略了，因为它们模糊了此实现的要点。

# 关于可逆容器的说明

如果你的容器提供了双向或随机访问迭代器，则它被认为是*可逆的*。可逆容器应该提供两个额外的类型别名：

| 类型名称 | 描述 |
| --- | --- |
| `reverse_iterator` | 用于反序遍历容器元素的类型。 |
| `const_reverse_iterator` | `reverse_iterator` 的一个版本，用于反序遍历容器中的 const 元素。 |

此外，容器应该提供 `begin()` 和 `rend()`，它们与 `begin()` 和 `end()` 对称；并且应该提供 `cbegin()` 和 `crend()`，它们与 `cbegin()` 和 `cend()` 对称。通常的实现使用了本章早些描述的 `reverse_iterator` 适配器。这些被留给读者作为练习。

# 使 hash_map 变为关联容器

除了所示的基础容器要求外，你还可以让你的容器符合关联容器、无序容器或顺序容器的额外要求。此示例使 `hash_map` 变为一个关联容器，因此它应该符合以下类型别名和方法。

## 关联容器类型别名要求

| 类型名称 | 描述 |
| --- | --- |
| `key_type` | 实例化容器的键。 |
| `key_compare` | 实例化容器的比较类或函数指针。 |
| `value_compare` | 用于比较两个 `value_type` 元素的类。 |

此示例实现还显示了名为 `mapped_type` 的别类型，因为这是 `map` 的做法。`value_compare` 不是作为类型别名实现的，而是作为嵌套定义。另一种，它可以是 `hash_map` 的一个 `friend` 类，但这遵循标准的定义。`value_compare` 类的目的是对两个元素的键调用比较函数：

```cpp
template <typename Key, typename T, typename Compare = std::equal_to<Key>>
using Hash = hash<Key>;

class hash_map {
  public:
    using key_type = Key;
```

# 扩展 STL

```cpp
using mapped_type = T;
using value_type = std::pair<const Key, T>;
using key_compare = Compare;
using reference = std::pair<const Key, T>&;
using const_reference = std::pair<const Key, T> const;
using size_type = size_t;
using difference_type = ptrdiff_t;
using hash_map_type = hash_map<Key, T, Compare, Hash>;
using iterator = hash_map_iterator<hash_map_type>;
using const_iterator = const_hash_map_iterator<hash_map_type>;

// 关联容器所需的类定义
class value_compare : public std::binary_function<value_type, value_type, bool> {
    public:
        bool operator()(const value_type& x, const value_type& y) const {
            return comp(x.first, y.first);
        }
    protected:
        Compare comp;
        value_compare(Compare c) : comp(c) { }
};
```

## 关联容器方法

标准对关联容器规定了一些额外的方法要求：

| 方法 | 描述 | 最坏复杂度 |
| --- | --- | --- |
| `insert(const key_type&, const value_type&, iterator hint)` | 在 hint 之前插入元素。 | 除 hint 外为对数级 |
| `insert(const initializer_list<value_type>&)` | 从初始化列表插入元素。 | 对数级 |
| `insert(Iterator start, Iterator end)` | 插入范围内的元素。 | 线性 |
| `erase(const key_type&)` | 删除指定键的元素。 | 对数级 |
| `erase(iterator position)` | 删除指定位置的元素。 | 对数级 |
| `erase(Iterator start, Iterator end)` | 删除范围内的元素。 | 线性 |
| `clear()` | 删除所有元素。 | 线性 |

```cpp
// 关联容器所需的类定义
class value_compare {
    public:
    std::binary_function<value_type, value_type, bool>
    {
        bool operator()(const value_type& x, const value_type& y) const
        {
            return comp(x.first, y.first);
        }
    }

protected:
    Compare comp;
    value_compare(Compare c) : comp(c) { }
};

// 迭代器需要访问哈希表的所有成员
friend class hash_map_iterator<hash_map_type>;
friend class const_hash_map_iterator<hash_map_type>;

virtual ~hash_map(); // 虚析函数
// 如果桶的数量非法，抛出无效参数异常。
explicit hash_map(const Compare& comp = Compare(),
    size_type numBuck = 101, const Hash& hash = Hash());

// 如果桶的数量非法，抛出无效参数异常。
template <typename InputIterator>
hash_map(InputIterator first, InputIterator last,
    const Compare& comp = Compare(),
    size_type numBuckets = 101, const Hash& hash = Hash());

// 初始化列表构造函数
// 如果初始化列表非法，抛出无效参数异常。
explicit hash_map(std::initializer_list<value_type> il,
    const Compare& comp = Compare(), size_type numBuckets = 101,
    const Hash& hash = Hash());

// 初始化列表赋值运算符
hash_map_type& operator=(std::initializer_list<value_type> il);

// 迭代器方法
iterator begin();
iterator end();
const_iterator begin() const;
const_iterator end() const;
const_iterator cbegin() const;
const_iterator cend() const;

// 尺寸方法
bool empty() const;
size_type size() const;
size_type max_size() const;

// 元素插入方法
T& operator[](const key_type& x);
std::pair<value_type, bool> insert(const value_type& x);

iterator insert(iterator position, const value_type& x);
template <typename InputIterator>
void insert(InputIterator first, InputIterator last);
void insert(std::initializer_list<value_type> il);

// 原地插入方法
std::pair<iterator, bool> emplace(value_type&& x);
iterator emplace_hint(iterator hint, value_type&& x);

// 元素删除方法
size_type erase(const key_type& x);
iterator erase(iterator position);
iterator erase(iterator first, iterator last);

// 其他修改类工具
void swap(hash_map_type& hashIn);
void clear() noexcept;

// 符合 STL 标准的方法
key_compare key_comp() const;
value_compare value_comp() const;

// 查找方法
iterator find(const key_type& x);
const_iterator find(const key_type& x) const;
std::pair<iterator, iterator> equal_range(const key_type& x);
std::pair<const_iterator, const_iterator> equal_range(const key_type& x) const;
size_type count(const key_type& x) const;

private:
    using ListType = std::list<value_type>;
    typename ListType::iterator findElement(const key_type& x,
        size_type bucket&);

    std::vector<ListType> mbuckets;
    size_type mSize;
    Compare mComp;
    Hash mHash;
```

### hash_map 构造函数

构造函数的实现如前所示。第二个构造函数是一个方法模板，它可以接受来自任何容器的迭代器，而不仅仅是其他 hash_map。如果不是方法模板，它将需要显式指定 `InputIterator` 类型，从而限制为来自 hash_map 的迭代器。尽管语法看起来复杂，但其实现非常简单：它初始化所有数据成员，然后调用 `insert()` 来实际插入指定范围内的所有元素。

```cpp
// 调用 insert() 来实际插入元素。
template <typename Key, typename T, typename Compare, typename Hash>
template <typename InputIterator>
hash_map<Key, T, Compare, Hash>::hash_map(
InputIterator first, InputIterator last, const Compare& comp,
size_type numBuckets, const Hash& hash
: mSize(0), mComp(comp), mHash(hash)
{
    if (numBuckets == 0)
        throw std::invalid_argument("桶的数量必须大于零");
    
    mBuckets.resize(numBuckets);
    insert(first, last);
}
```

### hash_map 初始化列表构造函数

初始化列表将在第10章中讨论。以下是接受初始化列表的 hash_map 构造函数，它与接受迭代器范围的构造函数的实现非常相似：

```cpp
template <typename Key, typename Compare, typename Hash>
hash_map<Key, T, Compare, Hash>::hash_map(std::initializer_list<value_type> il,
    const Compare& comp, size_type numBuckets, const Hash& hash)
    : mSize(0), mComp(comp), mHash(hash)
{
    if (numBuckets == 0)
        throw std::invalid_argument("桶的数量必须大于零");
    
    mBuckets.resize(numBuckets);
    insert(il.begin(), il.end());
}
```

### hash_map 初始化列表赋值

运算符也可以接受初始化列表。以下是接受初始化列表的赋值运算符：

```cpp
template <typename Key, typename T, typename Compare, typename Hash>
hash_map<Key, T, Compare, Hash>&
    operator=(std::initializer_list<value_type> il)
{
    // ... 实现 ...
}
```

### hash_map 插入操作

`insert()` 的简单形式返回一个对，指示该项目是新创建：

```cpp
template <typename Key, typename T, typename Compare, typename Hash>
std::pair<iterator, bool> hash_map<Key, T, Compare, Hash>::insert(iterator position, const value_type& x)
{
    // ... 实现 ...
}
```

`insert()` 的第三种形式是一个方法模板，这比直接调用 `insert()` 好得多，因为可以使用来自任何容器的迭代器来插入元素：

```cpp
template <typename Key, typename T, typename Compare, typename Hash>
template <typename InputIterator>
void hash_map<Key, T, Compare, Hash>::insert(InputIterator first, InputIterator last)
{
    // ... 实现 ...
}
```

`insert()` 的最后一种形式接受初始化列表：

```cpp
template <typename Key, typename T, typename Compare, typename Hash>
void hash_map<Key, T, Compare, Hash>::insert(std::initializer_list<value_type> il)
{
    // ... 实现 ...
}
```

### 扩展 STL

```cpp
mSize++;
```

```cpp
}
return std::make_pair(
hash_map_iterator<hash_map_type>(bucket, it, inserted);
}
```

`emplace_hint()` 方法会忽略提示（hint）并将调用转发给 `emplace()` 方法。此实现使用 `std::forward` 将 `x` 完美转发给 `emplace()`。如果将值引用传递给 `emplace_hint()`，则它将作为右值引用转发给 `emplace()`。如果将左值引用传递给 `emplace_hint()`，则它将作为左值引用转发：

```cpp
template <typename Key, typename T, typename Compare, typename Hash>
typename hash_map<Key, T, Compare, Hash>::iterator
hash_map_Key, T, Compare, Hash>::emplace_hint(
iterator *hint, value_type& x)
{
    // 完全忽略 hint。
    return emplace(std::forward<value_type>(x)).first;
}
```

### hash_map 的 Erase（删除）操作

在前面的章节“基础哈希表”中使用的 `erase()` 版本并不符合 STL 规范。你需要实现以下几个版本：

- 一个接受 `key_type` 作为参数并返回 `size_type` 表示从集合中删除元素数量的版本（对于 `hash_map` 来说，只有两种可能的返回值：0 和 1）。
- 一个在特定迭代器位置删除值，并返回指向被删除元素之后元素的迭代器版本。
- 一个根据两个迭代器删除范围内的元素，并返回指向最后一个删除元素之后元素的迭代器版本。

第一个版本的实现如下：
