

由给定标准库函数模板返回的参数转发调用包装器的类型与其对应状态实体的类型相同。

## 20.14.5 函数模板 invoke
[func.invoke]

```
template<class F, class... Args>
  constexpr invoke_result_t<F, Args...> invoke(F&& f, Args&&... args)
    noexcept(is_nothrow_invocable_v<F, Args...>);
```

返回：INVOKE(std::forward<F>(f), std::forward<Args>(args)... ) (20.14.4)。

## 20.14.6 类模板 reference_wrapper
[refwrap]

### 20.14.6.1 通用
[refwrap.general]

```
namespace std {
  template<class T> class reference_wrapper {
  public:
    // types
    using type = T;

    // construct/copy/destroy
    template<class U>
      constexpr reference_wrapper(U&&) noexcept(see below);
    constexpr reference_wrapper(const reference_wrapper& x) noexcept;

    // assignment
    constexpr reference_wrapper& operator=(const reference_wrapper& x) noexcept;

    // access
    constexpr operator T& () const noexcept;
    constexpr T& get() const noexcept;

    // invocation
    template<class... ArgTypes>
      constexpr invoke_result_t<T&, ArgTypes...> operator()(ArgTypes&&... ) const;
  };

  template<class T>
    reference_wrapper(T&) -> reference_wrapper<T>;
}
```

- `reference_wrapper<T>` 是对类型为 T 的对象或函数的引用的一种 *Cpp17CopyConstructible* 和 *Cpp17CopyAssignable* 包装器。
- `reference_wrapper<T>` 是一个可 trivial 复制的类型 (6.8)。
- `reference_wrapper` 的模板参数 T 可以是不完全类型。

### 20.14.6.2 构造函数和析构函数
[refwrap.const]

```
template<class U>
  constexpr reference_wrapper(U&& u) noexcept(see below);
```

- 令 *FUN* 表示仅用于阐述的函数
- 
      ```cpp
      void FUN(T&) noexcept;
      void FUN(T&&) = delete;
      ```
- 
- *约束：* 表达式 `FUN(declval<U>())` 是良构的且 `is_same_v<remove_cvref_t<U>, reference_wrapper>` 为 false。
- *效果：* 构造变量 `r`，如同通过 `T& r = std::forward<U>(u)`，然后构造一个存储对 `r` 的引用的 `reference_wrapper` 对象。
- *说明：* `noexcept` 内部的表达式等价于 `noexcept(FUN(declval<U>())).`

```
constexpr reference_wrapper(const reference_wrapper& x) noexcept;
```

效果：构造一个存储对 `x.get()` 的引用的 `reference_wrapper` 对象。

### 20.14.6.3 赋值

```
constexpr reference_wrapper& operator=(const reference_wrapper& x) noexcept;
```

*后置条件：* `*this` 存储对 `x.get()` 的引用。

### 20.14.6.4 访问

```
constexpr operator T& () const noexcept;
```

*返回：* 存储的引用。

```
constexpr T& get() const noexcept;
```

*返回：* 存储的引用。

### 20.14.6.5 调用

```
template<class... ArgTypes>
  constexpr invoke_result_t<T&, ArgTypes...>
    operator()(ArgTypes&&... args) const;
```

*强制要求：* T 是一个完整类型。

*返回：* `INVOKE(get(), std::forward<ArgTypes>(args)...)`。 (20.14.4)

### 20.14.6.6 辅助函数

以下 `ref` 和 `cref` 函数模板的模板参数 T 可以是不完全类型。

```
template<class T> constexpr reference_wrapper<T> ref(T& t) noexcept;
```

*返回：* `reference_wrapper<T>(t)`。

```
template<class T> constexpr reference_wrapper<T> ref(reference_wrapper<T> t) noexcept;
```

*返回：* `ref(t.get())`。

```
template<class T> constexpr reference_wrapper<const T> cref(const T& t) noexcept;
```

*返回：* `reference_wrapper<const T>(t)`。

```
template<class T> constexpr reference_wrapper<const T> cref(reference_wrapper<T> t) noexcept;
```

*返回：* `cref(t.get())`。

## 20.14.7 算术运算

### 20.14.7.1 通用

库为语言中的所有算术运算符提供了基本函数对象类 (7.6.5, 7.6.6)。

