
# 编写迭代器

最重要的容器要求是提供迭代器。为了与通用算法配合，每个容器必须提供一个访问容器元素的迭代器。你的迭代器通常应该重载 `operator*` 和 `operator->`，以及根据特定行为提供其他操作。只要你的迭代器提供了基本的迭代操作，一切就没问题。

创建迭代器时的第一个决定是它的类型：前向、双向还是随机访问。随机访问迭代器对于关联容器来说没有意义，因此双向迭代器似乎是 `hash_map` 迭代器的逻辑选择。这意味着你还必须提供 `operator++`、`operator--` 和 `operator==`。关于关于不同迭代器要求的更多详细信息，请参阅第 16 章。

第二个决定是如何对容器中的元素排序。`hash_map` 是无序的，按照排序后的顺序进行迭代可能太困难了。相反，你的迭代器只需要遍历各个桶 `buckets`，从第一个桶的元素开始，一直进行到最后一个桶的元素。这种顺序对客户端来说是随机的，但它是一致且可重复的。

第三个决定是如何表示你的迭代器。其实现通常取决于容器的内部实现方式。迭代器的主要目的是引用容器中的单个元素。在 `hash_map` 的情况下，每个元素都在一个 STL `list` 中，因此 `hash_map` 迭代器可以是一个对 `list` 迭代器的封装，指向所对应的元素。然而，双向迭代器的目的是允许客户端移动到下一个或上一个元素。为了从一个桶移动到下一个桶，你需要跟踪当前的桶以及迭代器所引用的 `hash_map` 对象。

一旦你选择了实现方式，就必须为“结束” `end` 确定一个一致的表示。记住，结束迭代器应该是“越界结束”标记：即通过对指向容器中最后一个元素的迭代器应用 `++` 得到的迭代器。`hash_map` 迭代器可以使用 `hash_map` 中最后一个桶的 `list` 作为它的结束迭代器。

容器需要同时提供 `const` 迭代器和非 `const` 迭代器。非 `const` 迭代器必须转换为 `const` 迭代器。此实现定义了一个 `const_hash_map_iterator` 类，并让 `hash_map_iterator` 派生自它。

## const_hash_map_iterator 类

根据上一节所做的决定，现在是时候定义 `const_hash_map_iterator` 类了。首先需要注意的是，`const_hash_map_iterator` 对象是针对 `hash_map` 类特定实例的迭代器。为了提供这种一对一的映射，`const_hash_map_iterator` 也必须是一个类，并以哈希映射类型作为模板参数 `HashMap`。

类定义中的主要问题是如何表现得像一个双向迭代器。记住，你的类并不为了符合双向迭代器的资格而必须派生自另一个类。然而，为了让你的迭代器在通用算法中有用，你必须指定它的类型。本章的讨论解释了 `iterator_traits` 是一个类模板，它为每种迭代器类型定义了五个类型定义 `typedef`。如果你愿意，可以为你的新迭代器对其进行部分特化。或者，`iterator_traits` 类模板的实现也可以直接从迭代器类本身获取这五个 `typedef`。因此，你可以直接在你的类中定义这些 `typedef`。事实上，这比你自己定义它们还要简单，你只需要使用迭代器类，它会为你提供这些 `typedef`。你只需要将迭代器类型和元素类型作为模板参数传递给迭代器类。`const_hash_map_iterator` 是双向迭代器，因此你指定 `bidirectional_iterator_tag` 为迭代器类型。其他法的迭代器类型包括 `input_iterator_tag`、`output_iterator_tag`、`forward_iterator_tag` 和 `random_access_iterator_tag`。对于 `const_hash_map_iterator`，元素类型是 `typename HashMap::value_type`。

基本上，这归结为从通用类模板派生你的迭代器类是最简单的。

以下是基本的 `const_hash_map_iterator` 类定义：

