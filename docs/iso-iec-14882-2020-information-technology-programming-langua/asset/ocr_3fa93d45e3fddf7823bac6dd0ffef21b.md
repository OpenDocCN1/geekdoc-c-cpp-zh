# ISO/IEC 14882:2020(E)

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

# 20.2.3 exchange [utility.exchange]

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

# 20.2.4 Forward/move helpers [forward]

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
```