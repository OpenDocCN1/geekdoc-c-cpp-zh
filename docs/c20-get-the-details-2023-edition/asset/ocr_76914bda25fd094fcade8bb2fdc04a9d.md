```
44
45   }
```

The classical way to solve this issue is to bring `std::begin` into the scope with a so-called using declaration (line 26). Thanks to ranges, you can directly use `std::ranges::begin` (line 31). `std::ranges::begin` considers both implementations of `begin`: the free version and the member function.

Finally, let me write about safety.

# 5.1.8.3 Safety

The ranges library provides the expected operation to iterate through or access the range directly. They need the header `<ranges>`.

Iterators

| Operation | Description |
| --- | --- |
| std::ranges::begin | Returns an iterator to the beginning of the range |
| std::ranges::end | Returns a sentinel indicating the end of the range |
| std::ranges::cbegin | Returns an iterator to the beginning of the read-only range |
| std::ranges::cend | Returns a sentinel indicating the end of the read-only range |
| std::ranges::rbegin | Returns a reverse iterator to the end of the range |
| std::ranges::rend | Returns a sentinel (reverse) indicating the beginning of the range |
| std::ranges::crbegin | Returns a reverse iterator to the end of the read-only range |
| std::ranges::crend | Returns a sentinel (reverse) indicating the beginning of the read-only range |
| std::ranges::data | Returns a pointer to the beginning of the contiguous range |
| std::ranges::cdata | Returns a pointer to the beginning of the contiguous read-only range |

When you use these operations to access the underlying range, there's a big difference. The compilation fails when you use the range access on the `std::ranges` variant if the argument is an rvalue⁹. On the contrary, using the same operation from the classical `std` namespace is undefined

> ⁹)https://en.cppreference.com/w/cpp/language/value_category