# 24 Ranges library

# [ranges]

# 24.1 General

# [ranges.general]

1 This Clause describes components for dealing with ranges of elements.

2 The following subclauses describe range and view requirements, and components for range primitives as summarized in Table 90.

Table 90: Ranges library summary [tab:range.summary]

|  | Subclause | Header |
|---|---|---|
| 24.3 | Range access | <ranges> |
| 24.4 | Requirements |  |
| 24.5 | Range utilities |  |
| 24.6 | Range factories |  |
| 24.7 | Range adaptors |  |

# 24.2 Header <ranges> synopsis

# [ranges.syn]

```
#include <compare>          // see 17.11.1
#include <initializer_list>    // see 17.10.2
#include <iterator>             // see 23.2

namespace std::ranges {
    inline namespace unspecified {
        // 24.3, range access
        inline constexpr unspecified begin = unspecified;
        inline constexpr unspecified end = unspecified;
        inline constexpr unspecified cbegin = unspecified;
        inline constexpr unspecified cend = unspecified;
        inline constexpr unspecified rbegin = unspecified;
        inline constexpr unspecified rend = unspecified;
        inline constexpr unspecified crbegin = unspecified;
        inline constexpr unspecified crend = unspecified;

        inline constexpr unspecified size = unspecified;
        inline constexpr unspecified ssize = unspecified;
        inline constexpr unspecified empty = unspecified;
        inline constexpr unspecified data = unspecified;
        inline constexpr unspecified cdata = unspecified;
    }

    // 24.4.2, ranges
    template<class T>
        concept range = see below;

    template<class T>
        inline constexpr bool enable_borrowed_range = false;

    template<class T>
        concept borrowed_range = see below;

    template<class T>
        using iterator_t = decltype(ranges::begin(declval<T&>()));
    template<range R>
        using sentinel_t = decltype(ranges::end(declval<R&>()));
    template<range R>
        using range_difference_t = iter_difference_t<iterator_t<R>>;
```