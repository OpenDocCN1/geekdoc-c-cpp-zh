
```
template <class BiIter, class ST, class SA>
bool operator!=(const sub_match<BiIter>& lhs,
  const basic_string&
  typename iterator_traits<BiIter>::value_type, ST, SA>& rhs
) {
  Returns: !(lhs == rhs);
}
```

```
template <class BiIter, class ST, class SA>
bool operator<(const sub_match<BiIter>& lhs,
  const basic_string&
  typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);
  Returns: lhs.compare(typename sub_match<BiIter>::string_type(rhs.data(), rhs.size())) < 0;
```

```
template <class BiIter, class ST, class SA>
bool operator>(const sub_match<BiIter>& lhs,
const basic_string
typename iterator_traits<BiIter>::value_type, ST, SA>& rhs): rhs < lhs
```

```
template <class BiIter, class ST, class SA>
bool operator>(const sub_match<BiIter>& lhs,
const basic_string
typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);
  Returns: !(lhs < rhs).
```

```
template <class BiIter, class ST, class SA>
bool operator<const sub_match<BiIter>& lhs,
const basic_string
typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);
  Returns: !(rhs < lhs).
```

```
template <class BiIter>
bool operator=(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs) == 0;
```

```
template <class BiIter>
bool operator!=(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs);
  Returns: !(lhs == rhs);
```

```
template <class BiIter>
bool operator>(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
  Returns: lhs.compare(rhs) > 0;
```

```
template <class BiIter>
bool operator<=(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
  Returns: lhs.compare(rhs) <= 0;
```

```
template <class BiIter>
bool operator>=(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
  Returns: rhs < lhs;
```

```
template <class BiIter>
bool operator<(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
  Returns: !(rhs < lhs);
```

```
template <class BiIter>
bool operator>(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
  Returns: !(lhs < rhs);
```

```
template <class BiIter>
bool operator==(typename iterator_traits<BiIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
  Returns: lhs.compare(typename sub_match<BiIter>::string_type(rhs.data(), rhs.size())) == 0;
```

```
template <class BiIter>
bool operator!typenametypename__<<IterIter>::value_type const lhs,
const sub_match<BiIter>& rhs)
```

``````

template <class BiIter,, ST,, SA>

 operator operator

const sub_match<BiIter>& lhs,

  const basic_string&

  typename iterator_traits<BiIter>::value_type, ST, SA>& rhs

) {

  Returns: lhs.compare(typename sub_match<BiIter>::string_type(rhs.data(), rhs.size())) == 0;

}

```

```

template <class BiIter, class ST, class SA>

bool operator!=(const sub_match<BiIter>& lhs,

  const basic_string&

  typename iterator_traits<BiIter>::value_type, ST, SA>& rhs

) {

  Returns: !(lhs == rhs);

}

```

```

template <class BiIter, class ST, class SA>

bool operator<(const sub_match<BiIter>& lhs,

  const basic_string&

  typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);

  Returns: lhs.compare(typename sub_match<BiIter>::string_type(rhs.data(), rhs.size())) < 0;

```

```

template <class BiIter, class ST, class SA>

bool operator>(const sub_match<BiIter>& lhs,

const basic_string

typename iterator_traits<BiIter>::value_type, ST, SA>& rhs): rhs < lhs

```

```

template <class BiIter, class ST, class SA>

bool operator>=(const sub_match<BiIter>& lhs,

const basic_string

typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);

  Returns: !(lhs < rhs).

```

```

template <class BiIter, class ST, class SA>

bool operator<=(const sub_match<BiIter>& lhs,

const basic_string

typename iterator_traits<BiIter>::value_type, ST, SA>& rhs);

  Returns: !(rhs < lhs).

```

```

template <class BiIter>

bool operator,typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs) == 0;

```

```

template <class BiIter>

bool operator!=(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs);

  Returns: !(lhs == rhs);

```

```

template <class BiIter>

