# 20 General utilities library [utilities]

# 20.1 General [utilities.general]

1 This Clause describes utilities that are generally useful in C++ programs; some of these utilities are used by other elements of the C++ standard library. These utilities are summarized in Table 41.

Table 41: General utilities library summary [tab:utilities.summary]

| Subclause | Header |
|---|---|
| 20.2 Utility components | <utility> |
| 20.3 Compile-time integer sequences | |
| 20.4 Pairs | |
| 20.5 Tuples | <tuple> |
| 20.6 Optional objects | <optional> |
| 20.7 Variants | <variant> |
| 20.8 Storage for any type | <any> |
| 20.9 Fixed-size sequences of bits | <bitset> |
| 20.10 Memory | <cstdlib>, <memory> |
| 20.11 Smart pointers | <memory> |
| 20.12 Memory resources | <memory_resource> |
| 20.13 Scoped allocators | <scoped_allocator> |
| 20.14 Function objects | <functional> |
| 20.15 Type traits | <type_traits> |
| 20.16 Compile-time rational arithmetic | <ratio> |
| 20.17 Type indexes | <typeindex> |
| 20.18 Execution policies | <execution> |
| 20.19 Primitive numeric conversions | <charconv> |
| 20.20 Formatting | <format> |

# 20.2 Utility components [utility]

# 20.2.1 Header <utility> synopsis [utility.syn]

1 The header <utility> contains some basic function and class templates that are used throughout the rest of the library.

```
#include <compare>          // see 17.11.1
#include <initializer_list>    // see 17.10.2

namespace std {
    // 20.2.2, swap
    template<class T>
        constexpr void swap(T& a, T& b) noexcept(see below);
    template<class T, size_t N>
        constexpr void swap(T (&a)[N], T (&b)[N]) noexcept(is_nothrow_swappable_v<T>);

    // 20.2.3, exchange
    template<class T, class U = T>
        constexpr T exchange(T& obj, U&& new_val);

    // 20.2.4, forward/move
    template<class T>
        constexpr T&& forward(remove_reference_t<T>& t) noexcept;
    template<class T>
        constexpr T&& forward(remove_reference_t<T>&& t) noexcept;
    template<class T>
        constexpr remove_reference_t<T>&& move(T&&) noexcept;
```