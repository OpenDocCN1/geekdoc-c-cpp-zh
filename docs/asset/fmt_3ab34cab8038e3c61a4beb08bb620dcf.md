
`match_results<BidirectionalIterator, Allocator>& m,`

`const basic_regex<CharT, traits>& e,`

`regex_constants::match_flag_type flags = regex_constants::match_default);`

* 要求：`BidirectionalIterator` 应当满足 `BidirectionalIterator` 的要求 (27.6)。
* 效果：确定是否存在匹配正则表达式的子序列 `[first, last)`。参数 `flags` 用于控制表达式如何与字符序列进行匹配。如果存在此种序列，则返回 `true`，否则返回 `false`。
* 后置条件：`m.ready() == true`。如果函数返回 `false`，则对参数 `m` 的影响是不定义的，除非 `m.size()` 和 `m.empty()` 返回 `true`。否则，对参数 `m` 的影响见表 136。

表 136 — `regex_search` 的影响

| 元素 | 值 |
| --- | --- |
| `m.size()` | 1 + `e.mark_count()` |
| `m.empty()` | false |
| `m.prefix().first` | `m[0].first` |
| `m.prefix().matched` | `m.prefix().first != m.prefix().second` |
| `m.suffix().first` | `m[0].second` |
| `m.suffix().second` | last |
| `m.suffix().matched` | `m.suffix().first != m.suffix().second` |
| `m[0].first` | 匹配正则表达式的字符序列的起始位置 |
| `m[0].second` | 匹配正则表达式的序列的结束位置 |
| `m[0].matched` | true |
| `m[n].first` | 对于所有整数 0 < n < `m.size()`，匹配子表达式 n 的序列的起始位置。或者，如果子表达式 n 未参与匹配，则为 last。 |
| `m[n].second` | 对于所有整数 0 < n < `m.size()`，匹配子表达式 n 的序列的结束位置。或者，如果子表达式 n 未参与匹配，则为 last。 |
| `m[n].matched` | 对于所有整数 0 < n < `m.size()`，如果子表达式 n 参与了匹配，则为 true，否则为 false。 |

```cpp
template <class CharT, class Allocator, class traits>
bool regex_search(const CharT* str, match_results<CharT*, Allocator>& m,
const basic_regex<CharT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default);
```

* 返回：`regex_search(str, str + char_traits<CharT>::length(str), m, e)`。

```cpp
template <class ST, class SA, class CharT, class traits>
bool regex_search(const basic_string<charT, SA>& s, match_results<basic_string<charT, SA>>::iterator, Allocator> const basic_regex<charT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default)
```

`regex_search(s.begin(), s.end(), e).`

```cpp
template <class BidirectionalIterator, class charT, class traits>
bool regex_search(BidirectionalIterator first, BidirectionalIterator last, const basic_regex<charT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default)
```

* 6 效果：通过构造一个 `match_results<BidirectionalIterator>` 类型的对象，并返回 `regex_search(first, last, e)` 的结果。

```cpp
template <class charT, class traits>
bool regex_search(const charT& str, const basic_regex<charT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default)
```

* 7 返回：`regex_search(str, str + char_traits<charT>::length(str), e)`。

## 31.11.4 regex_replace

```cpp
template <class OutputIterator, class traits>
bool regex_replace(OutputIterator out, BidirectionalIterator first, BidirectionalIterator last, const basic_regex<charT>& e, regex_constants::match_flag_type flags = regex_constants::match_default);
```

```cpp
template <class OutputIterator, class traits>
bool regex_replace(OutputIterator out, BidirectionalIterator first, BidirectionalIterator last, const basic_regex<charT>& e, regex_constants::match_flag_type flags = regex_constants::match_default);
```

* 1 效果：构造一个 `regex_iterator<BidirectionalIterator> i` 并使用它遍历 `[first, last)` 内的所有匹配项。如果没有找到匹配项，则 `out = copy(first, last)`。
(1.1) 如果 `!(flags & regex_constants::format_copy)`，则 `out = copy(m.prefix().first, m.prefix().second, out)`。
(1.2) 然后对第一个匹配项调用 `out = m.format(out, fmt)`，如果 `!(flags & regex_constants::format_copy)`，则对最后一个匹配项调用 `out = copy(m.suffix().first, m.suffix().second, out)`。

* 2 效果：构造一个 `basic_string<charT, ST>` 类型的字符串，并调用 `regex_replace(back_inserter(result), s.begin(), s.end(), e, fmt, flags)`。
* 3 效果：构造一个 `basic_string<charT>` 类型的字符串，并调用 `regex_replace(back_inserter(result), s, s + char_traits<charT>::length(s), e, fmt, flags)`。
* 4 返回：`result`。

```cpp
template <class traits, class charT, class ST, class SA>
basic_string<charT>
regex_replace(const basic_regex<charT, traits>& e,
    const basic_string<charT, ST, SA>& s,
    const charT& fmt,
    regex_constants::match_flag_type flags = regex_constants::match_default)
```

