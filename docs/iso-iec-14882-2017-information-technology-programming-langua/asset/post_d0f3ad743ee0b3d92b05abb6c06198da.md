
# ISO/IEC 14882:2017(E)

template<class... UnboundArgs>
 R operator()(UnboundArgs&&... unbound_args) cu-qual;
-- end note

## 23.14.4 Function template invoke [func.invoke]

```cpp
template <class F, class... Args>
invoke_result_t<F, Args...> invoke(F&& f, Args&&... args)
noexcept(is_nothrow_invocable_v<F, Args...>)
Returns: INVOKE(std::forward<F>(f), std::forward<Args>(args)...)) (23.14.3).
```

## 23.14.5 Class template reference_wrapper [refwrap]

```cpp
namespace std {
  template <class T> class reference_wrapper {
  public:
    // types
    using type = T;

    // construct/copy/destroy
    reference_wrapper(T&&) noexcept;
    reference_wrapper(T&&) = delete; // do not bind to temporary objects
    reference_wrapper(const reference_wrapper& x) noexcept;

    // assignment
    reference_wrapper& operator=(const reference_wrapper& x) noexcept;

    // access
    operator T() const noexcept;
    T& get() const noexcept;

    // invocation
    template<class... ArgTypes>
    invoke_result_t<class..., ArgTypes...> operator()(reference_wrapper<T>&&, ArgTypes...) const;
  }
```

reference_wrapper<T> is a CopyConstructible and CopyAssignable wrapper around a reference to an object or function of type T.

reference_wrapper<T> should be a trivially copyable type (6.9).

### 23.14.5.1 reference_wrapper construct/copy/destroy [refwrap.const]

reference_wrapper(T&&) noexcept;

> Effects: Constructs a reference_wrapper object that stores a reference to t.

reference_wrapper(const reference_wrapper& x) noexcept;

> Effects: Constructs a reference_wrapper object that stores a reference to x.get().

## 23.14.5.2 reference_wrapper assignment [refwrap.assign]

reference_wrapper& operator=(const reference_wrapper& x) noexcept;

1 Postconditions: *this stores a reference to x.get().

## 23.14.5.3 reference_wrapper access

```cpp
operator T&() const noexcept;
1 Returns: The stored reference.
T& get() const noexcept;
2 Returns: The stored reference.
```

## 23.14.5.4 reference_wrapper invocation

```cpp
template <class... T, typename Args>
inv_result_t<T&, Args...> invoke_...
operator()(ArgTypes&&... args) const;
1 Returns: INVOKE(get(args)...)(std::forward<ArgTypes>(args)).(23.14.3)
```

## 23.14.5.5 reference_wrapper helper functions

```cpp
template <class T> reference_wrapper<T> ref(T&& t) const noexcept;
1 Returns: reference_wrapper<T>.
template <class T> reference_wrapper<const T> ref(reference_wrapper<T> t) const noexcept;
2 Returns: ref(t.get()).
template <class T> reference_wrapper<const T> cref(const T&& t) const noexcept;
3 Returns: reference_wrapper<const T>().
template <class T> reference_wrapper<const T> cref(reference_wrapper<T> t) const noexcept;
4 Returns: cref(t.get()).
```

## 23.14.6 Arithmetic operations

The library provides basic classes for all of arithmetic operators in the language (8.6, 8.7).

### 23.14.6.1 Class T plus

```cpp
template<class T = void> struct plus {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
template<class T> struct plus<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) + std::forward<U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) + std::forward(U));
2 Returns: std::forward<T>(t) + std::forward(u).
```

### 23.14.6.2 Class T minus

```cpp
template<class T = void> struct minus {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
template<class T> struct minus<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) - std::forward(U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) - std::forward(U));
- Returns: std::forward<T>(t) - std::forward(u).
```

### 23.14.6.3 Class T multiplies

```cpp
template<class T = void> struct multiplies {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
template<class T> struct multiplies<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) * std::forward(U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) * std::forward(U));
- Returns: std::forward<T>(t) * std::forward(u).
```

### 23.14.6.4 Class T divides

```cpp
template<class T = void> struct divides {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
template<class T> struct divides<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) / std::forward(U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) / std::forward(U));
```

### 23.14.6.5 Class T modulus

```cpp
template<class T = void> struct modulus {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
Returns: x % y;
template<class T> struct modulus<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) % std::forward(U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) % std::forward(U));
- Returns: std::forward<T>(t) % std::forward(u).
```

### 23.14.6.6 Class T negate

```cpp
template<class T = void> struct negate {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
Returns: -x;
template<class T> struct negate<void> {
template<class T> constexpr auto operator()(T&& t) const
-> decltype(-std::forward<T>(t));
using is_transparent = unspecified;
};
template<class T> constexpr auto operator()(T&& t) const
-> decltype(-std::forward<T>(t));
Returns: -std::forward<T>(t).
```

## 23.14.7 Comparisons [comparisons]

1. The library provides basic function objects for all of the comparison operators in the (8.9, 8.10).
2. For templates less, greater, less_equal, and greater_equal, the specializations for any pointer type define a strict order that is consistent with other specializations and also consistent with the partial order imposed by the built-in operators <, >, ==, !=. [Note: When a < b is well-defined for pointers of type P, this implies (a < b) == less<P>(a, b), (a > b) == greater<P>(a, b), and so forth. For template specializations less<void>, greater<void>, less_equal<void>, and greater_equal<void>, if the operator calls a built-in operator comparing pointers, the call operator yields a strict total among those specializations and also consistent with the partial order imposed by those built-in operators.]

### 23.14.7.1 Class T equal_to

```cpp
template<class T = void> struct equal_to {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
```
1 Returns: x == y;
```cpp
template<class T> struct equal_to<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) == std::forward(U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) == std::forward(U));
2 Returns: std::forward<T>(t) == std::forward(u).
```

### 23.14.7.2 Class T not_equal_to

```cpp
template<class T = void> struct not_equal_to {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
```
1 Returns: x != y;
```cpp
template<class T> struct not_equal_to<void> {
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) != std::forward(U));
using is_transparent = unspecified;
};
template<class T, U> constexpr auto operator()(T&& t, U&& u) const
-> decltype(std::forward<T>(t) != std::forward(U));
2 Returns: std::forward<T>(t) != std::forward(u).
```

### 23.14.7.3 Class T greater

```cpp
template<class T = void> struct greater {
constexpr operator()(const T& x, const T&& y) const;
constexpr operator()(const T&& x, const T&& y) const;
```
1 Returns: x > y.