### 20.14.7.2 类模板 plus

```
template<class T = void> struct plus {
  constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

*返回：* `x + y`。

```
template<> struct plus<void> {
  template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) + std::forward<U>(u));

  using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
  -> decltype(std::forward<T>(t) + std::forward<U>(u));
```

*返回：* `std::forward<T>(t) + std::forward<U>(u)`。

### 20.14.7.3 类模板 minus [arithmetic.operations.minus]

```
template<class T = void> struct minus {
    constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

返回：x - y。

```
template<> struct minus<void> {
    template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) - std::forward<U>(u));
    using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) - std::forward<U>(u));
```

返回：std::forward<T>(t) - std::forward<U>(u)。

### 20.14.7.4 类模板 multiplies [arithmetic.operations.multiplies]

```
template<class T = void> struct multiplies {
    constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

返回：x * y。

```
template<> struct multiplies<void> {
    template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) * std::forward<U>(u));
    using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) * std::forward<U>(u));
```

返回：std::forward<T>(t) * std::forward<U>(u)。

### 20.14.7.5 类模板 divides [arithmetic.operations.divides]

```
template<class T = void> struct divides {
    constexpr T operator()(const T& x, const T& y) const;
};
```

```
constexpr T operator()(const T& x, const T& y) const;
```

返回：x / y。

```
template<> struct divides<void> {
    template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
        -> decltype(std::forward<T>(t) / std::forward<U>(u));
    using is_transparent = unspecified;
};
```

```
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) / std::forward<U>(u));
```

返回：std::forward<T>(t) / std::forward<U>(u)。

### 20.14.7.6 类模板 modulus [arithmetic.operations.modulus]

```
template<class T = void> struct modulus {
    constexpr T operator()(const T& x, const T& y) const;
```

```
```cpp
};

constexpr T operator()(const T& x, const T& y) const;
```
```

_Returns:_ `x % y`.

```
```cpp
template<> struct modulus<void> {
  template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) % std::forward<U>(u));

  using is_transparent = unspecified;
};
```
```

```
```cpp
template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
  -> decltype(std::forward<T>(t) % std::forward<U>(u));
```
```

_Returns:_ `std::forward<T>(t) % std::forward<U>(u)`.

### 20.14.7.7 类模板 negate

```
```cpp
template<class T = void> struct negate {
  constexpr T operator()(const T& x) const;
};
```
```

```
```cpp
constexpr T operator()(const T& x) const;
```
```

_Returns:_ `-x`.

```
```cpp
template<> struct negate<void> {
  template<class T> constexpr auto operator()(T&& t) const
    -> decltype(-std::forward<T>(t));

  using is_transparent = unspecified;
};
```
```

```
```cpp
template<class T> constexpr auto operator()(T&& t) const
  -> decltype(-std::forward<T>(t));
```
```

_Returns:_ `-std::forward<T>(t)`.

## 20.14.8 比较

### 20.14.8.1 通用

库为语言中的所有比较运算符提供了基本函数对象类 ([7.6.9](7.6.9), [7.6.10](7.6.10))。

对于模板 less、greater、less_equal 和 greater_equal，任何指针类型的特化产生的结果与指针上的实现定义严格全序一致 ([3.24](3.24))。

> [_注 1：_ 如果对于类型为 P 的指针 a 和 b，`a < b` 是良定义的，则 `(a < b) == less<P>()(a, b)`，`(a > b) == greater<P>()(a, b)`，等等。 — _注结束_]

对于模板特化 `less<void>`、`greater<void>`、`less_equal<void>` 和 `greater_equal<void>`，如果调用运算符调用比较指针的内置运算符，则调用运算符产生的结果与指针上的实现定义严格全序一致。

### 20.14.8.2 类模板 equal_to

```
```cpp
template<class T = void> struct equal_to {
  constexpr bool operator()(const T& x, const T& y) const;
};
```
```

```
```cpp
constexpr bool operator()(const T& x, const T& y) const;
```
```

_Returns:_ `x == y`.

```
```cpp
template<> struct equal_to<void> {
  template<class T, class U> constexpr auto operator()(T&& t, U&& u) const
    -> decltype(std::forward<T>(t) == std::forward<U>(u));
```

