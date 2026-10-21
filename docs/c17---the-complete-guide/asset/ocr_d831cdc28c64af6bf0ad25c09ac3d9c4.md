# 9.2.6 Standard Deduction Guides

The C++ standard library introduces a couple of deduction guides with C++17.

# Deduction Guides for Pairs and Tuples

As introduced in the motivation for deduction guides, std::pair needs deduction guides to ensure that class template argument deduction uses the decayed type of the passed argument:³

```
namespace std {
    template<typename T1, typename T2>
    struct pair {
        ...
        constexpr pair(const T1& x, const T2& y);  // take argument by-reference
        ...
    };

    template<typename T1, typename T2>
    pair(T1, T2) -> pair<T1, T2>;  // deduce argument types by-value
}
```

As a consequence, the declaration

```
std::pair p{"hi", "world"};  // takes const char [3] and const char [6]
```

is equivalent to:

```
std::pair<const char*, const char*> p{"hi", "world"};
```

For the variadic class template std::tuple, the same approach is used:

```
namespace std {
    template<typename... Types>
    class tuple {
    public:
        constexpr tuple(const Types&...);  // take arguments by-reference
        template<typename... UTypes> constexpr tuple(UTypes&&...);
        ...
    };

    template<typename... Types>
    tuple(Types...) -> tuple<Types...>;  // deduce argument types by-value
};
```

As a consequence, the declaration:

```
std::tuple t{42, "hello", nullptr};
```

 deduces the type of t as std::tuple<int, const char*, std::nullptr_t>.