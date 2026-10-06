# ISO/IEC 14882:2017(E)

```
// 23.11.2.6. shared_ptr creation
template<class T, class... Args>
shared_ptr<T> make_shared(Args&&... args);
template<class T, class A, class... Args>
shared_ptr<T> allocate(const A& a, Args&&... args) noexcept;
```

```
// 23.11.2.7. shared_ptr comparisons
template<class T, class U>
bool operator=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template<class T, class U>
bool operator!(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template<class T, class U>
bool operator<(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template<class T, class U>
bool operator>(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template<class T, class U>
bool operator<=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template<class T, class U>
bool operator>=(const shared_ptr<T>& a, const shared_ptr<U>& b) noexcept;
template<class T>
bool operator==(multiptr_t, const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator==(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator==(multiptr_t, const shared_ptr<T>& x, y) noexcept;
template<class T>
bool operator!=(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator!=(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator!=(multiptr_t, const shared_ptr<T>& x, y) noexcept;
template<class T>
bool operator<=(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator<=(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator<=(multiptr_t, const shared_ptr<T>& x, y) noexcept;
template<class T>
bool operator>=(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator>=(const shared_ptr<T>& x, nullptr_t) noexcept;
template<class T>
bool operator>=(multiptr_t, const shared_ptr<T>& x, y) noexcept;
```

```
// 23.11.2.8. shared_ptr specialized algorithms
template<class T>
void swap(shared_ptr<T>& a, shared_ptr<T>& b) noexcept;
```

```
// 23.11.2.9. shared_ptr casts
template<class T, class U>
shared_ptr<T> static_pointer_cast(const shared_ptr<U>& r) noexcept;
template<class T, class U>
shared_ptr<T> dynamic_pointer_cast(const shared_ptr<U>& r) noexcept;
```