```cpp
template <typename HashMap>
class const_hash_map_iterator : public std::iterator<
    std::bidirectional_iterator_tag, typename HashMap::value_type>
public:
    using value_type = typename HashMap::value_type;
    using list_iterator_type = typename HashMap::ListType::const_iterator;
    // 双向迭代器必须提供默认构造函数
    const_hash_map_iterator();
    const_hash_map_iterator(size_t bucket, list_iterator_type listIt,
                            const HashMap* inhash);
    const value_type& operator*() const;
    // 返回类型必须是可以 -> 的类型。
    // 返回一个指向 pair<const, T> 的指针，编译器将
    // 应用 -> get。
    const value_type* operator->() const;
    const_hash_map_iterator<HashMap>& operator++() const;
    const_hash_map_iterator<HashMap> operator++(int);
    const_hash_map_iterator<HashMap>& operator--() const;
    const_hash_map_iterator<HashMap> operator--(int);
    // 不需要定义拷贝构造函数或赋值=，因为
    // 默认行为就是我们想要的。
    // 不需要析构函数，因为默认行为
    //（删除 inhash）就是我们想要的。
    // 以下内容作为成员函数是可以的，因为我们
    // 支持此类型与不同类型进行比较。
    bool operator==(const const_hash_map_iterator<HashMap>& rhs) const;
    bool operator!=(const const_hash_map_iterator<HashMap>& rhs) const;
protected:
    size_t mBucketIndex;
    list_iterator_type mlistIterator;
    const HashMap* mHashMap;
    // 用于 operator++ 的辅助方法
    void increment();
    void decrement();
```

解引用和实现重载运算符是简洁的；详情请咨询第 14 章。`const_hash_map_iterator` 构造函数初始化三个成员变量。默认构造函数仅用于客户端可以声明 `const_hash_map_iterator` 而无需初始化。使用默认构造的迭代器不需要引用任何值。

解引用 `operator*` 和 `operator->` 是复杂的。第 14 章解释了 `operator*` 返回实际值，而 `operator->` 必须返回一个编译器可以应用 `->` 的指针。`const_hash_map_iterator` 返回迭代器引用的元素，`operator->` 返回元素的指针。`operator*` 返回实际元素：

```cpp
const_hash_map_iterator<HashMap>::value_type& operator*() const {
    return *mListIterator;
}
```

```cpp
const_hash_map_iterator<HashMap>::value_type* operator->() const {
    return &(*mListIterator);
}
```

增减运算符实现如下：

```cpp
const_hash_map_iterator<HashMap>& operator++() const {
    increment();
    return *this;
}
```

```cpp
const_hash_map_iterator<HashMap> operator++(int) {
    auto oldIt = *this;
    increment();
    return oldIt;
}
```

```cpp
const_hash_map_iterator<HashMap>& operator--() const {
    decrement();
    return *this;
}
```

```cpp
const_hash_map_iterator<HashMap> operator--(int) {
    auto oldIt = *this;
    decrement();
    return oldIt;
}
```

递增 `const_hash_map_iterator` 是让它引用容器中的“下一个”元素。该方法首先检查是否已到达桶的末尾；因此它寻找 `hash_map` 中的下一个非空桶，并将迭代器设置为该桶的起始元素。它不能简单地移动到下一个桶，因为该桶可能没有任何元素。如果没有非空桶，根据本示例选择的约定，`mListIterator` 将设置为 `hash_map` 中最后一个桶的迭代器，这就是 `const_hash_map_iterator` 的特殊“结束”位置。迭代器并不要求比指针更安全，因此检查诸如递增已经结束的迭代器等操作是必要的：

```cpp
// 如果 mListIterator 已经指向结束之后的元素
// 或者否则无效，行为是未定义的。
void const_hash_map_iterator<HashMap>::increment() {
    // mListIterator 是指向单个桶的迭代器。递增它。
    ++mListIterator;
}
```

```cpp
// 如果我们处于桶的末尾，
// 找到下一个包含元素的桶。
auto& buckets = mHashmap->mBuckets;
if (mLIterator == std::end(buckets[mBucketIndex])) {
    for (size_t i = mBucketIndex + 1; i < buckets.size(); i++) {
        if (!buckets[i].empty()) {
            // 我们找到了一个非空桶。
            // 让 mListIterator 指向该桶中的第一个元素。
            mLIterator = std::begin(buckets[i]);
            mBucketIndex = i;
            return;
        }
    }
    // 没有非空桶。将 mListIterator 指向
    // 列表的迭代器。
    mBucketIndex = buckets.size() - 1;
    mLIterator = std::end(buckets[mBucketIndex]);
}
```

