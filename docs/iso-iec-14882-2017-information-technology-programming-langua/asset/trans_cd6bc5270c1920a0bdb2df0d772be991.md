

# ISO/IEC 14882:2017(E)

```cpp
using OuterTraits = allocator_traits<OuterAlloc>; // exposition only
scoped_allocator_adaptor<InnerAlls>::..inner; // exposition only
```

```cpp
public:
    using outer_allocator_type = OuterAlloc;
    using inner_allocator_type = see below;

    using value_type = typename OuterTraits::value_type;
    using size_type = typename OuterTraits::size_type;
    using difference_type = typename OuterTraits::difference_type;
    using pointer = typename OuterTraits::pointer;
    using const_pointer = typename OuterTraits::const_pointer;
    using void_pointer = typename OuterTraits::void_pointer;
    using const_void_pointer = typename OuterTraits::const_void_pointer;

    using propagate_on_container_copy_assignment = see below;
    using propagate_on_container_move_assignment = see below;
    using propagate_on_container_swap = see below;
    using is_always_equal = see below;
```

```cpp
template <class Tp>
struct re {
    using other = scoped_allocator_adaptor<Tp,
        OuterTraits::rebind<Tp, InnerAlls...>>;
};
```

```cpp
scoped_allocator_adaptor();
template <class OuterA2>
scoped_allocator_adaptor(OuterA2&&, OuterAlloc,
    const InnerAlls&&) noexcept;
scoped_allocator_adaptor(scoped_allocator_adaptor<OuterA2>&& other) noexcept;
```

```cpp
template <class OuterA2>
scoped_allocator_adaptor(
    const OuterA2&, InnerAlls...&&&& other) noexcept;
template <class OuterA2>
scoped_allocator_adaptor();
scoped_allocator_adaptor(OuterA2&&, InnerAlls...&&&& other) noexcept;
```

```cpp
scoped_allocator_adaptor& operator=(const scoped_allocator_adaptor&) = default;
scoped_allocator_adaptor& operator=(scoped_allocator_adaptor&&) = default;

-scoped_allocator_adaptor();
```

```cpp
inner_allocator_type inner_allocator() noexcept;
const inner_allocator_type inner_allocator() const noexcept;
outer_allocator_type outer_allocator() noexcept;
const outer_allocator_type outer_allocator() const noexcept;
```

```cpp
pointer allocate(size_type n, const void_pointer hint);
void deallocate(pointer p, size_type n);
size_type max() const;
```

§ 23.13.1 © ISO/IEC 2017 - 保留所有 646

```cpp
template <class T, class... Args>
void construct(T* p, Args&&... args);
template <class T1, class T2, class... Args1, class... Args2>
void construct(const T1* p, piecewise_construct_t, tuple<Args1>... x, tuple<Args2>... y);
template <class T1, class T2>
void construct(const T1* p, T2* p);
template <class T1, class T2, class U, class V>
void construct(T1* p, T2* p, U&& x, V&& y);
template <class T1, class T2, class U, class V>
void construct(const T1* p, const T2* p, U&& x, V&& y);
template <class T1, class T2>
void construct(const T1* p, const T2* p, U&& x);
template <class T1, class T2>
void construct(const T1* p, const T2* p, V&& x);

template <class T>
void destroy(T* p);
```

```cpp
scoped_allocator_allocator::select_on_copy_construction() const;
};

template<class OuterAlloc, class... InnerAllocs>
scoped_allocator_allocator(OuterAlloc, InnerAllocs...)
    -> scoped_allocator_allocator<OuterAlloc, InnerAllocs...>(...
```

```cpp
template <class Outer1, class Outer2, class... InnerAllocs>
bool operator==(const scoped_allocator_allocator<Outer1, InnerAllocs...>&& a,
                const scoped_allocator_allocator<Outer2, InnerAllocs...>&& b) noexcept;
template <class Outer1, class Outer2, class... InnerAllocs>
bool operator!=(const scoped_allocator_allocator<Outer1, InnerAllocs...>&& a,
                const scoped_allocator_allocator<Outer2, InnerAllocs...>&& b) noexcept;
```

## 23.13.2 作用域分配器成员类型 [allocator.adapter.types]

using inner_allocator_type = 见下文;

-   1 类型：scoped_allocator_allocator<OuterAlloc>::sizeof(InnerAllocs) 为零，否则，
scoped_allocator_allocator<InnerAllocs...>::
-   2 类型：propagate_on_container_copy_assignment = 见下文；
类型：如果 OuterAlloc 和 InnerAllocs... 集合中的任何 A  allocator_traits<A>::propagate_on_container_copy_assignment::value 为 true，否则为 false_type。
-   3  类型：propagate_on_container_move_assignment = 见下文；
类型：如果 OuterAlloc 和 InnerAllocs... 集合中的任何 A 使得 allocator_traits<A>::propagate_on_container_move_assignment::value 为 true，否则为 false_type。
-   4 类型：propagate_on_container_swap = 见下文；
类型：如果 OuterAlloc 和 InnerAllocs... 集合中的任何 A 使得 allocator_traits<A>::propagate_on_container_swap::value 为 true，否则为 false_type。
-   5 类型：is_always_equal = 见下文；
类型：如果 OuterAlloc 和 InnerAllocs... 集合中的每一个 A 使得 allocator_traits<A>::is_always_equal::value 为 true，否则为 false_type。

## 23.13.3 作用域分配器构造函数 [allocator.adapter.constructors]

scoped_allocator_adaptor();
影响：初始化 scoped_allocator_adaptor 对象。

```cpp
template <class OuterA2>
scoped_allocator_adaptor(OuterA2&&, OuterAlloc,
    const InnerAlls&&) noexcept;
scoped_allocator_adaptor(scoped_allocator_adaptor<OuterA2>&& other) noexcept;
```

```cpp
template <class OuterA2>
scoped_allocator_adaptor(
    const OuterA2&, InnerAlls...&&&& other) noexcept;
template <class OuterA2>
scoped_allocator_adaptor();
scoped_allocator_adaptor(OuterA2&&, InnerAlls...&&&& other) noexcept;
```

```cpp
scoped_allocator_adaptor& operator=(const scoped_allocator_adaptor&) = default;
scoped_allocator_adaptor& operator=(scoped_allocator_adaptor&&) = default;

-scoped_allocator_adaptor();
```

```cpp
inner_allocator_type inner_allocator() noexcept;
const inner_allocator_type inner_allocator() const noexcept;
outer_allocator_type outer_allocator() noexcept;
const outer_allocator_type outer_allocator() const noexcept;
```

```cpp
pointer allocate(size_type n, const void_pointer hint);
void deallocate(pointer p, size_type n);
size_type max() const;
```

## 23.13.4 作用域分配器成员 [allocator.adapter.members]

inner_allocator_type inner_allocator();
影响：初始化 scoped_allocator_adaptor 对象。

```cpp
template <class T, class... Args>
void construct(T* p, Args&&... args);
```

