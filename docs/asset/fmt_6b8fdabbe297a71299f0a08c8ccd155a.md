
+ 2 注意：判别类型可能包含不同类型的值，但不会尝试它们之间进行转换，例如，`5` 被存储为 `int`，且不会隐式转换为 `"5"` 或 `5.0`。这种对解释的漠视但对类型的感知实际上允许单值的通用容器，且没有歧义转换的空间。

## 23.8.1 Header `<any>` 概要 [any.synop]

```cpp
namespace {
// 23.8.2, bad_any_cast
class bad_any_cast;

// 23.8.3, class any
class any;

// 23.8.4, 非成员函数
void swap(any&& x, any&& y) noexcept;

template <class T, class... Args>
make_any(Args&&, ...args);

template <class T, class U, class... Args>
make_any(initializer_list<U> il, Args&&, ...args);

template<class T>
Tany_cast(const any& operand);
template<class T>
Tany_cast(any& operand);
template<class T>
Tany_cast(any&& operand);
```

# ISO/IEC 14882:2017(E)

```cpp
template<class T>
const T* any_cast(const any* operand) noexcept;
template<class T>
T* any_cast(const any* operand) noexcept;
}
```

## 23.8.2 类 `bad_any_cast`

[any.bad_any_cast]

```cpp
class bad_any_cast : public bad_cast {
public:
    char* what() const noexcept override;
    const char* what() const noexcept override;
```

- `bad_any_cast` 类型的对象由失败的 `any_cast` (`23.8.4`) 抛出。
- 返回值：实现定义的 NTBS（未指定的类型）。
- 备注：消息可能是一个以空结尾的多字节字符串 (`20.4.2.1.5.2`)，适用于转换并显示为字符串 (`24.3, 25.4.1.4`)。

## 23.8.3 类 `any`

[any.class]

```cpp
class any {
public:
    // 23.8.3.1, 构造与析构
    constexpr any() noexcept;
    any(const any& other);
    any(any&& other) noexcept;

    template<class T>
    any(T&& value);

    template<class T, class... Args>
    explicit any(in_place_tag<T>, Args&&...);
    template<class T, class... Args>
    explicit any(in_place_tag<T>, std::initializer_list<U>, Args&&...);

    // 23.8.3.2, 赋值
    operator=(const any& rhs);
    operator=(any&& rhs) noexcept;

    template<class T>
    any& operator=(T&& rhs);

    // 23.8.3.3, 修饰符
    template<class T, class... Args>
    decay<T>&& emplace(Args&&...);
    template<class T, class... Args>
    decay<T>&& emplace(std::initializer_list<U>, Args&&...);
    void reset() noexcept;
    void swap(any&& rhs) noexcept;

    // 23.8.3.4, 观察
    bool has_value() const noexcept;
    const type_info& type() const noexcept;
};
```

ISO/IEC 14882:2017(E)

`any` 类的对象存储满足构造要求的任意类型实例，或者没有值，这被称为该类的状态。存储的实例是所包含的值。如果两个状态都没有值，或者都具有值，则这两个状态是等价。`any_cast` 函数提供了对包含值的类型安全访问。示例：所构造的对象持有一个 `int`。这种小对象优化仅应应用于适用于 `move_constructible_v<T>` 为真的的类型。

### 23.8.3.1 构造与析构 [any::cons]

`constexpr any() noexcept;`

后置条件：`has_value()` 为 `false`。

`any(const any& other);`

影响：如果 `has_value()` 为 `false`，则构造一个没有值的对象。否则，等同于 `any(in_place_tag<T>, Args&&...)`，其中 `T` 是包含值的类型。

`any(any&& other) noexcept;`

影响：如果 `has_value()` 为 `false`，则构造一个没有值的对象。否则，构造一个包含 `other` 中包含值的 `any` 对象，或者一个从 `value` 作为值构造的相同类型的对象。

后置条件：`other` 处于有效但未指定的状态。

`template<class T> any(T&& value);`

设：`VT` 应当为 `decay<T>`。

要求：`VT` 应满足 `CopyConstructible` 要求。

影响：构造一个 `any` 对象，其包含一个通过 `std::forward<T>(value)` 直接初始化的类型 `VT` 的对象，且 `move_constructible_v<VT>` 为 `true`。

`template<class T, class... Args> explicit any(in_place_tag<T>, Args&&...);`

设：`VT` 为 `decay<T>`。

要求：`VT` 应满足 `CopyConstructible` 要求。

影响：将包含的值初始化为使用参数 `std::forward<Args>(args)` 直接初始化类型为 `VT` 的对象。

后置条件：`*this` 包含一个类型为 `VT` 的值。

抛出：由 `VT` 的选定构造函数抛出的异常。

备注：除非 `copy_constructible_v<VT>` 为 `true` 且 `is_constructible_v<VT, Args...>` 为 `true`，否则此构造函数不参与重载决议。

`template <class T, class U, class Args> explicit any(in_place_tag<T>, std::initializer_list<U> il, Args&&... args);`

设：`VT` 为 `decay<T>`。

