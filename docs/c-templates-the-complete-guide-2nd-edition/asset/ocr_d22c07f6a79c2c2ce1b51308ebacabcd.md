```
```cpp
int value = 0;
int multiplier = 1;
for (std::size_t i = 0; i < N - offset; ++i) {
  if (arr[N-1-i] != '\'' ) { //ignore separating single quotes (e.g. in 1'000)
    value += toInt(arr[N-1-i]) * multiplier;
    multiplier *= base;
  }
}
return value;
}

// literal operator: parse integral literals with suffix _c as
// sequence of chars:
template<char... cs>
constexpr auto operator""_c() {
  return CTValue<int, parseInt<sizeof...(cs)>([cs...]>{};
}
```
```

Here we take the advantage of the fact that, for numeric literals, we can use the literal operator to deduce each character of the literal as its own template parameter (see Section 15.5.1 on page 277 for details). We pass the characters to a `constexpr` helper function `parseInt()` that computes the value of the character sequence at compile time and yields it as `CTValue`. For example:

+   - `42_c` yields `CTValue<int, 42>`
+   - `0x815_c` yields `CTValue<int, 2069>`
+   - `0b1111’1111_c` yields `CTValue<int, 255>`¹¹

Note that the parser does not handle floating-point literals. For them, the assertion results in a compile-time error because it is a run-time feature that can’t be used in compile-time contexts.

With this, we can use tuples as follows: [Click here to view code image](#)

```
```cpp
auto t = makeTuple(0, '1', 2.2f, std::string{"hello"});
auto c = t[2_c];
auto d = t[3_c];
```
```

This approach is used by Boost.Hana (see [BoostHana]), a metaprogramming library suited for computations on both types and values.

# 25.7 Afternotes

Tuple construction is one of those template applications that appears to have been independently attempted by many programmers. The Boost.Tuple Library [BoostTuple] became one of the most popular formulations of tuples in C++, and