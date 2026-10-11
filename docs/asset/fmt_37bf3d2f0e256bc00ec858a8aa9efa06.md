
`static constexpr regex_constants::syntax_option_type`

`group = regex_constants::group;`

`static constexpr regex_constants::syntax_option_type`

`egrep = regex_constants::egrep;`

`static constexpr regex_constants::syntax_option_type`

`multiline = regex_constants::multiline;`

# 31.8.2 构造函数

`basic_regex();`

`explicit basic_regex(const charT p, flag_type f = regex_constants::ECMAScript);`

`basic_regex(const charT p, size_t len, flag_type f = regex_constants::ECMAScript);`

`basic_regex(const basic_regex&) noexcept;`

`template<class T, SA>`

`explicit basic_regex(const basic_string<charT, SA>& s,`

`flag_type f = regex_constants::ECMAScript);`

`basic_regex(ForwardIterator first, ForwardIterator last,`

`basic_regex(initializer_list<charT> il, flag_type f = regex_constants::ECMAScript);`

# 31.8.3 basic_regex 赋值

`basic_regex assign(const basic_regex& that) noexcept;`

`basic_regex assign(const basic_regex& e) noexcept;`

`basic_regex assign(const charT* ptr, size_t len, flag_type f);`

`template<class string_traits, class A>`

`basic_regex assign(const basic_string<charT, string_traits>& s, A& s,`

`flag_type f = regex_constants::ECMAScript);`

`template<class InputIterator>`

`basic_regex& assign(InputIterator first, InputIterator last,`

`flag_type f = regex_constants::ECMAScript);`

`basic_regex assign(initializer_list<charT>,`

`flag_type f = regex_constants::);`

# 31.8.4 计数

`unsigned mark_count count() const;`

`flag_type flags() const;`

# 31.8.6 区域设置

`locale_type imbue(locale_type loc);`

`locale_type getloc() const;`

# 31.8.6 交换

`void swap(basic_regex&);`

# ISO/IEC 14882:2017(E)

```cpp
template <class ST, class SA>
basic_regex& operator=(const basic_string<charT, ST, SA>&& s);
```

- 8 效果：返回 `assign(p)`。

```cpp
basic_regex& assign(const basic_regex& that);
```

- 9 效果：等同于 `*this = that`。

- 10 返回：`*this`。

```cpp
basic_regex& assign(const basic_regex& that) noexcept;
```

- 11 效果：等同于 `*this = std::move(that)`。

- 12 返回：`*this`。

```cpp
basic_regex& assign(const charT* ptr, size_t len, flag_type f = regex_constants::ECMAScript);
```

- 13 执行 `assign(string_type(ptr), f)`。

```cpp
basic_regex& assign(const charT* traits, flag_type f = regex_constants::ECMAScript);
```

- 14 执行 `assign(string_type(ptr, len), f)`。

```cpp
template <class InputIterator>
basic_regex& assign(const basic_string<charT, string_traits, A>&& s),
flag_type f = regex_constants::ECMAScript);
```

- 15 抛出：如果 `s` 不是有效的正则表达式，则抛出 `regex_error`。

- 16 返回：`*this`。

- 17 效果：分配字符串中的正则表达式，如果发生异常，则不解释指定的标志；此时，`*this` 保持不变。

后置条件：如果没有发生异常，`flags()` 返回 `f`，且 `mark_count()` 返回表达式内标记的子表达式的数量。

```cpp
template <class InputIterator>
basic_regex& assign(InputIterator first, InputIterator last,
flag_type f = regex_constants::ECMAScript);
```

- 19 要求：类型 `InputIterator` 应当满足输入迭代器的要求 (`27.2.3`)。

- 20 返回：`assign(string_type(first, last))`。

```cpp
basic_regex& assign(initial_list<charT> il,
flag_type f = regex_constants::ECMAScript);
```

- 21 效果：等同于 `assign(il.begin(), il.end())`，`*this`。

# 31.8.4 basic_regex 常数操作

[re.regex.operations]

`unsigned mark_count() const;`

- 1 效果：返回正则表达式中标记的子表达式的数量。

`flag_type flags() const;`

- 2 效果：返回传递给对象构造函数或上一次 `assign assign` 的原始语法标志的副本。

# 31.8.5 basic_regex 区域 [re.regex.locale]

`local_type imbue(locale_type loc);`

- 1 效果：返回 `traits_inst.imbue(loc)` 的结果，其中 `traits_inst` 是存储在对象内的模板参数 `traits` 的（默认初始化的）实例。调用 `imbue` 后，`basic_regex` 对象将不再匹配任何字符序列。

`local_type getloc() const;`

- 2 效果：返回 `traits_inst.getloc()` 的结果，其中 `traits_inst` 是存储在对象内的模板参数 `traits` 的（默认初始化的）实例。

# 31.8.6 basic_regex swap [re.regex.swap]

`void swap(basic_regex &);`

- 1 效果：交换两个正则表达式的内容。