要求：`VT` 应满足 `CopyConstruct` 要求。

影响：如果使用参数 `il` 直接列表初始化一个 `VT` 对象，则初始化包含的值。

后置条件：`*this` 包含一个值。

抛出：由 `VT` 的选定构造函数抛出的异常。

备注：除非 `copy_constructible_v<VT>` 为 `true` 且 `is_constructible_v<VT, initializer_list<U>, Args...>` 为 `true`，否则此构造函数不参与重载决议。

`any() noexcept;`

影响：等同于 `reset()`。

### 23.8.3.2 赋值 [any.assign]

`any& operator=(const any&& rhs);`

影响：等同于 `any(rhs).swap(*this)`。如果抛出异常则无影响。

返回值：`*this`。

抛出：源于包含值的拷贝构造函数的异常。

`any& operator=(any&& rhs) noexcept;`

影响：等同于 `any(std::move(rhs)).swap(*this)`。

返回值：`*this`。

后置条件：`*this` 的状态等于 `rhs` 的状态，且 `rhs` 留处于有效但未指定的状态。

`template<class T> any& operator=(T&& rhs);`

设：`VT` 为 `decay<T>`。

要求：`VT` 应满足 `CopyConstruct` 要求。

影响：构造一个 `any` 对象，其包含一个通过 `std::forward<T>(rhs)` 直接初始化的类型 `VT` 的对象，并 `tmp.swap(*this)`。如果抛出异常则无影响。

返回值：`*this`。

备注：除非 `VT` 与 `any` 的类型不同且 `copy_constructible_v<VT>` 为 `true`，否则此运算符不参与重载决议。

抛出：由 `VT` 的选定构造函数抛出的异常。

### 23.8.3.3 修饰符 [any.modifiers]

`template<class T, class... Args> decay<T>&& emplace(Args&&...);`

设：`VT` 为 `decay<T>`。

要求：`VT` 应满足 `CopyConstruct` 要求。

影响：如果使用参数 `std::forward<Args>(args)` 直接列表初始化一个 `VT` 对象，则初始化包含的值。

后置条件：`*this` 包含一个值。

抛出：由 `VT` 的选定构造函数抛出的异常。

备注：此构造函数不参与重载决议，除非 `copy_constructible_v<VT>` 为 `true` 且 `is_constructible_v<VT, initializer_list<U>, Args...>` 为 `true`。 (注：此处原文逻辑似乎存在重复粘贴错误，已按原文逻辑翻译)

# ISO/IEC 14882:2017(E)

```cpp
template <class T, class U, ... Args>
    any make_any(initializer_list<U> il, Args&& ...args);

Effects: Equivalent to: return any(in_place_type<T>(args), std::forward<Args>(args)...);

template <class T>
    T any_cast(const any& operand);

template <class T>
    T any_cast(const any&& operand);

template <class T>
    T any_cast(any* operand);
```

Requires: For the first overload, is_constructible<T, const U&> is true. For the second overload, is_constructible<T, U> is true. For the third overload, is_constructible<T, U> is true. Otherwise the program is ill-formed.

Returns: For the first and second overload, static_cast<T>(*any_cast<U>(operand)). For the third overload, static_cast<T>(std::move(*any_cast<U>(operand))).

Throws: bad any_cast if typeid(operand) != remove_reference_t<T>.

```cpp
[Example:
    any x(5);
    assert(any_cast<int>(x) == 5); // holds int
    any_cast<int>(x) = 10; // cast to value
    assert(any_cast<int>(x) == 10); // cast to reference

    x = "Meow"; // holds char*
    assert(strcmp(any_cast<const char*>(x)
```

```cpp
template <class T>
T any_cast(const any* operand) noexcept;
```

Returns: If operand != nullptr && operand->type() == typeid(T), a pointer to the object contained by operand; otherwise, nullptr.

```cpp
[Example:
bool is_string(const any& operand) {
    return any_cast<string>(&operand) != nullptr;
}
// end example;
```

# 23.9 Bitsets [bitset]

## 23.9.1 Header `<bitset>` synopsis

```cpp
#include <string> // for stream (30.7.1), ostream (30.7.2), see 30.3.1
#include <iosf>

namespace std {
template<size_t N> class bitset {
    // 23.9.1. operators
    template<size_t N>
    bitset& operator(const bitset<N>& lhs, const bitset<N>& rhs) noexcept;
    template<size_t N>
    bitset& operator=(const bitset<N>& lhs, const bitset<N>& rhs) noexcept;
    template<size_t N>
    bitset& operator(const bitset<N>& lhs, const bitset<N>& rhs) noexcept;
    template <char T, class traits>
    basic_ostream<charT, traits>&
        operator<<=(basic_charT<T, traits>& os, const basic_charT<T, traits>& x);
    template <char T, class traits, size_t N>
    basic_ostream<charT, traits>&
        operator<<=(basic_charT<T, traits>& os, const basic_charT<T, traits>& x);
};
```

头文件 `bitset` 定义了一个类模板和若干相关函数，用于表示和操作固定大小的位序列。

## 23.9.2 Class template bitset [template.bitset]
