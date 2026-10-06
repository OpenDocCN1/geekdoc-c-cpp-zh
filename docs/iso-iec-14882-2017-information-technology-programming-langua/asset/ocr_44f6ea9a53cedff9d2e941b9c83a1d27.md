# ISO/IEC 14882:2017(E)

nullptr.

```
template <class T>
bool operator<==(const shared_ptr<T>& a, nullptr_t) noexcept;
template <class T>
bool operator<==(nullptr_t, const shared_ptr<T>& a) noexcept;
```

8 Returns: The first function template returns !(nullptr < a). The second function template returns !(a < nullptr).

```
template <class T>
bool operator<==(const shared_ptr<T>& a, nullptr_t) noexcept;
template <class T>
bool operator<==(nullptr_t, const shared_ptr<T>& a) noexcept;
```

9 Returns: The first function template returns !(a < nullptr). The second function template returns !(nullptr < a).

# 23.11.2.2 shared_ptr specialized algorithms

[util.smartptr.shared.spec]

```
template <class T>
void swap(shared_ptr<T>& a, shared_ptr<T>& b) noexcept;
```

1 Effects: Equivalent to a.swap(b).

# 23.11.2.2.9 shared_ptr casts

[util.smartptr.shared.cast]

```
template <class T, U>
shared_ptr<T> static_cast(const shared_ptr<U>& r) noexcept;
```

2 Requires: The expression const_cast((U*)nullptr) shall be well formed.

Returns:

> shared_ptr<T>(r, static_cast<typename r::element_type>(static_cast<T*>(r.get()))) will eventually result in undefined behavior, attempting to delete the same object twice. — end

```
template <class T, U>
shared_ptr<T> dynamic_cast(const shared_ptr<U>& r) noexcept;
```

4 Requires: The expression const_cast<T*>((U*)nullptr) shall be well formed and shall have well-defined behavior.

5 Returns:

+   (5.1) When dynamic_cast<typename shared_ptr<T>::element_type*>(r.get()) returns a non-null value, shared_ptr<T>(r, p).

+   (5.2) Otherwise, shared_ptr<T>().

> 6 [Note: The seemingly equivalent expression static_cast<const T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end

```
template <class T, U>
shared_ptr<T> const_cast(const shared_ptr<U>& r) noexcept;
```

7 Requires: The expression const_cast<T*>((U*)nullptr) shall be well formed.

8 Returns:

```
shared_ptr<T>(r, const_cast<typename shared_ptr<T>::element_type*>(r.get()))
```

§ 23.11.2.2.9 ©ISO/IEC 2017 — All rights reserved 627