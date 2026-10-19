

```cpp
template<class T>
    constexpr conditional_t<
        !is_nothrow_move_constructible_v<T> && is_copy_constructible_v<T>, const T&, T&&>
        move_if_noexcept(T& x) noexcept;

// 20.2.5, as_const
template<class T>
    constexpr add_const_t<T&> as_const(T& t) noexcept;
template<class T>
    void as_const(const T&&) = delete;

// 20.2.6, declval
template<class T>
    add_rvalue_reference_t<T> declval() noexcept;    // as unevaluated operand

// 20.2.7, integer comparison functions
template<class T, class U>
    constexpr bool cmp_equal(T t, U u) noexcept;
template<class T, class U>
    constexpr bool cmp_not_equal(T t, U u) noexcept;

template<class T, class U>
    constexpr bool cmp_less(T t, U u) noexcept;
template<class T, class U>
    constexpr bool cmp_greater(T t, U u) noexcept;
template<class T, class U>
    constexpr bool cmp_less_equal(T t, U u) noexcept;
template<class T, class U>
    constexpr bool cmp_greater_equal(T t, U u) noexcept;

template<class R, class T>
    constexpr bool in_range(T t) noexcept;

// 20.3, compile-time integer sequences
template<class T, T...>
    struct integer_sequence;
template<size_t... I>
    using index_sequence = integer_sequence<size_t, I...>;

template<class T, T N>
    using make_integer_sequence = integer_sequence<T, see below>;
template<size_t N>
    using make_index_sequence = make_integer_sequence<size_t, N>;

template<class... T>
    using index_sequence_for = make_index_sequence<sizeof...(T)>;

// 20.4, class template pair
template<class T1, class T2>
    struct pair;

// 20.4.3, pair specialized algorithms
template<class T1, class T2>
    constexpr bool operator==(const pair<T1, T2>&, const pair<T1, T2>&);
template<class T1, class T2>
    constexpr common_comparison_category_t<synth-three-way-result<T1>,
                                            synth-three-way-result<T2>>
        operator<=>(const pair<T1, T2>&, const pair<T1, T2>&);

template<class T1, class T2>
    constexpr void swap(pair<T1, T2>& x, pair<T1, T2>& y) noexcept(noexcept(x.swap(y)));

template<class T1, class T2>
    constexpr see below make_pair(T1&&, T2&&);

// 20.4.4, tuple-like access to pair
template<class T> struct tuple_size;
template<size_t I, class T> struct tuple_element;

template<class T1, class T2> struct tuple_size<pair<T1, T2>>;
template<size_t I, class T1, class T2> struct tuple_element<I, pair<T1, T2>>;

template<size_t I, class T1, class T2>
  constexpr tuple_element_t<I, pair<T1, T2>>& get(pair<T1, T2>&) noexcept;
template<size_t I, class T1, class T2>
  constexpr tuple_element_t<I, pair<T1, T2>>&& get(pair<T1, T2>&&) noexcept;
template<size_t I, class T1, class T2>
  constexpr const tuple_element_t<I, pair<T1, T2>>& get(const pair<T1, T2>&) noexcept;
template<size_t I, class T1, class T2>
  constexpr const tuple_element_t<I, pair<T1, T2>>&& get(const pair<T1, T2>&&) noexcept;
template<class T1, class T2>
  constexpr T1& get(pair<T1, T2>& p) noexcept;
template<class T1, class T2>
  constexpr const T1& get(const pair<T1, T2>& p) noexcept;
template<class T1, class T2>
  constexpr T1&& get(pair<T1, T2>&& p) noexcept;
template<class T1, class T2>
  constexpr const T1&& get(const pair<T1, T2>&& p) noexcept;
template<class T2, class T1>
  constexpr T2& get(pair<T1, T2>& p) noexcept;
template<class T2, class T1>
  constexpr const T2& get(const pair<T1, T2>& p) noexcept;
template<class T2, class T1>
  constexpr T2&& get(pair<T1, T2>&& p) noexcept;
template<class T2, class T1>
  constexpr const T2&& get(const pair<T1, T2>&& p) noexcept;

// 20.4.5, pair piecewise construction
struct piecewise_construct_t {
  explicit piecewise_construct_t() = default;
};
inline constexpr piecewise_construct_t piecewise_construct{};
template<class... Types> class tuple;        // defined in <tuple> (20.5.2)

// in-place construction
struct in_place_t {
  explicit in_place_t() = default;
};
inline constexpr in_place_t in_place{};

template<class T>
  struct in_place_type_t {
    explicit in_place_type_t() = default;
  };
template<class T> inline constexpr in_place_type_t<T> in_place_type{};

template<size_t I>
  struct in_place_index_t {
    explicit in_place_index_t() = default;
  };
template<size_t I> inline constexpr in_place_index_t<I> in_place_index{};
}
```

## 20.2.2 swap [utility.swap]

```
template<class T>
  constexpr void swap(T& a, T& b) noexcept(see below);
```

约束：`is_move_constructible_v<T>` 为 true 且 `is_move_assignable_v<T>` 为 true。

前提条件：类型 T 满足 Cpp17MoveConstructible（表 28）和 Cpp17MoveAssignable（表 30）要求。

