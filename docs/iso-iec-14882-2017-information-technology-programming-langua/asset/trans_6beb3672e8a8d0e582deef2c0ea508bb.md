
# ISO/IEC 14882:2017(E)

```cpp
using is_transparent = unspecified;

template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) < std::forward<U>(u));

    Returns: std::forward<T>(t) < std::forward<U>(u).
```

## 23.14.7.4 类类模板 less [comparisons.less]

```cpp
template <class T = void> struct less {
    constexpr bool operator()(const T& x, const T& y) const;
};

constexpr bool operator()(const T& x, const T& y) const {
    Returns: x < y;
}

template <> struct less<void> {
    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) < std::forward<U>(u));

    using is_transparent = unspecified;

    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) < std::forward<U>(u));
    Returns: std::forward<T>(t) < std::forward<U>(u);
};
```

## 23.14.7.5 类类模板 greater_equal [comparisons.greater_equal]

```cpp
template <class T = void> struct greater_equal {
    constexpr bool operator()(const T& x, const T& y) const;
};

constexpr bool operator()(const T& x, const T& y) const {
    Returns: x >= y;
}

template <> struct greater_equal<void> {
    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) >= std::forward<U>(u));

    using is_transparent = unspecified;

    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) >= std::forward<U>(u));
    Returns: std::forward<T>(t) >= std::forward<U>(u);
};
```

## 23.14.7.6 类类模板 less_equal [comparisons.less_equal]

```cpp
template <class T = void> struct less_equal {
    constexpr bool operator()(const T& x, const T& y) const;
};

constexpr bool operator()(const T& x, const T& y) const {
    Returns: x <= y;
}

template <> struct less_equal<void> {
    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) <= std::forward<U>(u));

    using is_transparent = unspecified;

    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) <= std::forward<U>(u));
    Returns: std::forward<T>(t) <= std::forward<U>(u);
};
```

## 23.14.8 逻辑操作

- 1. 标准库为语言中所有逻辑操作的基础函数类（8.14, 15.8.3）。

### 23.14.8.1 类类模板 logical_and

```cpp
template <class T = void> struct logical_and {
    constexpr bool operator()(const T& x, const T& y) const;
};

constexpr bool operator()(const T& x, const T& y) const {
    Returns: x && y;
}

template <> struct logical_and<void> {
    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) && std::forward<U>(u));

    using is_transparent = unspecified;

    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) && std::forward<U>(u));
    Returns: std::forward<T>(t) && std::forward<U>(u);
};
```

### 23.14.8.2 类类模板 logical_or

```cpp
template <class T = void> struct logical_or {
    constexpr bool operator()(const T& x, const T& y) const;
};

constexpr bool operator()(const T& x, const T& y) const {
    Returns: x || y;
}

template <> struct logical_or<void> {
    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) || std::forward<U>(u));

    using is_transparent = unspecified;

    template <class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) || std::forward<U>(u));
    Returns: std::forward<T>(t) || std::forward<U>(u);
};
```

### 23.14.8.3 类类模板 logical_not [logical.operations.not]

```cpp
template<class T = void> struct logical_not {
    constexpr operator()(const T& x) const;
};

constexpr operator()(const T& x) const {
    Returns: x;
}

template <> struct logical_not<void> {
    template<class T> constexpr operator()(T& t) const
    -> decltype(std::forward<T>(t));

    using is_transparent = unspecified;

    template<class T> constexpr operator()(T& t) const
        -> decltype(std::forward<T>(t));

    Returns std::forward<T>(t);
};
```

## 23.14.9 位操作 [bitwise.operations]

- 1 标准库为语言中所有位运算符提供了基础函数对象类（8.11, 8.13, 8.12, 8.31）。

### 23.14.9.1 类类模板 bit_and [bitwise.operations.and]

```cpp
template<class T = void> struct bit_and {
    constexpr operator()(const T& x, const T& y) const;
};

constexpr operator()(const T& x, const T& y) const {
    Returns: x & y;
}

template <> struct bit_and<void> {
    template<class T, class U> constexpr operator()(T& t, U& u) const
    -> decltype(std::forward<T>(t) & std::forward<U>(u));

    using is_transparent = unspecified;

    template<class T, class U> constexpr operator()(T& t, U& u) const
        -> decltype(std::forward<T>(t) & std::forward<U>(u));

    Returns std::forward<T>(t) & std::forward<U>(u);
};
```

### 23.14.9.2 类类模板 bit_or [bitwise.operations.or]

```cpp
template<class T = void> struct bit_or {
    constexpr operator()(const T& x, const T& y) const;
};

constexpr operator()(const T& x, const T& y) const {
    Returns: x | y;
}

template <> struct bit_or<void> {
    template<class T, class U> constexpr operator()(T& t, U& u) const
    -> decltype(std::forward<T>(t) | std::forward<U>(u));

    using is_transparent = unspecified;

    template<class T, class U> constexpr operator()(T& t, U& u) const
        -> decltype(std::forward<T>(t) | std::forward<U>(u));

    Returns std::forward<T>(t) | std::forward<U>(u);
};
```

### 23.14.9.3 类类模板 bit_xor [bitwise.operations.xor]

```cpp
template<class T = void> struct bit_xor {
    constexpr operator()(const T& x, const T& y) const;
};

constexpr operator()(const T& x, const T& y) const {
    Returns: x ^ y;
}

template <> struct bit_xor<void> {
    template<class T, class U> constexpr operator()(T& t, U& u) const
    -> decltype(std::forward<T>(t) ^ std::forward<U>(u));

    using is_transparent = unspecified;

    template<class T, class U> constexpr operator()(T& t, U& u) const
        -> decltype(std::forward<T>(t) ^ std::forward<U>(u));

    Returns std::forward<T>(t) ^ std::forward<U>(u);
};
```

### 23.14.9.4 类类模板 bit_and_equal [bitwise.operations.and_equal]

```cpp
template<class T = void> struct bit_and_equal {
    constexpr operator()(const T& x, const T& y) const;
};

constexpr operator()(const T& x, const T& y) const {
    Returns: x == y;
}

template <> struct bit_and_equal<void> {
    template<class T, class U> constexpr operator()(T& t, U& u) const
    -> decltype(std::forward<T>(t) == std::forward<U>(u));

    using is_transparent = unspecified;

    template<class T, class U> constexpr operator()(T& t, U& u) const
        -> decltype(std::forward<T>(t) == std::forward<U>(u));

    Returns std::forward<T>(t) == std::forward<U>(u);
};
```
