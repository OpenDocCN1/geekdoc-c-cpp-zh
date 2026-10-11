
9：返回：`u <= t`。

> 注意：上述比较函数的定义不需要构造 `t_tail`（或 `u_tail`）。这可能无法，因为 `t` 和 `u` 不要求可拷贝。此外，所有比较函数都是短路的；它们不会执行确定结果所需的额外元素。——注释结束

## 23.5.3.9 元组特性 [tuple.traits]

```cpp
template <class... Ttypes, class... Alloc>
struct uses_allocator<tuple<Ttypes...>, Alloc> : true_type { };
```

- 1 要求：`Alloc` 应为分配器 (20.5.3.5)。

> 注意：此特性的特化告知其他库 `tuple` 可以分配器构造，尽管它没有嵌套的 `allocator_type`。——注释结束

## 23.5.3.10 元组特化算法 [tuple.special]

```cpp
template <class... Ttypes>
void swap(tuple<Ttypes...>& x, tuple<Ttypes...>& y) noexcept(see below);
```

备注：除非 `is_swappable_v<T, T>` 对于所有 `i` (`0 <= i < sizeof...(Ttypes)`) 为真，否则该函数不参与重载解析。`noexcept` 内部的表达式等价于：
`except(swap(y))`

影响：仿佛通过 `x.swap(y)`。

# ISO/IEC 14882:2017(E)

## 23.6 可选对象 [optional]

### 23.6.1 一般规定 [optional.general]

此子类描述了表示可选对象的类模板。可选对象是一个包含另一个对象存储空间的对象，该对象负责管理该被包含对象（如果有）的生命周期。被包含的对象可以在可选对象初始化后初始化，并可能在可选对象销毁之前销毁。被包含对象的初始化状态由可选对象跟踪。

### 23.6.2 头文件 <optional> 概要 [optional.syn]

```cpp
namespace std {
// 23.6.3. class optional
template <class T>
class optional;
// 23.6.4. 无值状态指示器
struct nullopt_t (见下);
inline const nullopt_t nullopt(specified);
// 23.6.5. class bad_optional_access
class bad_optional_access;
// 23.6.6. 关系运算符
template <class T, class U>
constexpr bool operator==(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator!=(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator>(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator<=(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator>=(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator>(const optional<T>&, const optional<U>);
}
```

```cpp
// 23.6.7. 与 nullopt 比较
template <class T>
constexpr bool operator==(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator!=(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator<>(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator<=(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator>(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator>=(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator==(const optional<T>&, nullopt_t) noexcept;
template <class T>
constexpr bool operator!=(const optional<T>&, nullopt_t) noexcept;
```

```cpp
// 23.6.8. 与 T 比较
template <class T, class U>
constexpr bool operator==(const optional<T>&, const optional<U>);
template <class T, class U>
constexpr bool operator!=(const optional<U>, const optional<U>);
template <class T, class U>
constexpr bool operator<=(const optional<T>, const optional<U>);
template <class T, class U>
constexpr bool operator>=(const optional<U>, const optional<U>);
```

```cpp
template <class T, class U> constexpr bool operator=(const optional<T>&, const U);
template <class T, class U> constexpr bool operator=(const U, const optional<T>);
template <class T, class U> constexpr bool operator<(const optional<U>, const optional<T>);
template <class T, class U> constexpr bool operator>(const optional<T>, const U&);
template <class T, class U> constexpr bool operator>(const U, const optional<T>&);
template <class T, class U> constexpr bool operator>(const optional<T>&, const U&);
```

```cpp
// 23.6.9. 特化算法
```

```cpp
template <class T>
void swap(optional<T>&, optional<T>&) noexcept(见下);
template <class T>
constexpr optional<T> <见下> make_optional(T&&);
template <class T, class Args...>
constexpr optional<T> make_optional(Args&&... args);
template <class T, class U, class Args...>
template <class T, class U, class Args...>
make_optional(initializer_list<U>&&, Args&&... args);
```

```cpp
// 23.6.10. 哈希支持
```

```cpp
template <class T>
template <class T> struct hash<optional<T>>
}
```

- 1 程序需要为引用类型、或可能为 cv 修饰的类型 `in_place_t` 或 `null_t` 实例化 `optional` 是格式错误的。

### 23.6.3 类模板 optional [optional|optional]

