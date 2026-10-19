# ISO/IEC 14882:2020(E)

```
// 20.11.4.7, weak_ptr specialized algorithms
template<class T> void swap(weak_ptr<T>& a, weak_ptr<T>& b) noexcept;
```

```
// 20.11.5, class template owner_less
template<class T = void> struct owner_less;
```

```
// 20.11.6, class template enable_shared_from_this
template<class T> class enable_shared_from_this;
```

```
// 20.11.7, hash support
template<class T> struct hash;
template<class T, class D> struct hash<unique_ptr<T, D>>;
template<class T> struct hash<shared_ptr<T>>;
```

```
// 31.8.7, atomic smart pointers
template<class T> struct atomic;
template<class T> struct atomic<shared_ptr<T>>;
template<class T> struct atomic<weak_ptr<T>>;
}
```

# 20.10.3 Pointer traits [pointer.traits]

# 20.10.3.1 General [pointer.traits.general]

1 The class template pointer_traits supplies a uniform interface to certain attributes of pointer-like types.

```
namespace std {
  template<class Ptr> struct pointer_traits {
    using pointer        = Ptr;
    using element_type   = see below;
    using difference_type = see below;
    template<class U> using rebind = see below;
    static pointer pointer_to(see below r);
  };
  template<class T> struct pointer_traits<T*> {
    using pointer        = T*;
    using element_type   = T;
    using difference_type = ptrdiff_t;
    template<class U> using rebind = U*;
    static constexpr pointer pointer_to(see below r) noexcept;
  };
}
```

# 20.10.3.2 Member types [pointer.traits.types]

```
using element_type = see below;
```

1 Type: Ptr::element_type if the qualified-id Ptr::element_type is valid and denotes a type (13.10.3); otherwise, T if Ptr is a class template instantiation of the form SomePointer<T, Args>, where Args is zero or more type arguments; otherwise, the specialization is ill-formed.

```
using difference_type = see below;
```

2 Type: Ptr::difference_type if the qualified-id Ptr::difference_type is valid and denotes a type (13.10.3); otherwise, ptrdiff_t.

```
template<class U> using rebind = see below;
```

3 Alias template: Ptr::rebind<U> if the qualified-id Ptr::rebind<U> is valid and denotes a type (13.10.3); otherwise, SomePointer<U, Args> if Ptr is a class template instantiation of the form SomePointer<T, Args>, where Args is zero or more type arguments; otherwise, the instantiation of rebind is ill-formed.