bool operator>(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs)

  Returns: lhs.compare(rhs) > 0;

```

```

template <class BiIter>

bool operator<=(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs)

  Returns: lhs.compare(rhs) <= 0;

```

```

template <class BiIter>

bool operator>=(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs)

  Returns: rhs < lhs;

```

```

template <class BiIter>

bool operator<(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs)

  Returns: !(rhs < lhs);

```

```

template <class BiIter>

bool operator>(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs)

  Returns: !(lhs < rhs);

```

```

template <class BiIter>

bool operator==(typename iterator_traits<BiIter>::value_type const lhs,

const sub_match<BiIter>& rhs)

  Returns: lhs.compare(typename sub_match<BiIter>::string_type(rhs.data(), rhs.size())) == 0;

```

# 类模板 match_results

1 类 `match_results` 表示表示一类字符序列的类，代表正则表达式匹配的结果。该集合的存储由类模板 `match_results` 的成员函数根据需要分配和释放。

2 `match_results` 模板应满足 2.23.3 中指定的感知分配器的计数器（allocator-aware counter）和序列容器的要求，且仅支持为 `const` 限定的序列容器定义的操作。

3 已解构的 `match_results` 对象没有完全建立的结果状态。当一个完成的正则表达式匹配修改了其对象，导致其结果变为完全建立时，匹配就是就绪的。在未就绪的 `match_results` 对象上调用成员函数的效用是未定义的。

4 存储在索引 0 处的 `sub_match` 对象表示子表达式 0，即匹配项。在这种情况下，`sub_match` 成员 `matched` 始终为 `true`。存储在索引 `n` 处的 `sub_match` 对象表示被匹配的子表达式 `n`。如果子表达式 `n` 参与了正则表达式匹配，则 `sub_match` 成员 `matched` 求值为为 `true`，且成员 `first` 和 `second` 分表示形成该匹配的字符范围 `[first, second]`。否则，`matched` 为 `false`，且 `first` 和 `second` 指向所搜索序列的末尾。[注：表示未参与正则表达式匹配的不同子表达式的 `sub_match` 对象不需要是区分的。-- 结束]

```cpp
namespace std {
template <class Bidirectionaliterator>
  class Allocator = allocator<sub_match<Bidirectionaliterator>>
  class match_results {
  public:
    typedef sub_match<Bidirectionaliterator> value_type;
    typedef value_type const_reference;
    typedef value_type reference;
    typedef implementation_defined const_iterator;
    typedef const_iterator iterator;
    typedef typename iterator_traits<Bidirectionaliterator>::difference_type difference_type;
    typedef typename allocator_traits<Allocator>::size_type size_type;
    typedef Allocator allocator;
    typedef typename iterator_traits<Bidirectionaliterator>::iterator iterator;
    value_type value;
    typedef basic_string<char_type> char_type;
    // 28.10.1, construct/copy/destroy;
    explicit match_results(const Allocator& a = Allocator());
    match_results(const match_results& m);
    match_results(match_results&& m) noexcept;
    match_results& operator=(const match_results& m);
    match_results& operator=(match_results&& m);
    ~match_results();
    // 28.10.2, state;
    bool ready() const;
    // 28.10.3, size;
    size_type size() const;
    size_type max_size() const;
    bool empty() const;
```
```cpp
// 28.10.4. element access:
difference_type length(size_type sub = 0) const;
difference_type position(size_type sub = 0) const;
string_type str(size_type sub = 0) const;
const_reference operator[](size_type n) const;
const_reference prefix() const;
const_reference suffix() const;
const_iterator begin() const;
const_iterator end() const;
const_iterator cbegin() const;
const_iterator const() const;
```
```cpp
// 28.10.5. format:
template <class OutputIter>
OutputIter
format(OutputIter out,
const char* fmt_first, const char* fmt_last,
regex_constants::match_flag_type flags =
regex_constants::format_default) const;
template <class OutputIter, class ST, class SA>
OutputIter
format(OutputIter out,
