# ISO/IEC 14882:2017(E)

# 23.13.3 Scoped allocator adaptor constructors [allocator.adaptor.cnstr]

scoped_allocator_adapter();
Effects: Initializes the OuterAlloc base class and the inner allocator object.

```
template <class Outer2>
scoped_allocator_adapter(Outer2&& outerAlloc,
                           const InnerAllocs&... innerAllocs) noexcept;
```

+   2 Effects: Initializes the OuterAlloc base class with std::forward<Outer2>(outerAlloc) and inner with innerAllocs... (hence recursively initializing each allocator with the adapter with the corresponding allocator from the argument list).

+   3 Remarks: This constructor shall not participate in overload resolution unless is_constructible-<vOuterAlloc, Outer2> is true.
scoped_allocator_adapter(const scoped_allocator_adapter&& other) noexcept;

+   4 Effects: Initializes each allocator within the adapter with the corresponding allocator from other.
scoped_allocator_adapter(scoped_allocator_adapter&& other) noexcept;

+   5 Effects: Move constructs each allocator within the adapter with the corresponding allocator from other.

```
template <class Outer2>
scoped_allocator_adapter(const scoped_allocator_adapter<Outer2, InnerAllocs...>&& other) noexcept;n
```

+   6 Effects: Initializes each allocator within the adapter with the corresponding allocator from other.

+   7 Remarks: This constructor shall not participate in overload resolution unless is_constructible-<vOuterAlloc, Outer2> is true.

```
template <class Outer2>
scoped_allocator_adapter(scoped_allocator_adapter<Outer2, InnerAllocs...>&& other) noexcept;
other.
```

+   8 Effects: Initializes each allocator within the adapter with the corresponding allocator value from other.

+   9 Remarks: This constructor shall not participate in overload resolution unless is_constructible-<vOuterAlloc, Outer2> is true.

# 23.13.4 Scoped allocator adaptor members [allocator.adaptor.members]

1 In the construct member function, OUTERMOST(x) is x if x does not have an outer allocator() member and function OUTERMOST(x, outer_allocator()); otherwise; OUTERMOST_TRAITS(x) is allocator_traits<decltype(OUTERMOST(x))>. Note: OUTERMOST(x) and OUTERMOST_TRAITS(x) are recursive operations. It is implement in the definition of outer_allocator() to ensure that the recursion terminates.
It will terminate all instantiations of scoped_allocator_adapter. — end note

```
inner_allocator_type& inner_allocator() noexcept;
const inner_allocator_type& inner_allocator() const noexcept;
```

+   2 Returns: *this if sizeof...(InnerAllocs) is zero; otherwise, inner.
outer_allocator_type& outer_allocator() const noexcept;

+   3 Returns: static_cast<OuterAlloc&>(*this).

©ISO/IEC 2017 - All rights reserved 648