效果：交换两个位置存储的值。

说明：此函数是指定定制化点（16.4.5.2.1）。`noexcept` 中的表达式等价于：

```
is_nothrow_move_constructible_v<T> && is_nothrow_move_assignable_v<T>
```

```
template<class T, size_t N>
constexpr void swap(T (&a)[N], T (&b)[N]) noexcept(is_nothrow_swappable_v<T>);
```

约束：`is_swappable_v<T>` 为 true。

前提条件：对于范围 [0, N) 中的所有 i，a[i] 可与（16.4.4.3）b[i] 交换。

效果：如同通过 `swap_ranges(a, a + N, b)`。

## 20.2.3 exchange [utility.exchange]

```
template<class T, class U = T>
constexpr T exchange(T& obj, U&& new_val);
```

效果：等价于：

```
T old_val = std::move(obj);
obj = std::forward<U>(new_val);
return old_val;
```

## 20.2.4 Forward/move helpers [forward]

库提供了模板辅助函数，以简化对左值应用移动语义以及简化转发函数的实现。本小节中指定的所有函数都是信号安全的（17.13.5）。

```
template<class T> constexpr T&& forward(remove_reference_t<T>& t) noexcept;
template<class T> constexpr T&& forward(remove_reference_t<T>&& t) noexcept;
```

强制要求：对于第二个重载，`is_lvalue_reference_v<T>` 为 false。

返回：`static_cast<T&&>(t)`。

[示例 1：

```
template<class T, class A1, class A2>
shared_ptr<T> factory(A1&& a1, A2&& a2) {
  return shared_ptr<T>(new T(std::forward<A1>(a1), std::forward<A2>(a2)));
}

struct A {
  A(int&, const double&);
};

void g() {
  shared_ptr<A> sp1 = factory<A>(2, 1.414); // error: 2 will not bind to int&
  int i = 2;
  shared_ptr<A> sp2 = factory<A>(i, 1.414); // OK
}
```

在第一次调用 factory 时，A1 推导为 int，因此 2 作为右值转发给 A 的构造函数。在第二次调用 factory 时，A1 推导为 int&，因此 i 作为左值转发给 A 的构造函数。在这两种情况下，A2 都推导为 double，因此 1.414 作为右值转发给 A 的构造函数。——示例结束]

```
template<class T> constexpr remove_reference_t<T>&& move(T&& t) noexcept;
```

返回：`static_cast<remove_reference_t<T>&&>(t)`。

[示例 2：

```
template<class T, class A1>
shared_ptr<T> factory(A1&& a1) {
  return shared_ptr<T>(new T(std::forward<A1>(a1)));
}

struct A {
    A();
    A(const A&);      // 从左值复制
    A(A&&);           // 从右值移动
};

void g() {
    A a;
    shared_ptr<A> sp1 = factory<A>(a);                // "a" 绑定到 A(const A&)
    shared_ptr<A> sp2 = factory<A>(std::move(a));     // "a" 绑定到 A(A&&)
}
```

在第一次调用 factory 时，A1 推导为 A&，因此 a 作为非常量左值转发。这绑定到构造函数 A(const A&)，它从 a 复制值。在第二次调用 factory 时，由于调用 std::move(a)，A1 推导为 A，因此 a 作为右值转发。这绑定到构造函数 A(A&&)，它从 a 移动值。——示例结束]

```
template<class T> constexpr conditional_t<!is_nothrow_move_constructible_v<T> && is_copy_constructible_v<T>, const T&, T&&> move_if_noexcept(T& x) noexcept;
```

返回：`std::move(x)`。

## 20.2.5 Function template as_const [utility.as.const]

```
template<class T> constexpr add_const_t<T&> as_const(T& t) noexcept;
```

返回：t。

## 20.2.6 Function template declval [declval]

库提供了函数模板 declval 以简化作为未求值操作数（7.2）出现的表达式的定义。

```
template<class T> add_rvalue_reference_t<T> declval() noexcept;    // as unevaluated operand
```

强制要求：此函数未被 odr 使用（6.3）。

说明：declval 的模板参数 T 可以是不完全类型。

[示例 1：

```
template<class To, class From> decltype(static_cast<To>(declval<From>())) convert(From&&);
```

声明函数模板 convert，只有当类型 From 可以显式转换为类型 To 时才参与重载。另一个示例参见类模板 common_type（20.15.8.7）。——示例结束]

## 20.2.7 Integer comparison functions [utility.intcmp]

```
template<class T, class U>
    constexpr bool cmp_equal(T t, U u) noexcept;
```

强制要求：T 和 U 均为标准整数类型或扩展整数类型（6.8.2）。

效果：等价于：

```
using UT = make_unsigned_t<T>;
using UU = make_unsigned_t<U>;
if constexpr (is_signed_v<T> == is_signed_v<U>)
    return t == u;
else if constexpr (is_signed_v<T>)
    return t < 0 ? false : UT(t) == u;
else
    return u < 0 ? false : t == UU(u);
```

```
template<class T, class U>
    constexpr bool cmp_not_equal(T t, U u) noexcept;
```

效果：等价于：return !cmp_equal(t, u);

