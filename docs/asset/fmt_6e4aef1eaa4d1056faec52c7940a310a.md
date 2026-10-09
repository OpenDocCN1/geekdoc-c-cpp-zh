
`friend constexpr bool operator==(weak_ordering_v, weak_ordering_w) noexcept = default;`

`friend constexpr bool operator=(weak_ordering_v, unspecified) noexcept;`

`friend constexpr bool operator>(weak_ordering_v, unspecified) noexcept;`

`friend constexpr bool operator<=(weak_ordering_v, unspecified) noexcept;`

`friend constexpr bool operator<(weak_ordering_v, weak_ordering_w) noexcept;`

`friend constexpr bool operator>(unspecified, weak_ordering_v) noexcept;`

`friend constexpr bool operator<=(unspecified, weak_ordering_v) noexcept;`

`friend constexpr bool operator>=(unspecified, weak_ordering_v) noexcept;`

`friend constexpr weak_ordering operator<==(weak_ordering_v, unspecified) noexcept;`

`friend constexpr bool weak_ordering operator>=(unspecified, weak_ordering_v) noexcept;`

```
```

```cpp
// 有效值

inline constexpr weak_ordering_ordering::less(ord::less);

inline constexpr weak_ordering_ordering::equivalent(ord::equivalent);

inline constexpr weak_ordering_ordering::greater(ord::greater);
```

```cpp
constexpr operator partial_ordering() const 
返回：
value == 0 ? partial_ordering::equivalent
value < 0 ? partial_ordering::less
partial_ordering::greater
```

```cpp
constexpr bool operator==(unspecified, weak_ordering_v) noexcept;
constexpr bool operator<=(weak_ordering_v, unspecified) noexcept;
constexpr bool operator>(weak_ordering_v, unspecified) noexcept;
constexpr bool operator<=(weak_ordering_v, weak_ordering_v) noexcept;
constexpr bool operator>=(weak_ordering_v, weak_ordering_v) noexcept;
返回：v.value == 0 ? operator();
```

```cpp
constexpr bool operator<(unspecified, weak_ordering_v) noexcept;
constexpr bool operator>=(unspecified, weak_ordering_v) noexcept;
constexpr bool operator<=(unspecified, weak_ordering_v) noexcept;
constexpr bool operator>=(unspecified, weak_ordering_v) noexcept;
返回：0 == v.value for operator;
```

```cpp
constexpr weak_ordering operator<=(unspecified, weak_ordering_v) noexcept;
返回：v。
```

```cpp
constexpr weak_ordering operator>=(unspecified, weak_ordering_v) noexcept;
返回：v < 0 ? weak_ordering::greater : v > 0 ? weak_ordering::less : v.
```

# 17.11.2.4 类 strong_ordering [cmp.strongordered]

`strong_ordering` 通常用作三向比较运算符（7.6.8）的结果类型，它（a）满足所有的双向比较运算符（7.6.9, 7.6.10），并且（b）意味着可替换性。

```cpp
namespace std {
    class strong_ordering {
        int value; // 仅用于说明
        // 仅用于说明的构造函数
        constexpr explicit strong_ordering(ord v) noexcept : value(int(v)) {} // 仅用于说明
    public:
        // 有效值
        static const strong_ordering less;
        static const strong_ordering equal;
        static const strong_ordering greater;
        // 转换
        constexpr partial_ordering partial_ordering() const noexcept;
        constexpr weak_ordering weak_ordering() const noexcept;
        // 比较
        friend constexpr bool operator==(strong_ordering_v, unspecified) noexcept;
    }
}
```

```cpp
friend constexpr bool operator==(strong_ordering_v, strong_ordering_w) noexcept = default;
friend constexpr bool operator=(strong_ordering_v, unspecified) noexcept;
friend constexpr bool operator>(strong_ordering_v, unspecified) noexcept;
friend constexpr bool operator<=(strong_ordering_v, unspecified) noexcept;
friend constexpr bool operator<(strong_ordering_v, strong_ordering_w) noexcept;
friend constexpr bool operator>(unspecified, strong_ordering_v) noexcept;
friend constexpr bool operator<=(unspecified, strong_ordering_v) noexcept;
friend constexpr bool operator>=(unspecified, strong_ordering_v) noexcept;
friend constexpr strong_ordering operator<==(strong_ordering_v, unspecified) noexcept;
friend constexpr strong_ordering operator>=(unspecified, strong_ordering_v) noexcept;
}
```

```cpp
// 有效值
inline constexpr strong_ordering_ordering::less(ord::less);
inline constexpr strong_ordering_ordering::equal(ord::equal);
inline constexpr strong_ordering_ordering::equivalent(ord::equivalent);
inline constexpr strong_ordering_ordering::greater(ord::greater);
```

```cpp
constexpr operator partial_ordering() const noexcept
返回：
value == 0 ? partial_ordering::equivalent
value < 0 ? partial_ordering::less
partial_ordering::greater
```

