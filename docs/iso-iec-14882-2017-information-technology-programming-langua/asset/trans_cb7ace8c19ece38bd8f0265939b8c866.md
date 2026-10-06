

# ISO/IEC 14882:2017(E)

```cpp
template <class T, size_t N>
void swap(T&& a, T&& b) noexcept(is_not_swappable_v<T>);
```

- 4 注释：除非 `is_swappable_v<T>` 为真，否则此函数不参与重载解析。
- 5 要求：对于范围 [0, N) 中的所有 `i`，`a[i]` 应当与 (20.5.3.2) `b[i]` 可交换。
- 6 效果：等同于执行了 `swap_ranges(a, a + N, b)`。

## 23.2.4 exchange

```cpp
template <class T, class U = T> exchange(T& obj, U&& new_val);
```

- 1 效果：等同于
T old_val = std::move(obj);
obj = std::forward(new_val);
return old_val;

## 23.2.5 Forward/move_helpers

- 1 库提供了模板化的辅助函数，以简化向值的移动语义，并简化转发函数的实现。本子句中指定的所有函数都是安全的(21.10.4)。

```cpp
template <class T> constexpr T&& forward(reference_t<T>&& t) noexcept;
template <class T> constexpr T&& forward(reference_t<T>&& t) noexcept;
```

- 2 返回：`static_cast<T&>(t)`。
- 3 注释：如果第二个参数被实例化为左值引用，则程序将是错误的定义形式的（ill-formed）。

```cpp
示例:
template <class T, class A1, class A2>
shared_ptr<T> factory(A1&& a1, A2&& a2) {
    return shared_ptr<T>(new(std::forward<A1>(a1), std::forward<A2>(a2)));
}

struct A {
    int;
    const double;
};

void g() {
    shared_ptr<A> sp1 = factory<A>(2, 1.414); // 错误：2不会绑定到 int&
    int i = 2;
    shared_ptr<A> sp2 = factory<A>(i, 1.414); // OK
```

在第一次调用中，A1 被推导为 int，因此 2 作为右值被转发到 A 的构造函数。
在第二次调用中，A2 被推导为 int，因此 1 作为左值转发到 A 的构造函数。
在两种情况下，A2 都被推导为 double，因此 1.414 作为右值转发到 A 的构造函数。— 示例结束[]

```cpp
template <class T> constexpr T&& remove_reference_t<T>&& move(T&& t) noexcept;
```

- 5 返回：`static_cast<remove_reference_t<T>&>(t)`。
- 6 示例：

```cpp
template <class T, class A1>
shared_ptr<T> factory(A1&& a1) {
    return shared_ptr<T>(new(std::forward<A1>(a1)));
}
```

```cpp
struct A {
    A();
    A(const A&);      // 从值拷贝
    A(A&&);           // 从右值移动
};

void g() {
    A a;
    shared_ptr<A> spl = factory(a);      // "a" 绑定到 A(const A&)
    shared_ptr<A> spl = factory(std::move(a)); // "a" 绑定到 A(A&&)
};
```

在第一次调用中，A1 被推导为 A&&，因此它作为非 const 引用被转发。这绑定到了构造函数 A(const A&)，从 a 拷贝值。在第二次调用 factory 时，由于调用了 `std::move(a)`，A1 被推导为 A&&，因此移动到构造函数 A(A&&)，从而移动该值。示例结束

```cpp
template <class T> constexpr conditional<
    !is_nothrow_move_constructible_v<T> && is_copy_constructible_v<T>, const T&, T&&>
move_if_noexcept(T&& x) noexcept {
    return std::move(x);
}
```

## 23.2.6 函数 as_const

```cpp
template <class T> constexpr add_const<T>& as_const(T& t) noexcept {
    return t;
}
```

## 23.2.7 函数模板 decltype

库提供了函数 `decltype`，用于简化作为未求值表达式（第 8 节）中运行的表达式的定义。

```cpp
template <class T> T_reference<T>& declval() noexcept; // 未求值
```

- 2 注释：如果这被实例化为左值引用，程序将是错误的定义形式的。
- 3 注释：`decltype` 的模板参数 T 可以是不完全类型。

示例：
template <class T, class From> decltype(static_cast<T>(declval<From>()))(From&&)
声明了一个函数 T，只有当类型 From 转换为 T 时，该函数才参与重载。 示例结束

## 23.2.8 原始类型输出转换

- 1 所有函数通过填充范围 `[first, last]` 将值转换为字符串，其中 `first, last` 要求必须是一个值。
- 2 接收浮点值的函数没有精度参数，确保字符串表示由最少数量的字符组成，使得存在唯一的表示。
- 3 接收格式参数的函数没有精度参数，确保字符串表示由最少数量的字符组成。`to_chars` 等效于 `from_chars`。`to_chars` 的格式如下：如果 `fmt` 为 `chars_format::fixed`，如果 `fmt` 为 `chars_format::scientific`，如果 `fmt` 为 `chars_format::general`。
- 4 要求：`base` 在 2 到 36 之间。
- 5 效果：`base` 进制位数字表示。如果值为负，表示将以负号开头。
- 6 线程：无。
- 7 注释：`to_chars` 为所有符号整数类型提供了重载。` `first` `。
- 8 效果：值转换为 `printf` 风格的字符串。
- 9 线程：`to_chars` 作用于 `from_chars` 类型。
- 10 要求：`fmt` 是 `chars_format` 的枚举值之一。
- 11 效果：值转换为 `C` 语言风格的字符串。
- 12 线程：无。

```cpp
to_chars_result to_chars(char* first, char* last, float value, chars_format fmt, int precision);
to_chars_result to_chars(char* first, char* last, double value, chars_format fmt, int precision);
to_chars_result to_chars(char* first, char* last, long double value, chars_format fmt, int precision);
```

- 13 要求：`fmt` 是 `chars_format` 的枚举值之一。
- 14 效果：值转换为 `C` 语言风格的字符串，带有指定的精度。
- 15 线程：无。

参见：ISO C 7.21.1

## 23.2.9 原始类型输入转换 [utility.from.chars]

所有 `from_chars` 函数分析字符串 `[first, last)` 以匹配模式，其中 `[first, last)` 是一个有效范围。如果字符匹配模式，值保持不变，返回值的 `ptr` 为 `first`，`ec` 为 `errc::invalid_argument`。否则，匹配模式的字符被解释为值的表示。返回值的 `ptr` 指向第一个不匹配模式的字符，如果所有字符匹配则指向 `last`。如果解析出的值不在范围内，`ec` 为 `errc::too_large`，且范围 `[first, last]` 内容未定义。

## 23.3 编译时整数序列

```
[intseq]
```

## 23.3.1 通用

库提供了一个表示整数序列的类模板。当作为函数模板时，参数包可以被推导并用于包展开。
[注意：`index_sequence` 别名用于 `size_t` 整数序列的常见情况；参见 23.3.5.5。注意结束]

## 23.3.2 类模板 integer_sequence

```cpp
[std::integer_sequence]
```

```cpp
namespace std {
template<class T, T... I>
struct integer_sequence {
  using value_type = T;
  static constexpr size_t size() noexcept { return sizeof(I); };
};
}
```

