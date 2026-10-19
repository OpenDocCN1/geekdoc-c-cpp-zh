

由容器使用，第二个分配器被传递给容器元素的构造函数，并且，如果元素本身是容器，则第三个分配器被传递给元素的元素，依此类推。如果容器嵌套的深度大于分配器的数量，则如同单分配器的情况一样，最后一个分配器会被重复使用，用于任何剩余的递归。

> [注 1：`scoped_allocator_adaptor` 派生自外部分配器类型，因此在大多数表达式中可以替代外部分配器类型。—— 尾注]

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

## 20.13.2  成员类型

`using inner_allocator_type = see below;`

1  *类型：* 如果 `sizeof...(InnerAllocs)` 为零，则为 `scoped_allocator_adaptor<OuterAlloc>`；否则为 `scoped_allocator_adaptor<InnerAllocs...>`。

`using propagate_on_container_copy_assignment = see below;`

2  *类型：* 如果 `OuterAlloc` 与 `InnerAllocs...` 的集合中任意 `A` 的 `allocator_traits<A>::propagate_on_container_copy_assignment::value` 为 true，则为 `true_type`；否则为 `false_type`。

`using propagate_on_container_move_assignment = see below;`

3  *类型：* 如果 `OuterAlloc` 与 `InnerAllocs...` 的集合中任意 `A` 的 `allocator_traits<A>::propagate_on_container_move_assignment::value` 为 true，则为 `true_type`；否则为 `false_type`。

`using propagate_on_container_swap = see below;`

4  *类型：* 如果 `OuterAlloc` 与 `InnerAllocs...` 的集合中任意 `A` 的 `allocator_traits<A>::propagate_on_container_swap::value` 为 true，则为 `true_type`；否则为 `false_type`。

`using is_always_equal = see below;`

5  *类型：* 如果 `OuterAlloc` 与 `InnerAllocs...` 的集合中每个 `A` 的 `allocator_traits<A>::is_always_equal::value` 均为 true，则为 `true_type`；否则为 `false_type`。

## 20.13.3  构造函数

```
scoped_allocator_adaptor();
```

1  *效果：* 值初始化 `OuterAlloc` 基类和内部分配器对象。

```
template<class OuterA2>
  scoped_allocator_adaptor(OuterA2&& outerAlloc, const InnerAllocs&... innerAllocs) noexcept;
```

2  *约束：* `is_constructible_v<OuterAlloc, OuterA2>` 为 true。

3  *效果：* 用 `std::forward<OuterA2>(outerAlloc)` 初始化 `OuterAlloc` 基类，并用 `innerAllocs...` 初始化 `inner`（从而用参数列表中相应的分配器递归初始化适配器内的每个分配器）。

```
scoped_allocator_adaptor(const scoped_allocator_adaptor& other) noexcept;
```

4  *效果：* 用 `other` 中相应的分配器初始化适配器内的每个分配器。

```
scoped_allocator_adaptor(scoped_allocator_adaptor&& other) noexcept;
```

5  *效果：* 用 `other` 中相应的分配器移动构造适配器内的每个分配器。

```
template<class OuterA2>
    scoped_allocator_adaptor(
        const scoped_allocator_adaptor<OuterA2, InnerAllocs...>& other) noexcept;
```

约束：`is_constructible_v<OuterAlloc, const OuterA2&>` 为 true。

效果：用 `other` 中相应的分配器初始化适配器内的每个分配器。

```
template<class OuterA2>
    scoped_allocator_adaptor(scoped_allocator_adaptor<OuterA2, InnerAllocs...>&& other) noexcept;
```

约束：`is_constructible_v<OuterAlloc, OuterA2>` 为 true。

效果：用 `other` 中相应的分配器右值初始化适配器内的每个分配器。

## 20.13.4  成员 [allocator.adaptor.members]

1 在 construct 成员函数中，如果表达式 `x.outer_allocator()` 有效（13.10.3），则 `OUTERMOST(x)` 为 `OUTERMOST(x.outer_allocator())`，否则为 `x`；`OUTERMOST_ALLOC_TRAITS(x)` 为 `allocator_traits<remove_reference_t<decltype(OUTERMOST(x))>>`。

> [注 1：`OUTERMOST(x)` 和 `OUTERMOST_ALLOC_TRAITS(x)` 是递归操作。`outer_allocator()` 的定义有责任确保递归终止。对于 `scoped_allocator_adaptor` 的所有实例化，递归都会终止。—— 尾注]

```
inner_allocator_type& inner_allocator() noexcept;
const inner_allocator_type& inner_allocator() const noexcept;
```

返回：如果 `sizeof...(InnerAllocs)` 为零，则为 `*this`；否则为 `inner`。

```
outer_allocator_type& outer_allocator() noexcept;
```

返回：`static_cast<OuterAlloc&>(*this)`。

```
const outer_allocator_type& outer_allocator() const noexcept;
```

返回：`static_cast<const OuterAlloc&>(*this)`。

```
[[nodiscard]] pointer allocate(size_type n);
```

返回：`allocator_traits<OuterAlloc>::allocate(outer_allocator(), n)`。

```
[[nodiscard]] pointer allocate(size_type n, const_void_pointer hint);
```

返回：`allocator_traits<OuterAlloc>::allocate(outer_allocator(), n, hint)`。

```
void deallocate(pointer p, size_type n);
```

效果：如同执行 `allocator_traits<OuterAlloc>::deallocate(outer_allocator(), p, n)`。

```
size_type max_size() const;
```

返回：`allocator_traits<OuterAlloc>::max_size(outer_allocator())`。

```
template<class T, class... Args>
    void construct(T* p, Args&&... args);
```

效果：等价于：

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

效果：调用 `OUTERMOST_ALLOC_TRAITS(*this)::destroy(OUTERMOST(*this), p)`。