```cpp
template <class traits, class charT, class ST, class SA>
basic_string<charT>
regex_replace(const basic_regex<charT, traits>& e,
    const basic_string<charT, SA>& s,
    const charT& fmt,
    regex_constants::match_flag_type flags = regex_constants::match_default);
```

# ISO/IEC 14882:2017(E)

## 31.12 正则表达式迭代器

### 31.12.1 类模板 `regex_iterator`

`regex_iterator` 类是一个迭代器适配器。它通过枚举现有迭代器序列中所有出现的正则表达式匹配项，代表了该序列的新视图。`regex_iterator` 使用 `regex_search` 在其构造时目标序列中查找连续的正则表达式匹配项。迭代器在构造时会存储一个 `match_results<BidirectionalIterator>` 值。如果到达序列末尾（`regex_search` 返回 `false`），则迭代器将等于序列结束的迭代器值。默认构造函数构造一个序列结束迭代器（未定义），它是唯一允许用于结束位置的迭代器。在序列结束迭代器上执行 `regex_iterator` 操作的结果未定义。对于其他迭代器值，返回一个 `const match_results<BidirectionalIterator>&`。返回 `operator*` 在 `match_results<BidirectionalIterator>` 上的结果。可以向 `regex_iterators` 中存储内容。两个非结束序列的迭代器是相等的。两个结束序列迭代器即使从相同的参数构造，也不相等的。

```cpp
namespace std {
    template <BidirectionalIterator>
    typename iterator_traits<BidirectionalIterator>::value_type;
    class traits : regex_traits<BidirectionalIterator>;
    class regex_iterator {
    public:
        regex_iterator() = basic_regex<charT, traits>
        using forward_iterator;
        using iterator_category = match_results<BidirectionalIterator>;
        using value_type = pdiff_t;
        using pointer = const value_type*;
        using reference = const value_type&;
        regex_iterator()
        _iterator();
        regex_iterator(const BidirectionalIterator a, BidirectionalIterator b,
                       const regex_type* re,
                       const regex_constants::match_type m = regex_constants::match_default);
        regex_iterator(const BidirectionalIterator a, BidirectionalIterator,
                       const regex_constants::match_type flags = regex_constants::match_default) = delete;
                       const regex_type* re);
        regex_iterator(const regex_iterator& iter);
        regex_iterator& operator=(const regex_iterator& iter) = default;
        bool operator==(const regex_iterator& other) const;
        bool operator!=(const regex_iterator& other) const;
        const value_type& operator*() const;
        const value_type* operator->() const;
        regex_iterator& operator++();
        regex_iterator operator++(int);
    private:
        BidirectionalIterator begin; // exception only
        BidirectionalIterator end; // exception only
        const regex_type* prege; // exception only
        const regex_constants::match_type flags; // exception only
        match_results<BidirectionalIterator> match; // exception only
};
```

如果类型为 `regex_iterator` 的对象不是序列结束迭代器，且当 `match[0].matched == true` 且 `match[0].first == match[0].second` 时，它持有一个零长度的匹配。[注：例如，当正则表达式的匹配模式仅由断言（如 `^`、`\D`、`\b`、`\B`）组成时可能会发生]

### 31.12.1.1 regex_iterator 构造函数 [re.regiter.cnstr]

```cpp
regex_iterator();
```

- 1 效果：构造一个序列结束迭代器。`regex_iterator(BidirectionalIterator a, BidirectionalIterator b, const regex_type &re, const constants::match_type m = constants::match_default);`
- 2 初始化：将 `begin` 和 `end` 设置为 `a` 和 `b`，具体设置 `regex` 为 `re`，`flags` 为 `m`，然后调用 `regex_search(begin, end, match, *flags)`。如果为 `false`，返回序列结束迭代器。

### 31.12.1.2 regex_iterator 比较 [re.regiter.comp]

```cpp
bool operator!=(const regex_iterator& right) const;
```

- 1 返回：如果 `*this` 和 `right` 都是序列结束迭代器，或者满足以下所有条件，返回 `true`：
(1) `begin == right.begin`,
(2) `end == right.end`,
(3) `prex == right.prex`,
(4) `flags == right.flags` 以及
(5) `match[0] == right.match[0]`；否则返回 `false`。
- 2 返回：`(*this == right)`。（注：OCR文本中的 `bool operator=(const regex_iterator& right) const;` 根据逻辑和后续的 `operator==` 可能是 `operator!=` 的误写。）

### 31.12.1.3 regex_iterator 解引用 [re.regiter.deref]

```cpp
const value_type& operator*() const;
```

- 1 返回：`match`.

```cpp
const value_type* operator->() const;
```

- 2 返回：`&match`.

### 31.12.1.4 regex_iterator 自增 [re.regiter.incr]

```cpp
regex_iterator& operator++();
```