```cpp
template <class T>
class optional {
public:
    using value_type = T;
    // 23.6.3.1, 构造函数
    constexpr optional() noexcept;
    constexpr optional(null_t) noexcept;
    constexpr optional(const optional<T>&);
    constexpr optional(optional<T>&&) noexcept(见下);
    template <class... class Args...>
    constexpr explicit optional(in_place_t, Args&&...);
    template <class U, class Args...>
    constexpr explicit optional(in_place_t, initializer_list<U>&&, Args&&...);
    constexpr optional(const U&);
    template <class U>
    optional optional(const U&);
    template<class U>
    optional(U&&&&);
    // 23.6.3.2, 析构函数
    ~optional();
    // 23.6.3.3, 赋值
    optional& operator=(null_t) noexcept;
    optional& operator=(const optional<T>&);
    optional& operator=(optional&&) noexcept(见下);
    template<class U = T>
    const optional& operator=(const U&&&);
    template<class U = T>
    const optional& operator=(U&&&&);
    template<class... Args>
    T& operator(Args&&...);
    template<class... Args>
    T& operator(initializer_list<Args>, Args&&...);
    // 23.6.3.4. 
    void swap(optional&&) noexcept(见下);
    // 23.6.3.5. 观察者
    const T* operator() const;
    const T* operator() const;
    const T& operator() const;
    const T& operator() const;
    explicit bool operator(bool) const noexcept;
    bool has_value() const;
    const T value() const;
    const T value() const;
    const T& value() const&;
    template<class U>
    const T& value_or(U&&) const&;
    template<class U>
    const T& value_or(U&&) const&&;
    // 23.6.3.6. 修改器
    void reset() noexcept;
private:
    T* val; // 仅用于说明
}
template<class T> optional operator() -> T;
```

在任何时刻，`optional<T>` 的任何实例都包含一个值或不包含一个值。当 `optional<T>` 的实例包含一个值时，意味着类型为 `T` 的对象（称为可选对象的被包含值）存储在动态内存中，以分配其被包含的值。实现不允许使用额外的存储空间，例如动态内存。被包含的值应分配在`optional<T>` 存储区域中适用于 `T` 的适当对齐区域。当类型为 `optional<T>` 的对象转换为 `bool` 时，如果对象包含一个值，则转换返回 `true`；否则转换返回 `false`。成员 `val` 仅用于说明。当 `optional<T>` 对象包含一个值时，`val` 指向被包含的值。

### 23.6.3.1 构造函数

`constexpr optional() noexcept;`

`constexpr optional(null_t) noexcept;`

- 后置条件：`*this` 不包含一个值。
- 备注：类型 `T` 的每个构造函数均为 `constexpr`。

`constexpr optional(const optional& rhs);`

- 影响：如果 `rhs` 包含一个值，则以表达式 `rhs` 初始化被包含的 `T` 类型对象。
- 后置条件：`bool(this) == bool(rhs);`
- 抛出：所选构造函数抛出的异常。
- 备注：如果 `is_copy_constructible<T>` 为 `false`，则该构造函数被删除；`is_trivially_copy_constructible<T>` 为 `true`，则应为 `constexpr`。

`constexpr optional(optional&& rhs) noexcept(见下);`

- 影响：如果 `rhs` 包含一个值，则以表达式 `move(rhs)` 初始化被包含的值；`rhs` hơn。
- 后置条件：`bool(this) == bool(*rhs);`
- 抛出：所选构造函数抛出的异常。
- 备注：除非 `is_move_constructible<T>` 为 `true`，否则该构造函数不参与重载决。`is_trivially_move_constructible<T>` 为 `true`，则应为 `constexpr`。

`template <class... Args> constexpr explicit optional(in_place_t, Args&&... args);`

- 影响：以参数 `std::forward<Args>(args)` 直接初始化 `T` 类型对象作为被包含的值。
- 后置条件：`*this` 包含一个值。
- 抛出：所选构造函数抛出的异常。
- 备注：如果用于初始化的构造函数为 `constexpr`，则该构造函数应为 `constexpr`。除非 `is_constructible<T, initializer_list<U>, Args&&...>` 为 `true`，否则该构造函数不参与重载决。

`template <class U, class Args...> constexpr explicit optional(in_place_t, initializer_list<U> il, Args&&... args);`

- 影响：以表达式 `std::forward<U>(il)` 直接初始化 `T` 类型对象作为被包含的值。
- 后置条件：`*this` 包含一个值。
- 抛出：所选构造函数抛出的异常。
- 备注：除非 `is_constructible<T, Args&&...>` 为 `true`，否则该构造函数不参与重载决。如果 `T` 的用于初始化的构造函数为 `constexpr`，则该构造函数应为 `constexpr`。

`template <class U> constexpr optional(U&& u);`

- 影响：以表达式 `std::forward<U>(u)` 直接初始化 `T` 类型对象作为被包含的值。
- 后置条件：`*this` 包含一个值。
- 抛出：所选构造函数抛出的异常。
- 备注：如果 `T` 的所选构造函数为 `constexpr`，则该构造函数应为 `constexpr`。

# ISO/IEC 14882:2017(E)

构造函数。除非 `is_constructible_v<T, U&>` 为真、`is_name_v<decay_t<U>, in_place_t>` 为假，且 `is_same_v<decay_t<U>>` 为假，否则该构造函数不参与重载解析。该构造函数是显式的（explicit），当且仅当 `is_convertible_v<U&, T>` 为假。

```cpp
template <class U> explicit(const optional<U> rhs);
```

影响：如果 `rhs` 包含一个值，则在用表达式 `*rhs` 直接初始化类型为 `T` 的对象时，将包含的值赋值。

后置条件：`bool(rhs) == *(this)`。

抛出异常：`T` 的选定构造函数抛出的任何异常。

备注：此构造函数不参与重载解析（注意：此处 OCR 文本似乎截断或重复了）
