
```cpp
template <class Iterator, class Iterator2>
constexpr bool operator>=(const move_iterator<Iterator>& x, const move_iterator<Iterator2>& y);
  返回：!(x < y);
```

## 27.5.3.3.14 move_iterator 非成员函数 move_iter.nonmember

```cpp
template <class Iterator1, class Iterator2>
constexpr auto operator-(
const move_iterator<Iterator1>& x,
const move_iterator<Iterator2>& y) -> decltype(x.base() - y.base());
  返回：x.base() - y.base();
```

```cpp
template <class Iterator>
constexpr typename move_iterator<Iterator>::difference_type operator+(const move_iterator<Iterator>& x, auto n);
  返回：x + n;
```

```cpp
template <class Iterator>
auto move_iterator<Iterator> make_move_iterator(Iterator i);
  返回：move_iterator<Iterator>(i);
```

## 27.6 流迭代器 [stream.iterators]

为了使算法模板能够直接处理输入输出流，提供了相应的迭代器类。

示例：

```cpp
partial_sum(istream_iterator<double, char>(cin),
istream_iterator<double, char>(),
ostream_iterator<double, char>(cout, "\n"));
```

从 `cin` 读取包含浮点数的文件，并将部分和打印到 `cout` 示例中。

## 27.6.1 模板类 iterator_iterator [stream.iterator]

`class iterator_iterator` 是一种输入迭代器（27.2.3），它通过 `operator>>` 从其构造的流中读取连续元素。在构造后，以及每次使用 `++` 时，迭代器都会读取并存储一个 `T` 类型的值。如果迭代器未能读取并存储 `T` 类型的值（流返回 true），则该迭代器将变为流结束迭代器值。带有 `input_iterator` 的构造函数始终构造一个有效的迭代器，这是用于结束条件的唯一合法迭代器。在流结束迭代器上执行 `operator+` 的结果未定义。对于任何其他值，返回一个 `const T`。

# ISO/IEC 14882:2017(E)

```cpp

ostream_iterator& operator=(const T& value);

ostream_iterator& operator*();

ostream_iterator& operator++();

ostream_iterator& operator++(int);

```

```cpp

private:

    basic_ostream<charT,traits> out_stream; // 仅用于说明

                                // 仅用于说明

    charT;

```

## 27.6.2.1 ostream_iterator 构造函数与析构函数

> [ostream.iterator.cons]

`ostream_iterator(const ostream_type& s);`

+ 1
Effects：使用 `addressof(s)` 初始化 `out_stream` 并将 `delim` 置 null。

`ostream_iterator(const ostream_type& s, const charT delimiter);`

Effects：使用 `addressof(s)` 初始化 `out_stream` 并将 `delim` 设置为 `delimiter`。

`ostream_iterator(const ostream_iterator& x);`

Effects：构造 `x` 的拷贝。

`-ostream_iterator();`

Effects：迭代器被销毁。

## 27.6.2.2 ostream_iterator 运算符操作

> [ostream.iterator.ops]

`ostream_iterator& operator=(const T& value);`

等同：

```cpp

*out_stream << value;

if (delim == 0)

    *out_stream << delim;

return *this;

```

`ostream_iterator& operator*();`

Returns：`*this*`。

```cpp

ostream_iterator& operator++();

ostream_iterator& operator++(int);

```

Returns：`*this*`。

## 27.6.3 类模板 istream_bufiter

类模板 `istream_bufiter` 定义了一个输入迭代器 (27.2.3)，它从 `streambuf` 读取字符，并提供对当前字符的访问。当每个迭代器被求值时，迭代器会移动到下一个输入。如果到达流的末尾（`ambuf_type::getc()` `traits::eof()`），则迭代器变为流末尾迭代器值。默认构造函数 `istream_bufiter()` 和构造函数 `istream_bufiter(0)` 构造一个适用于作为范围结束的流末尾迭代器。`istream_bufiter` 的所有特化都应具有平凡的拷贝构造函数、constexpr 默认构造函数以及平凡的析构函数。

+ 2 在流末尾迭代器上执行 `operator*()` 的结果是未定义的。对于任何其他迭代器值，返回一个 `char_type` 值。无法通过输入迭代器赋值字符。

## ISO/IEC 14882:2017(E)

```cpp

namespace std {

template<class charT, class traits = char_traits<charT>>

class istambuf_iterator {

public:

    using iterator_category = input_iterator_tag;

    using value_type = charT;

    using difference_type = typename traits::difference_type;

    using pointer = const charT*;

    using reference = const charT&;

    using char_type = traits::charT;

    using int_type = typename traits::int_type;

    using streambuf_type = basic_streambuf<charT,traits>;

    using stream_type = basic_istream<charT,traits>;

    // 仅代理

    constexpr istambuf_iterator() noexcept;

    istambuf_iterator(const istambuf_iterator& r) noexcept = default;

    istambuf_iterator(streambuf_type& s) noexcept;

    istambuf_iterator(streambuf_type* s) noexcept;

    istambuf_iterator(const proxy& p) noexcept;

    charT operator*() const;

    istambuf_iterator& operator++() = default;

    proxy& operator++(int);

    bool operator==(const istambuf_iterator& b) const;

private:

    streambuf_type* sbuf;

}; // 仅代理

```

