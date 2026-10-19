
used by the container, the second allocator is passed to the constructors of the container’s elements, and, if the elements themselves are containers, the third allocator is passed to the elements’ elements, and so on. If containers are nested to a depth greater than the number of allocators, the last allocator is used repeatedly, as in the single-allocator case, for any remaining recursions.

> [Note 1: The `scoped_allocator_adaptor` is derived from the outer allocator type so it can be substituted for the outer allocator type in most expressions. — end note]

```
namespace std {
    template<class OuterAlloc, class... InnerAllocs>
    class scoped_allocator_adaptor : public OuterAlloc {
    private:
        using OuterTraits = allocator_traits<OuterAlloc>;    // exposition only
        scoped_allocator_adaptor<InnerAllocs...> inner;      // exposition only

    public:
        using outer_allocator_type = OuterAlloc;
        using inner_allocator_type = see below;

        using value_type            = typename OuterTraits::value_type;
        using size_type             = typename OuterTraits::size_type;
        using difference_type       = typename OuterTraits::difference_type;
        using pointer               = typename OuterTraits::pointer;
        using const_pointer         = typename OuterTraits::const_pointer;
        using void_pointer          = typename OuterTraits::void_pointer;
        using const_void_pointer    = typename OuterTraits::const_void_pointer;

        using propagate_on_container_copy_assignment = see below;
        using propagate_on_container_move_assignment = see below;
        using propagate_on_container_swap            = see below;
        using is_always_equal                        = see below;

        template<class Tp> struct rebind {
            using other = scoped_allocator_adaptor<
                OuterTraits::template rebind_alloc<Tp>, InnerAllocs...>;
        };

        scoped_allocator_adaptor();
        template<class OuterA2>
            scoped_allocator_adaptor(OuterA2&& outerAlloc,
                const InnerAllocs&... innerAllocs) noexcept;

        scoped_allocator_adaptor(const scoped_allocator_adaptor& other) noexcept;
        scoped_allocator_adaptor(scoped_allocator_adaptor&& other) noexcept;

        template<class OuterA2>
            scoped_allocator_adaptor(
                const scoped_allocator_adaptor<OuterA2, InnerAllocs...>& other) noexcept;
        template<class OuterA2>
            scoped_allocator_adaptor(
                scoped_allocator_adaptor<OuterA2, InnerAllocs...>&& other) noexcept;

        scoped_allocator_adaptor& operator=(const scoped_allocator_adaptor&) = default;
        scoped_allocator_adaptor& operator=(scoped_allocator_adaptor&&) = default;

        ~scoped_allocator_adaptor();

        inner_allocator_type& inner_allocator() noexcept;
        const inner_allocator_type& inner_allocator() const noexcept;
        outer_allocator_type& outer_allocator() noexcept;
        const outer_allocator_type& outer_allocator() const noexcept;

        [[nodiscard]] pointer allocate(size_type n);
        [[nodiscard]] pointer allocate(size_type n, const_void_pointer hint);
        void deallocate(pointer p, size_type n);

        size_type max_size() const;

        template<class T, class... Args>
          void construct(T* p, Args&&... args);

        template<class T>
          void destroy(T* p);

        scoped_allocator_adaptor select_on_container_copy_construction() const;
    };

    template<class OuterAlloc, class... InnerAllocs>
        scoped_allocator_adaptor<OuterAlloc, InnerAllocs...>
            -> scoped_allocator_adaptor<OuterAlloc, InnerAllocs...>;
}
```

## 20.13.2  Member types

`using inner_allocator_type = see below;`

1  *Type:* `scoped_allocator_adaptor<OuterAlloc>` if `sizeof...(InnerAllocs)` is zero; otherwise, `scoped_allocator_adaptor<InnerAllocs...>`.

`using propagate_on_container_copy_assignment = see below;`

2  *Type:* `true_type` if `allocator_traits<A>::propagate_on_container_copy_assignment::value` is true for any `A` in the set of `OuterAlloc` and `InnerAllocs...`; otherwise, `false_type`.

`using propagate_on_container_move_assignment = see below;`

3  *Type:* `true_type` if `allocator_traits<A>::propagate_on_container_move_assignment::value` is true for any `A` in the set of `OuterAlloc` and `InnerAllocs...`; otherwise, `false_type`.

`using propagate_on_container_swap = see below;`

4  *Type:* `true_type` if `allocator_traits<A>::propagate_on_container_swap::value` is true for any `A` in the set of `OuterAlloc` and `InnerAllocs...`; otherwise, `false_type`.

