

```cpp
template<typename Iterator, typename Distance>
EnableIf<IsBidirectionalIterator<Iterator> &&
         !IsRandomAccessIterator<Iterator>>
advance(Iterator& it, Distance n) {
  if (n > 0) {
    for (; n > 0; ++it, --n) //linear time
    {
    }
  } else {
    for (; n < 0; --it, ++n) //linear time
    {
    }
  }
}

// implementation for all other iterators:
template<typename Iterator, typename Distance>
EnableIf<!IsBidirectionalIterator<Iterator>>
advance(Iterator& it, Distance n) {
  if (n < 0) {
    throw "advance(it): invalid iterator category for ...";
  }

  while (n > 0) { //linear time
    ++it;
    --n;
  }
}
```

通过使每个函数模板的 enable_if 条件与其他所有函数模板的 EnableIf 条件互斥，我们确保对于一组给定的实参，最多只有一个函数模板能成功进行模板实参推导。

我们的示例说明了使用 EnableIf 进行算法特化的一个缺点：每次引入算法的新变体时，都需要重新检查所有算法变体的条件，以确保它们互斥。相比之下，使用标签分派（第 697 页 20.2.0 节）引入双向迭代器变体，只需添加一个新的使用 `std::bidirectional_iterator_tag` 标签的 `advanceIter()` 重载即可。

### 20.3.2 EnableIf 应该放在哪里？

EnableIf 通常用在函数模板的返回类型中。然而，这种方法对于构造函数模板或转换函数模板不适用，因为两者都没有指定的返回类型。例如，使用 EnableIf 可以使返回类型根据模板参数而变化。在这种情况下，我们可以将 EnableIf 嵌入到默认模板实参中，如下所示：

