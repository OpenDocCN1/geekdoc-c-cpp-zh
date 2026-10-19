
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

Constraints: is_move_constructible_v<T> is true and is_move_assignable_v<T> is true.

Preconditions: Type T meets the Cpp17MoveConstructible (Table 28) and Cpp17MoveAssignable (Table 30) requirements.

Effects: Exchanges values stored in two locations.

Remarks: This function is a designated customization point (16.4.5.2.1). The expression inside noexcept is equivalent to:

```
is_nothrow_move_constructible_v<T> && is_nothrow_move_assignable_v<T>
```

```
template<class T, size_t N>
constexpr void swap(T (&a)[N], T (&b)[N]) noexcept(is_nothrow_swappable_v<T>);
```

Constraints: is_swappable_v<T> is true.

Preconditions: a[i] is swappable with (16.4.4.3) b[i] for all i in the range [0, N).

Effects: As if by swap_ranges(a, a + N, b).

## 20.2.3 exchange [utility.exchange]

```
template<class T, class U = T>
constexpr T exchange(T& obj, U&& new_val);
```

Effects: Equivalent to:

```
T old_val = std::move(obj);
obj = std::forward<U>(new_val);
return old_val;
```

## 20.2.4 Forward/move helpers [forward]

The library provides templated helper functions to simplify applying move semantics to an lvalue and to simplify the implementation of forwarding functions. All functions specified in this subclause are signal-safe (17.13.5).

```
template<class T> constexpr T&& forward(remove_reference_t<T>& t) noexcept;
template<class T> constexpr T&& forward(remove_reference_t<T>&& t) noexcept;
```

Mandates: For the second overload, is_lvalue_reference_v<T> is false.

Returns: static_cast<T&&>(t).

[Example 1:

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

In the first call to factory, A1 is deduced as int, so 2 is forwarded to A's constructor as an rvalue. In the second call to factory, A1 is deduced as int&, so i is forwarded to A's constructor as an lvalue. In both cases, A2 is deduced as double, so 1.414 is forwarded to A's constructor as an rvalue. — end example]

```
template<class T> constexpr remove_reference_t<T>&& move(T&& t) noexcept;
```

Returns: static_cast<remove_reference_t<T>&&>(t).

[Example 2:

```
template<class T, class A1>
shared_ptr<T> factory(A1&& a1) {
  return shared_ptr<T>(new T(std::forward<A1>(a1)));
}

struct A {
    A();
    A(const A&);      // copies from lvalues
    A(A&&);           // moves from rvalues
};

void g() {
    A a;
    shared_ptr<A> sp1 = factory<A>(a);                // "a" binds to A(const A&)
    shared_ptr<A> sp2 = factory<A>(std::move(a));     // "a" binds to A(A&&)
}
```

In the first call to factory, A1 is deduced as A&, so a is forwarded as a non-const lvalue. This binds to the constructor A(const A&), which copies the value from a. In the second call to factory, because of the call std::move(a), A1 is deduced as A, so a is forwarded as an rvalue. This binds to the constructor A(A&&), which moves the value from a. — end example]

```
template<class T> constexpr conditional_t<!is_nothrow_move_constructible_v<T> && is_copy_constructible_v<T>, const T&, T&&> move_if_noexcept(T& x) noexcept;
```

Returns: std::move(x).

## 20.2.5 Function template as_const [utility.as.const]

```
template<class T> constexpr add_const_t<T&> as_const(T& t) noexcept;
```

Returns: t.

## 20.2.6 Function template declval [declval]

The library provides the function template declval to simplify the definition of expressions which occur as unevaluated operands (7.2).

```
template<class T> add_rvalue_reference_t<T> declval() noexcept;    // as unevaluated operand
```

Mandates: This function is not odr-used (6.3).

Remarks: The template parameter T of declval may be an incomplete type.

[Example 1:

```
template<class To, class From> decltype(static_cast<To>(declval<From>())) convert(From&&);
```

declares a function template convert which only participates in overloading if the type From can be explicitly converted to type To. For another example see class template common_type (20.15.8.7). — end example]

## 20.2.7 Integer comparison functions [utility.intcmp]

```
template<class T, class U>
    constexpr bool cmp_equal(T t, U u) noexcept;
```

Mandates: Both T and U are standard integer types or extended integer types (6.8.2).

Effects: Equivalent to:

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

Effects: Equivalent to: return !cmp_equal(t, u);
