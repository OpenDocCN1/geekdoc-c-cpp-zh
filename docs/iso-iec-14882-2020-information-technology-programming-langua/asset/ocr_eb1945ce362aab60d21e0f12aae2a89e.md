# ISO/IEC 14882:2020(E)

```
struct A {
    A();
    A(const A&);      // copies from lvalues
    A(A&&);           // moves from rvalues
};

void g() {
    A a;
    shared_ptr<A> sp1 = factory<A>(a);                // "a" binds to A(const A&)
    shared_ptr<A> sp1 = factory<A>(std::move(a));     // "a" binds to A(A&&)
}
```

In the first call to factory, A1 is deduced as A&, so a is forwarded as a non-const lvalue. This binds to the constructor A(const A&), which copies the value from a. In the second call to factory, because of the call std::move(a), A1 is deduced as A, so a is forwarded as an rvalue. This binds to the constructor A(A&&), which moves the value from a. — end example]

```
template<class T> constexpr conditional_t<!is_nothrow_move_constructible_v<T> && is_copy_constructible_v<T>, const T&, T&&> move_if_noexcept(T& x) noexcept;
```

Returns: std::move(x).

# 20.2.5 Function template as_const [utility.as.const]

```
template<class T> constexpr add_const_t<T&> as_const(T& t) noexcept;
```

Returns: t.

# 20.2.6 Function template declval [declval]

The library provides the function template declval to simplify the definition of expressions which occur as unevaluated operands (7.2).

```
template<class T> add_rvalue_reference_t<T> declval() noexcept;    // as unevaluated operand
```

Mandates: This function is not odr-used (6.3).

Remarks: The template parameter T of declval may be an incomplete type.

[Example 1:
template<class To, class From> decltype(static_cast<To>(declval<From>())) convert(From&&);
declares a function template convert which only participates in overloading if the type From can be explicitly converted to type To. For another example see class template common_type (20.15.8.7). — end example]

# 20.2.7 Integer comparison functions [utility.intcmp]

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