### 27.6.3.1 类模板 istambuf_iterator::proxy

```cpp

namespace std {

template<class charT, class traits = char_traits<charT>>

class istambuf_iterator<charT,traits>::proxy { // 仅代理

    char keep;

    basic_streambuf<charT,traits>* sbuf;

    proxy(charT c, basic_streambuf<charT,traits>* sbuf)

        : keep(c), sbuf(sbuf) {}

public:

    charT operator*() { return keep; }

};

```

类 `istambuf_iterator<charT,traits>::proxy` 用于提供不具类名的等效功能。类 `istambuf_iterator<charT,traits>::proxy` 为后增运算符（`operator++`）的返回值提供一个临时占位符。它保留迭代器之前值所指向的字符，以便以后获取该字符。

## 27.6.3.2 istreambuf_iterator 构造函数 [istreambuf_iterator.cons]

+ 1 对于本节中的每个 `istreambuf_iterator` 构造函数，当且仅当异常成员 `sbuf_` 被空指针初始化时，才会构造一个流末尾迭代器。

```cpp

constexpr istreambuf_iterator() noexcept;

```

+ 2 Effects：将 `sbuf_` 初始化为 `nullptr`。

```cpp

istreambuf_iterator(istreambuf_type& s) noexcept;

```

+ 3 Effects：将 `sbuf` 初始化为 `s.rddbuf()`。

```cpp

istreambuf_iterator(istreambuf_type* s) noexcept;

```

+ 4 Effects：将 `sbuf_` 初始化为 `s`。

```cpp

istreambuf_iterator(const proxy& p) noexcept;

```

+ 5 Effects：将 `sbuf_` 初始化为 `p.sbuf_`。

## 27.6.3.3 istreambuf_iterator 操作 [istreambuf_iterator.ops]

```cpp

charT operator+();

```

+ 1 Returns：由 `istambuf sbuf_->getc()` 获取的字符。

```cpp

istreambuf_iterator operator++();

```

+ 2 Effects：等同于 `sbuf_->sbmp()`。

+ 3 Returns：`*this*`。

```cpp

proxy operator+(int);

```

+ 4 Returns：`proxy(sbuf_->sbmp(), sbuf_)`。

```cpp

bool equal(const istreambuf_iterator b) const;

```

+ 5 Returns：如果两个迭代器都是流末尾的，则返回 true。

```cpp

template <class charT, class traits>

bool operator==(const istreambuf_iterator<charT,traits>& a, const istreambuf_iterator<charT,traits>& b);

```

+ 6 Returns：true。

```cpp

template <class charT, class traits>

bool operator!=(const istreambuf_iterator<charT,traits>& a, const istreambuf_iterator<charT,traits>& b);

```

+ 7 Returns：false。

## 27.6.4 类模板 istambuf_iterator

```cpp

namespace std {

  template<class charT, class traits = char_traits<charT>>

  class istambuf_iterator {

public:

    using iterator_category = input_iterator_tag;

    using value_type = charT;

    using difference_type = typename traits::difference_type;

    using pointer = const charT*;

    using reference = const charT&;

    using char_type = traits::charT;

    using int_type = typename traits::int_type;

    using streambuf_type = basic_streambuf<charT,traits>;

    using stream_type = basic_istream<charT,traits>;

    istambuf_iterator() noexcept;

    istambuf_iterator(streambuf_type& s);

    istambuf_iterator(streambuf_type* s);

    istambuf_iterator(const proxy_type& p);

    istambuf_iterator(const istambuf_iterator& r) = default;

    istambuf_iterator(istreambuf_iterator&&) noexcept = default;

    istambuf_iterator& operator=(const istambuf_iterator& r) = default;

    istambuf_iterator& operator=(istreambuf_iterator&&) noexcept = default;

    charT operator*() const;

    istambuf_iterator& operator++() = default;

    istambuf_iterator& operator++(int);

    bool operator==(const istambuf_iterator& b) const;

    bool operator!=(const istambuf_iterator& b) const;

};

```

# ISO/IEC 14882:2017(E)

```cpp

template <class C> constexpr rend(const C& c) -> decltype(std::rend(c));

Returns: std::rend(c).

```

## 27.8 容器访问

除了可以通过包含 `<iterator>` 头文件可用外，27.8 节中的函数模板在包含以下任何头文件时可用：`<regex>`, `<set>`, `<string>`, `<unordered_map>`, `<unordered_set>`, `<list>`, `<map>`, `<deque>`, `<forward_list>` 和 `<vector>`。

```cpp

template <class C> constexpr auto size(const C& c) -> decltype(c.size());

Returns: c.size().

```

```cpp

template <class T, size_t N> constexpr auto size(const T (&array)[N]) noexcept

Returns: N.

```

```cpp

template <class C> constexpr auto empty(const C& c) -> decltype(c.empty());

Returns: false.

```

```cpp

template <class T, size_t N> constexpr bool empty(const T (&array)[N]) noexcept

Returns: false.

```

```cpp

template <class E> constexpr bool empty(initializer_list<E> il) noexcept;

Returns: il.size() == 0.

```

```cpp

template <class C> constexpr auto data(const C& c) -> decltype(c.data());

Returns: c.data().

```

```cpp