递减 `decrement` 是递增 `increment` 的反：它使迭代器指向容器中“上一个”元素。然而，由于起始和结束位置之间的不对称，存在一种不对称性：起始是第一个元素，但结束是最后一个元素的“后一个位置”。递减算法首先检查底层列表迭代器是否处于其当前桶的起始。如果不是，则进行递减。否则，列表迭代器必须设置为指向该桶中的第一个元素，这通过递减操作得到结束迭代器。如果没有找到非空桶，则递减是无效的，因此代码可以执行任何操作 `未定义行为`。循环对其循环变量使用了符号类型，而不是 `size_t` 等无符号类型，因为循环使用了 `--`：

```cpp
} else {
    // 我们不在桶的开头，所以直接向下移动。
    --mListIterator;
}
```

注意，`increment()` 和 `decrement()` 访问 `hash_map` 类的私有成员。因此，`hash_map` 类将 `const_hash_iterator` 声明为友元类 `friend class`。

在执行 `increment()` 和 `decrement()` 之后，`operator==` 和 `operator=` 非常简单。它们只需要比较对象的三个数据成员：

```cpp
template <typename HashMap>
bool const_hash_map_iterator<HashMap>::operator==(
    const const_hash_map_iterator<HashMap>& rhs) const
{
    // 所有字段，包括迭代器指向的 hash_map，
    // 必须相等。
    return (mHashmap == rhs.mHashmap && mBucketIndex == rhs.mBucketIndex &&
    mListIterator == rhs.mListIterator);
}
```

```cpp
template <typename HashMap>
bool const_hash_map_iterator<HashMap>::operator!(
    const const_hash_map_iterator<HashMap>& rhs) const
{
    return !(*this == rhs);
}
```

`hash_map_iterator` 类派生自 `const_hash_map_iterator`。`hash_map_iterator` 不需要重写 `operator==`、`operator!=`、`increment()` 和 `decrement()`，因为基类版本已经足够了：

```cpp
template <typename HashMap>
class hash_map_iterator : public const_hash_map_iterator<HashMap> {
public:
    using value_type = typename const_hash_map_iterator<HashMap>::value_type;
    using list_iterator_type = typename HashMap::ListType::iterator;
    // 双向迭代器必须提供默认构造函数
    hash_map_iterator();
    hash_map_iterator(size_t bucket, list_iterator_type listIt,
    HashMap* inHashMap);
    value_type& operator*();
    // 返回类型必须是可以使用 -> 操作的类型。
    // 返回一个指向 pair<const Key, T> 的指针，编译器将
    // 再次应用 -> 操作。
    value_type* operator->();
    hash_map_iterator<HashMap>& operator++();
    hash_map_iterator<HashMap> operator++(int);
    hash_map_iterator<HashMap> operator--();
    hash_map_iterator<HashMap> operator--(int);
};
```

## hash_map_iterator 方法实现

`hash_map_iterator` 方法的实现相当直接。构造函数只是调用基类的构造函数。`operator*` 和 `operator--` 使用 const 和非 const 类型。`operator++` 和 `operator--` 使用基类中的 `increment()` 和 `decrement()`，但返回的是 `hash_map` 而不是 `const_hash_iterator`。C++ 命名查找要求你显式使用此指针来引用基类模板中的数据成员和方法：

```cpp
template<typename HashMap>
hash_map_iterator<HashMap>::hash_map_iterator() : const_hash_map_iterator<HashMap>()
{
}
```

```cpp
template<typename HashMap>
hash_map_iterator<HashMap>::hash_map_iterator(size_t bucket,
list_type listIt, HashMap* inHashMap)
: const_hash_map_iterator<HashMap>(bucket, listIt, inHashMap)
{
}
```

```cpp
// 返回实际元素。
template<typename HashMap>
typename hash_map_iterator<HashMap>::operator*()
{
    return const_cast<value_type&>(*(this->mListIterator));
}
```