[点击此处查看代码图片](https://...)

```cpp
#include <iterator>
#include <enable_if.hpp>
#include <functional.hpp>

template<typename Iterator>
  constexpr bool IsInputIterator =
    isConvertible<
      typename std::iterator_traits<Iterator>::iterator_category,
      std::input_iterator_tag>;

// ...
```

```cpp
template<typename T>
class Container {
public:

  // construct from an input iterator sequence:
  template<typename Iterator,
           typename = EnableIfIsConvertibleToIterator>
  Container(Iterator first, Iterator last);

  // convert to a container so long as the value type ...
  template<typename U, typename = EnableIfIsConvertibleTo...>
  operator Container<U>() const;
};
```

然而，这里存在一个问题。如果我们尝试再添加另一个重载（例如，针对非类访问迭代器的更高效的 Container 构造函数版本），将会导致错误。

[点击此处查看代码图片](#)

```cpp
// construct from an input iterator sequence:
template<typename Iterator,
         typename = EnableIfIsConvertibleToIterator<T>,
         typename = IsRandomAccessIterator<Iterator>>
Container(Iterator first, Iterator last);

template<typename Iterator,
         typename = EnableIfIsConvertibleToIterator<T>,
         typename = ...>
Container(Iterator first, Iterator last); // ...
```

问题在于，这两个构造函数模板除了默认模板实参外完全相同，而在确定两个模板是否等价时，默认模板实参是不被考虑的。

我们可以通过再添加一个默认函数模板参数来缓解这个问题，这样两个构造函数模板就具有不同数量的模板参数：

[点击此处查看代码图片](#)

```cpp
// construct from an input iterator sequence:
template<typename Iterator,
         typename = EnableIfIsConvertibleToIterator<T>,
         typename = IsRandomAccessIterator<Iterator>>
Container(Iterator first, Iterator last);

template<typename Iterator,
         typename = EnableIfIsConvertibleToIterator<T>,
         typename = ...>
Container(Iterator first, Iterator last); // OK now: no-
                                         // longer ...
```

### 20.3.3 编译期 if

这里值得指出的是，C++17 的 `constexpr if` 语法（参见第 34 页 8.5 节）在许多情况下避免了对 EnableIf 的需求。例如，在 C++17 中，我们可以将 `advance()` 示例重写如下：

[点击此处查看代码图片](#)

cppreference.com/w/cpp/language/if

```cpp
template<typename Iterator, typename Distance>

void advance(Iterator& x, Distance n) {

  if constexpr (IsRandomAccessIterator<Iterator>) {

    // implementation for random access iterators:
    x += n;                         // constant

  }
  else if constexpr (IsBidirectionalIterator<Iterator>) {

    // implementation for bidirectional iterators:
    if (n > 0) {

      for (; n > 0; ++x, --n)  // linear time for positive n
      {
      }
    }
    else {

      for (; n < 0; --x, ++n)  // linear time for negative n
      {
      }
    }
  }
  else {
    // implementation for all other iterators that are...
    if (...) {
        throw "advance(it): invalid iterator category";
    }

    while (n > 0) {        // linear time for ...
        ++x;
        --n;
    }
  }
}
```

这样清晰得多。更专用的代码路径（例如，针对随机访问迭代器）只会为能够支持它们的类型实例化。因此，只要代码位于适当受保护的 `if constexpr` 体内，即使涉及并非所有迭代器都支持的操作（如 `+=`）也是安全的。

然而，这样做也有缺点。仅当泛型组件中的差异可以完全表达在函数模板体内时，才能以这种方式使用 `constexpr if()`。在以下情况下，我们仍然需要 EnableIf：

-   涉及不同的“接口”
-   需要不同的类定义
-   对于某些模板实参列表，不应存在有效的实例化。

人们很自然地会想用下面的模式来处理最后一种情况：

点击此处查看代码图片

```cpp
template<typename T>
void f(T x) {
    if constexpr (condition<T>::value) {
        // do something here...
    }
    else {
        // not a T for which f() makes sense
        static_assert(condition<T>::value, "can't call f()");
    }
}
```

这样做并不可取，因为它不能很好地与 SFINAE 配合：函数 `f(T x)` 不会从候选列表中移除，因此可能会妨碍其他重载决议结果。作为替代方案，使用 `EnableIf<T>::...` 时，当 `EnableIf<...>` 的替换失败，整个函数会被移除。

### 20.3.4 概念

到目前为止介绍的技术运行良好，但通常有些笨拙，可能会消耗相当多的编译器资源，并且在出错时可能导致难以处理的诊断信息。因此，许多泛型库作者期待一种能够更直接实现相同效果的语言特性。出于这个原因，一个称为“概念（concepts）”的特性很可能会被添加到语言中；参见第 103 页 6.5 节、第 377 页 8.0 节以及附录 E。

例如，我们期望重载的容器构造函数可以简单地写成如下形式：

点击此处查看代码图片

```cpp
template<typename T>
class Container {
public:
    // construct from an input iterator sequence:
    template<typename Iterator>
    requires InputIterator<Iterator>
    Container(Iterator first, Iterator last);

    // construct from a random access iterator sequence:
    template<typename Iterator>
    requires IsRandomAccessIterator<Iterator>
    Container(Iterator first, Iterator last);

    // convert to a container so long as the value type ...
    template<typename U>
    requires IsConvertible<T, U>
    operator Container<U>() const;
};
```

requires 子句（在第 70 页 5.1 节讨论）描述了模板的要求。如果任何要求未被满足，该模板就不会被视为候选。因此，它是语言本身对表 5.1 所表达思想的更直接支持。

与 `enable_if` 相比，requires 子句还有额外的好处。约束累积（在第 74 页 5.3.1 节描述）在实现选择范围很小的模板之间提供了排序，从而消除了对标签分派的需求。此外，requires 子句可以附加到非模板上。例如，当类型 T 可以使用 `<` 进行比较时，提供一个 `sort()` 成员函数：

点击此处查看代码图片

```cpp
template<typename T>
class Container {
public:
    requires HasLess<T>
    void sort() {
        ...
    }
};
```

## 20.4 类模板特化

类模板偏特化可用于为特定的模板实参提供类模板的替代专用实现，就像我们对函数模板使用重载一样。而且，与重载函数模板类似，基于模板实参的属性来区分这些偏特化是有意义的。考虑一个以键和值类型作为模板参数的通用 `Dictionary` 类模板。只要键类型提供相等运算符，就可以实现一个简单但低效的 `Dictionary`：

点击此处查看代码图片

```cpp
template<typename Key, typename Value>
class Dictionary
{
private:
    vector<pair<Key, Value>> data;
public:
    // subscripted access to the data:
    Value& operator[](const Key& key)
    {
        // search for the element with this key:
        for (auto& element : data) {
            if (element.first == key) {
                return element.second;
            }
        }

        // there is no element with this key; add one
        data.push_back({key, Value{}});
        return data.back().second;
    }
};
```

如果键类型支持 `<` 运算符，我们可以基于标准库的 `map` 容器提供更高效的实现。类似地，如果键类型支持哈希操作，我们可以基于标准库的 `unordered_map` 提供更高效的实现。

### 20.4.1 启用/禁用类模板

启用/禁用类模板不同实现的方法是使用类模板的启用/禁用偏特化。为了使用 EnableIf，我们定义带模板的偏特化。首先为 `Dictionary` 引入一个未命名的默认模板参数：

点击此处查看代码图片

```cpp
template<typename Key, typename Value, typename = void>
class Dictionary
{
    ...
};
```

这个新的模板参数充当 `enable_if` 的锚点，`enable_if` 可以嵌入到支持 `<` 的 `Dictionary` 偏特化的模板实参列表中：

点击此处查看代码图片

```cpp
template<typename Key, typename Value>
class Dictionary<Key, Value,
    typename = ...>
{
    ...
};
```

