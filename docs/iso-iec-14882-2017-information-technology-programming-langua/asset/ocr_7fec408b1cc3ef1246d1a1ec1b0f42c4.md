# ISO/IEC 14882:2017(E)

(2.1) — U is the same type as **pointer**,

(2.2) — U is nullptr_t, or

(2.3) — pointer is the same type as **element_type***, U is a pointer type V*, and V(*) [] is convertible to **element_type(*)[]**.

```
template <class U, class E>
unique_ptr(unique_ptr<U>, E&& u) noexcept;
```

3 This constructor behaves the same as in the primary template, except that it shall not participate in overload resolution unless all of the following conditions hold, where UP is unique_ptr<U, E>:

(3.1) — U is an array type,

(3.2) — pointer is the same type as **element_type***, and

(3.3) — UP::pointer is the same type as UP::element_type*, and

(3.4) — element_type(*)[] is convertible to element_type(*)[], and

(3.5) — either D is a reference type and E is the same type as D, or D is not a reference type and E is implicitly convertible to D.

> [Note: This replaces the overload-resolution specification of the primary template — end note]

# 23.11.1.3 **unique_ptr assignment** [unique_ptr.runtime.asgn]

```
template <class U, class E>
unique_ptr& operator(unique_ptr<U>, E&& u) noexcept;
```

1 This operator behaves the same as in the primary template

(1.1) — U is an array type,

(1.2) — pointer is the same type as **element_type***,

(1.3) — UP::pointer is the same type as UP::element_type*,

(1.4) — element_type(*)[] is convertible to element_type(*)[], and

(1.5) — is_assignable_v<D, E&&> is true.

> [Note: This replaces the overload-resolution specification of the primary template — end note]

# 23.11.1.3.3 **unique_ptr observers** [unique_ptr.runtime.observers]

```
operator()(size_t i) const;
```

1 Requires: i < the number of elements in the array to which the stored pointer points.

2 Returns: get().

# 23.11.1.3.4 **unique_ptr modifiers** [unique_ptr.runtime.modifiers]

```
void reset(unique_ptr p = nullptr) noexcept;
```

1 Effects: Equivalent to reset(pointer()).

```
template <class U> void reset(U p) noexcept;
```

2 This function behaves the same as in the primary template, except that it shall not participate in overload resolution unless either

(2.1) — U is the same type as pointer, or