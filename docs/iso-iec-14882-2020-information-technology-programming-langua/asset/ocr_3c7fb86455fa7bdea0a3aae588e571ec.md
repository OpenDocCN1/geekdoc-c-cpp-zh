# ISO/IEC 14882:2020(E)

> [Note 2: The seemingly equivalent expression shared_ptr<T>(dynamic_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

```
template<class T, class U>
  shared_ptr<T> const_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
  shared_ptr<T> const_pointer_cast(shared_ptr<U>&& r) noexcept;
```

Mandates: The expression const_cast<T*>((U*)nullptr) is well-formed.

Returns:

  shared_ptr<T>(R, const_cast<typename shared_ptr<T>::element_type*>(r.get()))

where R is r for the first overload, and std::move(r) for the second.

> [Note 3: The seemingly equivalent expression shared_ptr<T>(const_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

```
template<class T, class U>
  shared_ptr<T> reinterpret_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
  shared_ptr<T> reinterpret_pointer_cast(shared_ptr<U>&& r) noexcept;
```

Mandates: The expression reinterpret_cast<T*>((U*)nullptr) is well-formed.

Returns:

  shared_ptr<T>(R, reinterpret_cast<typename shared_ptr<T>::element_type*>(r.get()))

where R is r for the first overload, and std::move(r) for the second.

> [Note 4: The seemingly equivalent expression shared_ptr<T>(reinterpret_cast<T*>(r.get())) will eventually result in undefined behavior, attempting to delete the same object twice. — end note]

# 20.11.3.11 get_deleter

[util.smartptr.getdeleter]

```
template<class D, class T>
  D* get_deleter(const shared_ptr<T>& p) noexcept;
```

Returns: If p owns a deleter d of type cv-unqualified D, returns addressof(d); otherwise returns nullptr. The returned pointer remains valid as long as there exists a shared_ptr instance that owns d.

> [Note 1: It is unspecified whether the pointer remains valid longer than that. This can happen if the implementation doesn't destroy the deleter until all weak_ptr instances that share ownership with p have been destroyed. — end note]

# 20.11.3.12 I/O

[util.smartptr.shared.io]

```
template<class E, class T, class Y>
  basic_ostream<E, T>& operator<<(basic_ostream<E, T>& os, const shared_ptr<Y>& p);
```

Effects: As if by: os << p.get();

Returns: os.

# 20.11.4 Class template weak_ptr

[util.smartptr.weak]

# 20.11.4.1 General

[util.smartptr.weak.general]

The weak_ptr class template stores a weak reference to an object that is already managed by a shared_ptr. To access the object, a weak_ptr can be converted to a shared_ptr using the member function lock.

```
namespace std {
  template<class T> class weak_ptr {
  public:
    using element_type = remove_extent_t<T>;

    // 20.11.4.2, constructors
    constexpr weak_ptr() noexcept;
    template<class Y>
      weak_ptr(const shared_ptr<Y>& r) noexcept;
    weak_ptr(const weak_ptr& r) noexcept;
```