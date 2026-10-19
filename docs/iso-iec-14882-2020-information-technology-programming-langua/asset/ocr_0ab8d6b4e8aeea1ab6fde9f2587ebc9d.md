```
// assignment
unique_ptr& operator=(unique_ptr&& u) noexcept;
template<class U, class E>
    unique_ptr& operator=(unique_ptr<U, E>&& u) noexcept;
unique_ptr& operator=(nullptr_t) noexcept;
```

```
// 20.11.1.4.4, observers
T& operator[](size_t i) const;
pointer get() const noexcept;
deleter_type& get_deleter() noexcept;
const deleter_type& get_deleter() const noexcept;
explicit operator bool() const noexcept;
```

```
// 20.11.1.4.5, modifiers
pointer release() noexcept;
template<class U> void reset(U p) noexcept;
void reset(nullptr_t = nullptr) noexcept;
void swap(unique_ptr& u) noexcept;
```

```
// disable copy from lvalue
unique_ptr(const unique_ptr&) = delete;
unique_ptr& operator=(const unique_ptr&) = delete;
};
}
```

1 A specialization for array types is provided with a slightly altered interface.

+   (1.1) — Conversions between different types of unique_ptr<T[], D> that would be disallowed for the corresponding pointer-to-array types, and conversions to or from the non-array forms of unique_ptr, produce an ill-formed program.

+   (1.2) — Pointers to types derived from T are rejected by the constructors, and by reset.

+   (1.3) — The observers operator* and operator-> are not provided.

+   (1.4) — The indexing observer operator[] is provided.

+   (1.5) — The default deleter will call delete[].

2 Descriptions are provided below only for members that differ from the primary template.

3 The template argument T shall be a complete type.

# 20.11.1.4.2 Constructors [unique.ptr.runtime.ctor]

```
template<class U> explicit unique_ptr(U p) noexcept;
```

1 This constructor behaves the same as the constructor in the primary template that takes a single parameter of type pointer.

2 Constraints:

+   (2.1) — U is the same type as pointer, or

+   (2.2) — pointer is the same type as element_type*, U is a pointer type V*, and V(*) [] is convertible to element_type(*) [].

```
template<class U> unique_ptr(U p, see below d) noexcept;
template<class U> unique_ptr(U p, see below d) noexcept;
```

3 These constructors behave the same as the constructors in the primary template that take a parameter of type pointer and a second parameter.

4 Constraints:

+   (4.1) — U is the same type as pointer,

+   (4.2) — U is nullptr_t, or

+   (4.3) — pointer is the same type as element_type*, U is a pointer type V*, and V(*) [] is convertible to element_type(*) [].