```
constexpr auto operator()(T&& t, U&& u) const;
```

**Preconditions:** If the expression `std::forward<T>(t) <=> std::forward<U>(u)` results in a call to a built-in operator `<=>` comparing pointers of type P, the conversion sequences from both T and U to P are equality-preserving ([18.2]).

**Effects:**

+   — If the expression `std::forward<T>(t) <=> std::forward<U>(u)` results in a call to a built-in operator `<=>` comparing pointers of type P, returns `strong_ordering::less` if (the converted value of) t precedes u in the implementation-defined strict total order over pointers ([3.24]), `strong_ordering::greater` if u precedes t, and otherwise `strong_ordering::equal`.
+   
+   — Otherwise, equivalent to: `return std::forward<T>(t) <=> std::forward<U>(u);`

# 20.14.9  Concept-constrained comparisons                                      [range.cmp]

In this subclause, *BUILTIN-PTR-CMP(T, op, U)* for types T and U and where *op* is an equality (7.6.10) or relational operator (7.6.9) is a boolean constant expression. *BUILTIN-PTR-CMP(T, op, U)* is true if and only if *op* in the expression `decltype<T>() op declval<U>()` resolves to a built-in operator comparing pointers.

```
struct ranges::equal_to {
  template<class T, class U>
    requires equality_comparable_with<T, U> || BUILTIN-PTR-CMP(T, ==, U)
  constexpr bool operator()(T&& t, U&& u) const;

  using is_transparent = unspecified;
};
```

**Preconditions:** If the expression `std::forward<T>(t) == std::forward<U>(u)` results in a call to a built-in operator `==` comparing pointers of type P, the conversion sequences from both T and U to P are equality-preserving ([18.2]).

**Effects:**

+   — If the expression `std::forward<T>(t) == std::forward<U>(u)` results in a call to a built-in operator `==` comparing pointers: returns `false` if either (the converted value of) t precedes u or u precedes t in the implementation-defined strict total order over pointers ([3.24]) and otherwise `true`.
+   
+   — Otherwise, equivalent to: `return std::forward<T>(t) == std::forward<U>(u);`

```
struct ranges::not_equal_to {
  template<class T, class U>
    requires equality_comparable_with<T, U> || BUILTIN-PTR-CMP(T, ==, U)
  constexpr bool operator()(T&& t, U&& u) const;

  using is_transparent = unspecified;
};
```

`operator()` has effects equivalent to:

`return !ranges::equal_to{}(std::forward<T>(t), std::forward<U>(u));`

```
struct ranges::greater {
  template<class T, class U>
    requires totally_ordered_with<T, U> || BUILTIN-PTR-CMP(U, <, T)
  constexpr bool operator()(T&& t, U&& u) const;

  using is_transparent = unspecified;
};
```

`operator()` has effects equivalent to:

`return ranges::less{}(std::forward<U>(u), std::forward<T>(t));`

```
struct ranges::less {
  template<class T, class U>
    requires totally_ordered_with<T, U> || BUILTIN-PTR-CMP(T, <, U)
  constexpr bool operator()(T&& t, U&& u) const;
```