`using is_always_equal = see below;`

5  *Type:* `true_type` if `allocator_traits<A>::is_always_equal::value` is true for every `A` in the set of `OuterAlloc` and `InnerAllocs...`; otherwise, `false_type`.

## 20.13.3  Constructors

```
scoped_allocator_adaptor();
```

1  *Effects:* Value-initializes the `OuterAlloc` base class and the inner allocator object.

```
template<class OuterA2>
  scoped_allocator_adaptor(OuterA2&& outerAlloc, const InnerAllocs&... innerAllocs) noexcept;
```

2  *Constraints:* `is_constructible_v<OuterAlloc, OuterA2>` is true.

3  *Effects:* Initializes the `OuterAlloc` base class with `std::forward<OuterA2>(outerAlloc)` and `inner` with `innerAllocs...` (hence recursively initializing each allocator within the adaptor with the corresponding allocator from the argument list).

```
scoped_allocator_adaptor(const scoped_allocator_adaptor& other) noexcept;
```

4  *Effects:* Initializes each allocator within the adaptor with the corresponding allocator from `other`.

```
scoped_allocator_adaptor(scoped_allocator_adaptor&& other) noexcept;
```

5  *Effects:* Move constructs each allocator within the adaptor with the corresponding allocator from `other`.

```
template<class OuterA2>
    scoped_allocator_adaptor(
        const scoped_allocator_adaptor<OuterA2, InnerAllocs...>& other) noexcept;
```

Constraints: `is_constructible_v<OuterAlloc, const OuterA2&>` is true.

Effects: Initializes each allocator within the adaptor with the corresponding allocator from `other`.

```
template<class OuterA2>
    scoped_allocator_adaptor(scoped_allocator_adaptor<OuterA2, InnerAllocs...>&& other) noexcept;
```

Constraints: `is_constructible_v<OuterAlloc, OuterA2>` is true.

Effects: Initializes each allocator within the adaptor with the corresponding allocator rvalue from `other`.

## 20.13.4  Members [allocator.adaptor.members]

1 In the construct member functions, `OUTERMOST(x)` is `OUTERMOST(x.outer_allocator())` if the expression `x.outer_allocator()` is valid (13.10.3) and `x` otherwise; `OUTERMOST_ALLOC_TRAITS(x)` is `allocator_traits<remove_reference_t<decltype(OUTERMOST(x))>>`.

> [Note 1: `OUTERMOST(x)` and `OUTERMOST_ALLOC_TRAITS(x)` are recursive operations. It is incumbent upon the definition of `outer_allocator()` to ensure that the recursion terminates. It will terminate for all instantiations of `scoped_allocator_adaptor`. — end note]

```
inner_allocator_type& inner_allocator() noexcept;
const inner_allocator_type& inner_allocator() const noexcept;
```

Returns: `*this` if `sizeof...(InnerAllocs)` is zero; otherwise, `inner`.

```
outer_allocator_type& outer_allocator() noexcept;
```

Returns: `static_cast<OuterAlloc&>(*this)`.

```
const outer_allocator_type& outer_allocator() const noexcept;
```

Returns: `static_cast<const OuterAlloc&>(*this)`.

```
[[nodiscard]] pointer allocate(size_type n);
```

Returns: `allocator_traits<OuterAlloc>::allocate(outer_allocator(), n)`.

```
[[nodiscard]] pointer allocate(size_type n, const_void_pointer hint);
```

Returns: `allocator_traits<OuterAlloc>::allocate(outer_allocator(), n, hint)`.

```
void deallocate(pointer p, size_type n);
```

Effects: As if by: `allocator_traits<OuterAlloc>::deallocate(outer_allocator(), p, n)`.

```
size_type max_size() const;
```

Returns: `allocator_traits<OuterAlloc>::max_size(outer_allocator())`.

```
template<class T, class... Args>
    void construct(T* p, Args&&... args);
```

Effects: Equivalent to:

```
    apply([p, this](auto&&... newargs) {
        OUTERMOST_ALLOC_TRAITS(*this)::construct(
            OUTERMOST(*this), p,
            std::forward<decltype(newargs)>(newargs)...);
    },
    uses_allocator_construction_args<T>(inner_allocator(),
        std::forward<Args>(args)...));
```

```
template<class T>
    void destroy(T* p);
```

Effects: Calls `OUTERMOST_ALLOC_TRAITS(*this)::destroy(OUTERMOST(*this), p)`.