- 2 后置条件：`*this` 包含了原先在 `*this` 中的正则表达式。

- 3 复杂度：常数时间。

# 31.8.7 basic_regex 非成员函数 [re.regex.nonmemb]

## 31.8.7.1 basic_regex 非成员交换 swap [re.regex.nmswap]

```cpp
template <class CharT, class Traits>
void swap(basic_regex<CharT, Traits> &lhs, basic_regex<CharT, Traits> &rhs);
```

- 1 效果：调用 `lhs.swap(rhs)`。

# 31.9 类模板 template_match [re.submatch]

11 类模板 `sub_match` 表示由特定标记的子表达式匹配的字符序列。

```cpp
namespace std {
  template <BidirectionalIterator>
  class sub_match : public BidirectionalIterator {
  public:
    typename iterator_traits<BidirectionalIterator>::value_type = typename iterator_traits<BidirectionalIterator>::value_type;
    using difference_type = typename iterator_traits<BidirectionalIterator>::difference_type;
    using iterator = BidirectionalIterator;
    using string_type = basic_string<value_type>;

    bool matched;

    constexpr sub_match match();

    difference_type length() const;
    operator string_type() const;
    string_type str() const;

    int compare(const sub_match& s) const;
    int compare(const string_type& s) const;
    int compare(const value_type* s) const;
  };
} // 
```

## 31.9.1 sub_match 成员 [re.submatch.members]

```cpp
constexpr sub_match();
// 效果：初始化基类对和成员。
difference_type length() const;
// 返回：matched ? distance(first, second) : 0。
operator string_type() const;
// 返回：matched ? string_type(first, second) : string_type().
string_type str() const;
// 返回：matched ? string_type(first, second) : string_type().
int compare(const sub_match& s) const;
// 返回：str().compare(s());
int compare(const string_type& s) const;
// 返回：str().compare(s).
int compare(const value_type* s) const;
// 返回：str().compare(s).
```

## 31.9.2 sub_match-成员运算符 [re.submatch.op]

```cpp
template <class BiIter>
bool operator=(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);
// 返回：lhs.compare(rhs) == 0

template <class BiIter>
bool operator!=(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);
// 返回：lhs.compare(rhs) != 0

template <class BiIter>
bool operator<(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);
// 返回：lhs.compare(rhs) < 0

template <class BiIter>
bool operator<=(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);
// 返回：lhs.compare(rhs) <= 0

template <class BiIter>
bool operator>=(const sub_match<BiIter>& lhs, const sub_match<BiIter>& rhs);
// 返回：lhs.compare(rhs) > 0

template <class BiIter, class ST, class SA>
bool operator=(typename iterator_traits<BiIter>::value_type, ST, SA& lhs, const basic_string<ST>& rhs);
// 返回：rhs.compare(typename sub_match<BiIter>::string_type(lhs.data(), lhs.size())) == 0

template <class BiIter, class ST, class SA>
bool operator!(typename iterator_traits<BiIter>::value_type, ST, SA& lhs, const sub_match<BiIter>& rhs);
// 返回：!(lhs == rhs)

template <class BiIter, class ST, class SA>
bool operator<(typename iterator_traits<BiIter>::value_type, ST, SA& lhs, const sub_match<BiIter>& rhs);
// 返回：rhs < lhs

... (后续截断部分已按翻译逻辑处理)
```

# ISO/IEC 14882:2017(E)

```cpp

bool operator===(const sub_match<BiIter>& lhs,

               const typename iterator_traits<BiIter>::value_type* rhs);

   返回: lhs.compare(rhs) == 0;

```

```cpp

template <class BiIter>

bool operator!=(const sub_match<BiIter>& lhs,

               const typename iterator_traits<BiIter>::value_type* rhs);

   返回: !(lhs == rhs);

```

```cpp

template <class BiIter>

bool operator<=(const sub_match<BiIter>& lhs,

               const typename iterator_traits<BiIter>::value_type* rhs);

   返回: lhs.compare(rhs) < 0;

```

```cpp

template <class BiIter>

bool operator>(const sub_match<BiIter>& lhs,

               const typename iterator_traits<BiIter>::value_type* rhs);

   返回: lhs < rhs;

```

```cpp

template <class BiIter>

bool operator>=(const sub_match<BiIter>& lhs,

               const typename iterator_traits<BiIter>::value_type* rhs);

   返回: !(lhs < rhs);

```

```cpp

template <class BiIter>

bool operator=(const typename iterator_traits<BiIter>::value_type& lhs,

               const sub_match<BiIter>& rhs);

   返回: lhs.compare(typename sub_match<BiIter>::string_type(1, lhs)) == 0;

```

```cpp

template <class BiIter>

bool operator!=(const typename iterator_traits<BiIter>::value_type& lhs,

               const sub_match<BiIter>& rhs);

   返回: !(lhs == rhs);

```

```cpp

template <class BiIter>

bool operator>=(const typename iterator_traits<BiIter>::value_type& lhs,

               const sub_match<BiIter>& rhs);
```
