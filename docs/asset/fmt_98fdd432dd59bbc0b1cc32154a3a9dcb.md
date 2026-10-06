
```cpp
StringPtr::iterator begin();    // 返回指向第一个元素的迭代器
StringPtr::iterator end();      // 返回最后一个元素
                                之后的迭代器
```

由于这两个成员返回了（正确的）迭代器，`StringPtr` 对象中的元素可以很容易地排序：

```cpp
int main() {
    StringPtr sp;                                // 假设 sp 已经填充了内容
    sort(sp.begin(), sp.end());                 // sp 现在已排序
}
```

为了使此正常工作，定义了 `StringPtr::iterator`。正如其类型所示，`iterator` 是 `StringPtr` 的嵌套类型。为了结合通用算法使用 `StringPtr::iterator`，它必须是一个随机访问迭代器，其 `value_type` 为 `std::string`。因此，该迭代器指定了：

```cpp
using iterator_category = std::random_access_iterator_tag;
using difference_type = std::ptrdiff_t;
using value_type = std::string;
using pointer = value_type *;
using reference = value_type &;
```

现在我们准备好定义 `StringPtr` 的类接口了。它提供了返回（反向）迭代器和一个嵌套类。以下是它的接口：

```cpp
struct StringPtr : public std::vector<std::string> *;
```

```cpp
{
class iterator;
  using reverse_iterator = std::reverse_iterator<iterator>;

  iterator begin();
  iterator end();
  reverse_iterator rbegin();
  reverse_iterator rend();
};
```

```cpp
struct StringPtr::iterator
{
  using iterator_category = std::random_access_iterator_tag;
  using difference_type = std::ptrdiff_t;
  using value_type = std::string;
  using pointer = value_type *;
  using reference = value_type&;
```

我们来看 `StringPtr::iterator` 的特性：

- `iterator` 将 `StringPtr` 定义为其友元，因此 `StringPtr` 的构造函数是私有的。拷贝构造函数和迭代器赋值能够构造类项，但这可以通过默认值实现，不需要特定的声明或实现。此外，由于 `StringPtr` 的基类已经提供了一个迭代器，我们可以使用 `iterator` 来访问存储在 `StringPtr` 对象中的信息。

- `StringPtr::begin` 和 `StringPtr::end` 可能简单地返回迭代器对象。它们的实现如下：

  - inline StringPtr::StringPtr::begin() {

      - return iterator(std::vector<std::string>::begin());

    }

  - inline StringPtr::StringPtr::end() {

      - return iterator(std::vector<std::string>::end());

    }

- `iterator` 剩余的所有成员都是公有的。实现它们非常容易，主要是对可用的迭代器 `d_current` 进行递增和解引用。随机访问迭代器需要一系列操作。它们的实现非常简单，通常可以实现良好，例如：

  - `iterator &operator++();` 前置增运算符：

    inline StringPtr::iterator &StringPtr::iterator::operator++() {

      +d_current;

      return *this;

    }

  - `iterator operator++(int);` 后置增运算符：

    inline StringPtr::iterator StringPtr::iterator::operator++(int) {

      return iterator(d_current++);

    }

## 22.14. 构造 &operator=()

- `iterator &operator--();` 前置减运算符：

```cpp
inline StringPtr::iterator &StringPtr::iterator::operator--()
{
    --d_current;
    return *this;
}
```

- `iterator operator--(int);` 后置减运算符：

```cpp
inline StringPtr::iterator StringPtr::iterator::operator--(int)
{
    return iterator(d_current--);
}
```

- `iterator operator=(iterator const &other);` 重载的赋值运算符。由于迭代器本身不分配任何内存，可以使用默认赋值运算符。

- `bool operator===(iterator const &rhv);` 测试两个迭代器对象的等等性：

```cpp
inline bool operator===(StringPtr::iterator const &lhs, StringPtr::iterator const &rhs) 
{
    return lhs.d_current == rhs.d_current;
}
```

- `auto operator<=>(iterator const &rhv);` 测试两个迭代器对象的顺序：