```cpp
constexpr operator weak_ordering() const noexcept
返回：
value == 0 ? weak_ordering::equivalent
value < 0 ? weak_ordering::less
weak_ordering::greater
```

```cpp
constexpr bool operator==(unspecified, strong_ordering_v) noexcept;
constexpr bool operator<=(strong_ordering_v, unspecified) noexcept;
constexpr bool operator>(strong_ordering_v, unspecified) noexcept;
constexpr bool operator<=(strong_ordering_v, strong_ordering_v) noexcept;
constexpr bool operator>=(strong_ordering_v, strong_ordering_v) noexcept;
```

返回：v.value == 0 ? operator();

```cpp
constexpr bool operator<(unspecified, strong_ordering_v) noexcept;
constexpr bool operator>=(unspecified, strong_ordering_v) noexcept;
constexpr bool operator<=(unspecified, strong_ordering_v) noexcept;
constexpr bool operator>=(unspecified, strong_ordering_v) noexcept;
```

返回：0 == v.value for operator;

```cpp
constexpr strong_ordering operator<=(unspecified, strong_ordering_v) noexcept;
```

返回：v。

```cpp
constexpr strong_ordering operator>=(unspecified, strong_ordering_v) noexcept;
返回：v < 0 ? strong_ordering::greater : v > 0 ? strong_ordering::less : v.
```

# 17.11.3 类模板 common_comparison_category [cmp.common]

类型 `common_comparison_category` 为所有模板可以转换的最强比较类别提供别名。

> [注意 1：如果两个比较类型是不同的类型，且前者的实例可以转换为后者的实例，则该比较类型比另一个类型强。]

```cpp
template<class... Ts>
struct common_comparison_category {
    using type = Ts...;
};
```

备注：成员类型定义名 `type` 表示 `Ts...`（展开后的参数包）的共同比较类型 (11.11.3)，或者如果 `Ts` 中的任何元素不是比较类别。

> [注意 2：如果展开为空，则为 std::ordering。]

# 17.11.4 概念 three_way_comparison [cmp.concept]

```cpp
template<class T, class Cat>
concept compares_as =
    same_as<common_comparison_category<T, Cat>, Cat>;

template<class T, class U>
concept partially_ordered_with_t =
requires(const remove_reference_t<T>& t, const remove_reference_t<U>& u) {
    { t < u } -> boolean-test;
    { t > u } -> boolean-test;
    { t == u } -> boolean-test;
    { t != u } -> boolean-test;
    { u < t } -> boolean-test;
    { u > t } -> boolean-test;
    { u <= t } -> boolean-test;
    { u >= t } -> boolean-test;
};
```

设 `t` 和 `u` 分别为 `const` 类型 `remove_reference_t<T>` 和 `remove_reference_t<U>` 的值。`T` 和 `U` 满足 `partially_ordered_with<T, U>` 当且仅当：

- (1.1) `t < u == t > u == t >= u == t <= u == t > t, u >= t` 具有相同的符号，
- (1.2) `bool(t == u) == bool(u == t)` 为真，
- (1.3) `bool(t < u) == bool(u > t)` 为真，
- (1.4) `bool(t <= u) == bool(u >= t)` 为真，
- (1.5) `bool(t != u) == bool(t != u)` 为真。

```cpp
template<class T, class Cat>
concept three_way_comparable =
    partially_ordered_with<T, T> &
requires(const remove_reference_t<T>& a, const remove_reference_t<T>& b) {
    { a <=> b } -> compares_as<Cat>;
}
```

设 `a` 和 `b` 为 `const` 类型 `remove_reference_t<T>` 的值。`T` 和 `Cat` 满足 `three_way_comparable<T, Cat>` 当且仅当：

- (2.1) `(a <=> b) == bool(a == b)` 为真，
- (2.2) `(a != b) == bool(a != b)` 为真，
- (2.3) `((a <=> b) == 0)` 与 `(b <=> a)` 相等，
- (2.4) `(a <=> b < 0) == bool(a < b)` 为真，
- (2.5) `(a <=> b > 0) == bool(a > b)` 为真，
- (2.6) `(a <=> b <= 0) == bool(a <= b)` 为真，
- (2.7) `(a <=> b >= 0) == bool(a >= b)` 为真，且
- (2.8) 如果 `T` 可转换为 `strong_ordering`，则 `T` 满足 `totally_ordered` (18.5.4)。

# ISO/IEC 14882:2020(E)

```cpp
template<class T, class U, class Cat = partial_ordering>
concept three_way_comparable = 
    three_way_comparable<Cat>,
    three_way_comparable<const remove_reference_t<T>&, const remove_reference_t<U>&&>,
    common_comparable<const remove_reference_t<T>&, const remove_reference_t<U>&, Cat&&>,
    weakly_equality_with<T, U>,
    partially_ordered_with<T, U>&&
requires(const remove_reference_t<T>& t, const remove_reference_t<U>& u) {
    { t < u } -> compares_as<Cat>;
    { u > t } -> compares_as<Cat>;
};
```
