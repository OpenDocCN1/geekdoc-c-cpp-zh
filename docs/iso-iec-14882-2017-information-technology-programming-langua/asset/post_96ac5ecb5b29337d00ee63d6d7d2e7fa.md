
# ISO/IEC 14882:2017(E)

Table 135 — Effects of regex_match algorithm (continued)

| Element | Value |
| --- | --- |
| m[0].matched | true |
| m[n].first | For all integers 0 < n < m.size(), the start of the sequence that matched sub-expression n. Alternatively, if sub-expression n did not participate in the match, then last. |
| m[n].second | For all integers 0 < n < m.size(), the end of the sequence that matched sub-expression n. Alternatively, if sub-expression n did not participate in the match, then last. |
| m[n].matched | For all integers 0 < n < m.size(), true if sub-expression n participated in the match, false otherwise. |

```cpp
template <class BidirectionalIterator, class charT, class traits>
bool regex_match(BidirectionalIterator first, BidirectionalIterator last,
                const basic_regex<charT, traits>& e,
                regex_constants::match_flag_type flags = regex_constants::match_default);
```

4 Effects: Behaves "as if" by constructing an instance of match_results<BidirectionalIterator> what, and returning the result of regex_match(first, last, what, e, flags).

```cpp
template <class ST, class Alloc>
bool regex_match(const charT& str, Allocator<charT>& m,
                match_results<basic_string<charT, Alloc>>(
                const basic_regex<charT, traits>& e,
                regex_constants::match_flag_type flags = regex_constants::match_default);
```

5 Returns: regex_match(str, str + char_traits<charT>::length(str), m, e).

```cpp
template <class ST, class SA, class charT, class traits>
bool regex_match(const basic_string<charT, SA>& str, SA& s,
                match_results<basic_string<charT, SA>>(traits::length(str), SA,
                Allocator<charT>& a),
                const basic_regex<charT, traits>& e,
                regex_constants::match_flag_type flags = regex_constants::match_default);
```

6 Returns: regex_match(str.begin(), s.end(), m, e).

```cpp
template <class charT, class traits>
bool regex_match(const charT& str, charT& e,
                const basic_regex<charT, traits>& e,
                regex_constants::match_flag_type flags = regex_constants::match_default);
```

7 Returns: regex_match(str, str + char_traits<charT>::length(str), e).

```cpp
template <class ST, class SA, class charT, class traits>
bool regex_match(const basic_string<charT, SA>& str, SA& s,
                const basic_regex<charT, traits>& e,
                regex_constants::match_flag_type flags = regex_constants::match_default);
```

8 Returns: regex_match(str.begin(), s.end(), e).

# ISO/IEC 14882:2017(E)

## 31.11.3 regex_search

```cpp
template <class BidirectionalIterator, class Allocator, class CharT, class traits>
bool regex_search(BidirectionalIterator first, BidirectionalIterator last,
match_results<BidirectionalIterator, Allocator>& m,
const basic_regex<CharT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default);
```

* Requires: BidirectionalIterator shall satisfy the requirements of BidirectionalIterator (27.6).
* Effects: Determines whether there is sub-sequence [first, last) that matches the regular expression. The parameter flags is used to control how the expression is matched against the character sequence. Returns true if such sequence exists, false otherwise.
* Postconditions: m.ready() == true. If the function returns false, then the effect on parameter m is unspecified unless m.size() and m.empty() returns true. Otherwise the effects on parameter m are given in Table 136.

Table 136 — Effects of regex_search

| Element | Value |
| --- | --- |
| m.size() | 1 + e.mark_count() |
| m.empty() | false |
| m.prefix().first | m[0].first |
| m.prefix().matched | m.prefix().first != m.prefix().second |
| m.suffix().first | m[0].second |
| m.suffix().second | last |
| m.suffix().matched | m.suffix().first != m.suffix().second |
| m[0].first | The start of the sequence of characters that matched the regular expression |
| m[0].second | The end of the sequence of characters that matched the regular expression |
| m[0].matched | true |
| m[n].first | For all integers 0 < n < m.size(), the start of the sequence that matched sub-expression n. Alternatively, if sub-expression n did not participate in the match, then last. |
| m[n].second | For all integers 0 < n < m.size(), the sequence that matched sub-expression n. Alternatively, if sub-expression n did not participate in the match, then last. |
| m[n].matched | For all integers 0 < n < m.size(), true if sub-expression n participated in the match, false otherwise. |

```cpp
template <class CharT, class Allocator, class traits>
bool regex_search(const CharT* str, match_results<const CharT*, Allocator>& m,
const basic_regex<CharT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default);
```

* Returns: regex_search(str, str + char_traits<CharT>::length(str), m, e, flags).

```cpp
template <class ST, class SA, class Allocator, class charT, class traits>
bool regex_search(const basic_string<charT, SA>& s, match_results<typename basic_string<charT, SA>::iterator, Allocator> const basic_regex<traits>& e, const regex_constants::match_flag_type flags = regex_constants::match_default)
```

5 regex_search(s.begin(), s.end(), e, flags).

```cpp
template <class BidirectionalIterator, class charT, class traits>
bool regex_search(BidirectionalIterator first, BidirectionalIterator last, const regex<traits>& e, const regex_constants::match_flag_type flags = regex_constants::match_default)
```

* 6 Effects: Behaves as "if" by constructing an object of type match_results<BidirectionalIterator> and returning regex_search(first, last, e, flags).

```cpp
template <class charT, class traits>
bool regex_search(const basic_regex<charT, traits>& e, const regex_constants::match_flag_type flags = regex_constants::match_default)
```

* 7 regex_search(str, str + char_traits<charT>::length(str), e).

```cpp
template <class ST, class SA, class charT, class traits>
bool regex_search(const basic_string<charT, SA>& s, const basic_regex<charT, traits>& e,
regex_constants::match_flag_type flags = regex_constants::match_default)
```

regex_search(s.begin(), s.end(), e).

## 31.11.4 regex_replace

```cpp
template <class OutputIterator, class traits>
bool regex_replace(OutputIterator out, BidirectionalIterator first, BidirectionalIterator last, const basic_regex<traits>& e, regex_constants::match_flag_type flags = regex_constants::match_default);
```

```cpp
template <class OutputIterator, class traits>
bool regex_replace(OutputIterator out, BidirectionalIterator first, BidirectionalIterator last, const basic_regex<traits>& e, regex_constants::match_flag_type flags = regex_constants::match_default);
```

* 1 Effects: Constructs a regex_iterator<BidirectionalIterator> i and uses it to iterate through all the matches within [first, last). If no matches are found, out = copy(first, last).
(1.1) If !(flags & regex_constants::format_copy), out = copy(m.prefix().first, m.prefix().second, out).
(1.2) Then calls out = m.format(out, fmt) for the first match, if !(flags & regex_constants::format_copy), out = copy(m.suffix().first, m.suffix().second, out) for the last match.

* 2 Effects: Constructs an empty string of type basic_string<charT, ST> and calls: regex_replace(back_inserter(result), s.begin(), s.end(), e, fmt, flags).
* 3 Effects: Constructs an empty string of type basic_string<charT> and calls: regex_replace(back_inserter(result), s, s + char_traits<charT>::length(s), e, fmt, flags).
* 4 Returns: result.

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