```cpp
inline auto operator<=>(StringPtr::iterator const &lhs, StringPtr::iterator const &rhs) 
{
    return lhs.d_current <= rhs.d_current;
}
```

- `int operator-(iterator const &rhv);` 返回左侧迭代器与右侧迭代器之间的元素数量：

```cpp
inline int operator-(StringPtr::iterator const &lhs, StringPtr::iterator const &rhs) 
{
    return lhs.d_current - rhs.d_current;
}
```

- `Type &operator*() const;` 返回迭代器指向的对象。对于常量迭代器，返回类型应该是 `Type &`。该字符串通过解引用 `d_current` 获取：

```cpp
inline std::string &StringPtr::iterator::operator*() const 
{
    return d_current;
}
```

- `iterator operator+(int step);` 该运算符按步增加当前迭代器：

```cpp
inline StringPtr::iterator operator+(StringPtr::iterator const &lhs, int step)
{
    StringPtr::iterator ret(lhs);
    ret.d_current += step;
    return ret;
}
```

- `iterator operator-(int step);` 该运算符按步减少当前迭代器：

```cpp
inline StringPtr::iterator operator-(StringPtr::iterator const &lhs, int step)
{
    StringPtr::iterator ret(lhs);
    ret.d_current -= step;
    return ret;
}
```

- `std::string *operator->() const;` 附加的运算符。这里只需要一次解引用操作，返回字符串的指针，允许我们通过迭代器访问字符串的成员：

```cpp
inline std::string *StringPtr::iterator::operator->() const
{
    return &d_current;
}
```

- 两个附加的运算符是 `operator+=` 和 `operator-=`。访问迭代器并没有正式要求它们，但它们经常有用。

```cpp
inline StringPtr::iterator &StringPtr::iterator::operator+=(int step)
{
    d_current += step;
    return *this;
}
```

```cpp
inline StringPtr::iterator &StringPtr::iterator::operator-=(int step)
{
    d_current -= step;
    return *this;
}
```

其他迭代器的接口更简单，只需要随机访问迭代器接口的子集。例如，前向迭代器永远不会递减，也不会按任意步长递增。因此在这种情况下可以从接口中省略所有的减运算符和 `operator+(int step)`。当然，使用的标签将是 `std::forward_iterator_tag`。标签（以及所需的运算符集合）随其他迭代器类型相应变化。

## 22.1.4 实现‘反向迭代器’

一旦我们实现了迭代器，就可以很快地实现匹配的反向迭代器。为了实现反向迭代器，使用了 `std::reverse_iterator`，它很好地实现了

## 22.14. 构建迭代器

一旦我们定义了迭代器，就可以构造反向迭代器。它的构造函数仅需一个我们想要构造反向迭代器的迭代器类型的对象。

为了为 `StringPtr` 实现反向迭代器，我们只需要在它的接口中定义 `reverse_iterator` 类型。这只需要一行代码，必须插入到类 `iterator` 的接口中：

```cpp
using reverse_iterator = std::reverse_iterator<iterator>;
```

此外，广为人知的成员 `rbegin` 和 `rend` 也被添加到 `StringPtr` 的接口中。同样地，它们可以很容易地实现为：

```cpp
inline StringPtr::reverse_iterator StringPtr::begin()
{
    return reverse_iterator(end());
}
inline StringPtr::reverse_iterator StringPtr::rend()
{
    return reverse_iterator(begin());
}
```

注意 `reverse_iterator` 构造函数接收的参数：反向迭代器的起始点是通过向 `reverse_iterator` 构造函数提供成员函数 `end` 返回的值得到的（即普通迭代器的终点）；反向迭代器的终点是通过向 `reverse_iterator` 构造函数提供成员函数 `begin` 返回的值得到的（即普通迭代器的起始点）。

以下程序演示了 `StringPtr` 的 `RandomAccessIterator` 的用法：

