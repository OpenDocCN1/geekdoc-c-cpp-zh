# ISO/IEC 14882:2017(E)

```
template <class T1, D1, class T2, class D2>
bool operator=(const unique_ptr<T1>& x, const unique_ptr<T2>& y);
    return (x < y);
```

Returns:(x < y);

```
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t) noexcept;
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x) noexcept;
```

Returns:x;

```
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t) noexcept;
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x) noexcept;
```

Returns:(bool);

```
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

13 Requires: The specialization <unique_ptr<T, D>::pointer> should be a function object type (23.14) that induces a strict ordering (28.7) on the pointer values.

14 Returns: The first function template returns <unique_ptr<T, D>::pointer>(x.get(), nullptr). The second function template returns <unique_ptr<T, D>::pointer>(nullptr, nullptr);

```
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

15 Returns: The first function template returns nullptr < x. The second function template returns x < (nullptr).

```
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

16 Returns: The first function template returns !(nullptr < x). The second function template returns !(x < nullptr).

```
template <class T, class D>
bool operator=(const unique_ptr<T, D>& x, nullptr_t);
template <class T, class D>
bool operator=(nullptr_t, const unique_ptr<T, D>& x);
```

17 Returns: The first function template returns !(x < nullptr). The second function template returns !(nullptr < nullptr).

# 23.11.2 Shared-ownership pointers [util.smartptr]

# 23.11.2.1 Class bad_weak_ptr [util.smartptr.weak.bad]

§ 23.11.2.1 ©ISO/IEC 2017 - All rights reserved 618