```cpp
#include <iostream>
#include <algorithm>
#include "stringptr.h"
using namespace std;

int main(int argc, char **argv)
{
    StringPtr sp;

    while (*argv)
        sp.push_back(new string(*argv++));

    sort(sp.begin(), sp.end());
    copy(sp.begin(), sp.end(), ostream_iterator<string>(cout, " "));

    cout << "\n======\n";

    sort(sp.rbegin(), sp.rend());
    copy(sp.rbegin(), sp.rend(), ostream_iterator<string>(cout, " "));

    cout << '\n';
}
```

```cpp
/*
当调用为：
 a.out bravo mike charlie zulu quebec
```

# 第 22 章：类模板

```
生成的输出：
a.out bravo charlie mike quebec zulu
=====
zulu quebec mike charlie bravo a.out
*/
```

虽然由此可以从普通迭代器构造反向迭代器，但反之则不然：无法从反向迭代器初始化普通迭代器。

假设我们想要处理 `vector<string> lines` 中存储的所有行，直到任何末尾的空行（仅包含空格的行）。我们该如何操作呢？一种方法是从向量的第一行开始处理，一直到第一个末尾空行为止。然而，一旦我们遇到空行，它并不一定是是末尾空行集中的第一行。在这种情况下，我们使用以下算法：

- 首先，使用

  rit = find_if(lines.begin(), lines.rend(), Empty());

  来获取一个指向最后一个非空行的反向迭代器

- 接下来，使用

  for_each(lines.begin(), --rit, Process());

来处理直到第一个空行之前的所有行

然而，在使用泛型算法时，我们不能混合使用迭代器和反向迭代器。那么，我们可以使用现有的 `reverse_iterator` 来初始化第二个迭代器吗？解决方案并不困难，因为迭代器可以从指针初始化。虽然反向迭代器 `rit` 不是指针，但 `&*(rit) = &+NO_TRANS((--i))rit` 是。因此我们使用它来处理直到末尾空行集中第一个行的行。通常情况下，如果 `rit` 是指向某个元素的反向迭代器，而我们需要一个指向该元素的迭代器，我们可以使用 `&rit` 来初始化迭代器。在这里，解引用运算符允许访问反向迭代器所指的元素。运算符的地址通过

在定义 `const_reverse_iterator` 时，`const_iterator::operator--` 必须是可修改的值或对象的成员。由于 `reverse_iterator` 使用了迭代器的 `operator--`，我们遇到了一个小冲突。一方面，`std::input_iterator_tag` 是不合适的，因为我们必须允许迭代器递减；另一方面，`std::bidirectional_iterator` 也是合适的，因为我们不允许修改数据。

迭代器标签主要是概念性的。如果 `const_iterators` 和 `const_reverse_iterators` 只允许递增操作，那么 `input_iterator_tag` 是迭代器的最佳选择。此外，由于 `input_iterator_tag` 的性质，这导致 `const_iterator` 不应该允许 `operator--`。这可以通过将迭代器的 `operator--` 存储在迭代器的私有部分来解决（注意声明一个派自 `std::reverse_iterator` 的 `const_iterator` 并没有解决这个问题：它是一个调用迭代器 `operator--` 的 `reverse_iterator`）。

为了保持解引用 `const_iterator` 的常 性，`Data::iterator` 提供的规范可以添加到 `const_iterator` 类中。`Data::const_iterator` 继承自 `Data::iterator`，但它可能也指定：

```cpp
using const_pointer   = value_type const;
using const_reference = value_type const &
```

其中其 `operator()` 返回 `const_reference`。接面的示例说明了涉及 `iterator`、`const_iterator`、`reverse_iterator` 和 `const_reverse_iterator` 的元素，这些类型可以传递给 `reverse_iterator` 模板以获取相应的迭代器：

编译：仅声明，未实现

#include <string>

#include <iterator>

#include <iostream>

struct Data {

    class iterator;

    class const_iterator;

    using reverse_iterator = std::reverse_iterator<iterator>;

    using const_reverse_iterator = std::reverse_iterator<const_iterator>;

    private:

        std::string *d_data;

        size_t d_n;

    // ...

};

struct Data::iterator {
