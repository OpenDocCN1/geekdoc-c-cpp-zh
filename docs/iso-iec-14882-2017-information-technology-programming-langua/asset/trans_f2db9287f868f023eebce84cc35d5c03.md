

# ISO/IEC 14882:2017(E)

11 效果：等效于：

```
construct(p, piecewise_construct,
    forward_as_tuple(std::vector<U>(x)),
    forward_as_tuple(std::vector<V>(y)));
```

template <class T1, T2, class U, class V>
void construct(pair<T1, T2>* p, const pair<U, V>& pr);

12 效果：等效于：

```
construct(p, piecewise_construct,
    forward_as_tuple(pr.first),
    forward_as_tuple(pr.second));
```

template <class T1, T2, class U, class V>
void construct(pair<T1, T2>* p, const pair<U, V>& pr);

13 效果：等效于：

```
construct(p, piecewise_construct,
    forward_as_tuple(std::forward<U>(pr.first)),
    forward_as_tuple(std::forward<V>(pr.second));
```

template <class T>
void destroy(T* p);

14 效果：相当于 p->T()。

polymorphic_allocator select_on_container_copy_construction() const;

15 返回：polymorphic_allocator()。

> [注：内存资源不会传播。 — 结束]

memory_resource* resource() const;

17 返回：memory_rsrc。

## 23.1.2.3 polymorphic_allocator 等等性 [mem.poly.allocator.eq]

```
template <class T1, T2>
bool operator==(const polymorphic_allocator<T1>& a,
    const polymorphic_allocator<T2>& b) noexcept
```

- 1 返回：*a.resource() == *b.resource();*

```
template <class T1, T2>
bool operator!=(const polymorphic_allocator<T1>& a,
    const polymorphic_allocator<T2>& b) noexcept
```

- 2 返回：!(a == b);

## 23.1.2.4 访问全局 memory_resource 对象 [mem.res.global]

memory_resource* new_delete_resource() noexcept;

- 1 返回：一个指向静态存储期对象的指针，该对象的类型派自 memory_resource，并可以作为使用 ::operator new 和 ::operator delete 分配内存的资源。每次调用此函数时都返回上一个右值。对于返回值 p 和内存资源 r，p->is_equal(r) 返回 true && r == p。

memory_resource* null_memory_resource() noexcept;

返回：一个指向静态存储期对象的指针，该对象的类型派自 memory_resource，其 allocate() 会抛出 bad_alloc 且 deallocate() 无效果。每次调用此函数都会返回相同的值。对于返回值 p 和内存资源 r，p->is_equal(r) 返回 r == p。

3 默认内存资源指针是一个指向内存资源的指针，当没有通过接口显式提供内存资源时，某些设施将使用该资源。它的初始值为 new_delete_resource() 的返回值。

memory_resource* set_delete_resource(memory_resource* r) noexcept;

- 4 效果：如果 r 不为空，则将默认内存资源指针设置为 r；否则将默认内存资源指针设置为 new_delete_resource()。

- 5 后置条件：get_delete_resource() == r。

- 6 返回：默认内存资源指针的返回值。

- 7 备注：调用 set_delete_resource 和 get_delete_resource 函数不应产生数据竞态。对 set_delete_resource 函数的调用应与后续 set_delete_resource 和 get_delete_resource 函数的调用同步。

memory_resource* get_delete_resource() noexcept;

- 8 返回：默认内存资源指针的当前值。

## 23.12.5 池资源类

## 23.12.1 synchronized_pool_resource 和 unsynchronized_pool_resource [mem.res_pool.overview]

- 1 synchronized_pool_resource 和 unsynchronized_pool_resource 类（统称为池资源类）是通用内存资源，具有以下特性：
-- 如果在销析构时没有对某些块调用 deallocate，则每个资源都会释放其分配的内存。
-- 内存池资源由多个池（pools）组成，用于不同的块大小。每个单独的池管理一组块（chunks），这些块被划分为均匀大小的单元，通过调用 allocate() 返回。每次调用 allocate(size, alignment) 都会被分发到能够容纳至少该块大小的池。
-- 当池耗尽时，从池中分配一个块将导致从上游分配器（在构造时提供）分配一个额外的块，以补充池。每次成功补充后，块的大小按几何级数增加。[注：通过按块块进行分配，池化策略增加了连续分配在大小上更接近且不浪费的概率]。
-- 超过任何池的最大块大小的分配请求将直接从上游分配器完全满足。
-- 可以将 A_options 结构体传递给池资源的构造函数，以调整最大块大小和最大块大小。

- 2 synchronized_pool_resource 可以从多个线程进行访问而无需外部同步，并可能具有线程安全的池以减少同步开销。unsynchronized_pool_resource 类可能被从多个线程同时访问，从而避免了单线程应用程序中的同步开销。

```cpp
struct pool_options {
    size_t max_blocks_per_chunk = 0;
    size_t largest_required_pool_block = 0;
};
```

```cpp
class synchronized_pool_resource : memory_resource {
public:
    synchronized_pool_resource(const pool_options& opts, memory_resource* upstream);

    synchronized_pool_resource();
    synchronized_pool_resource(const pool_options& opts);
    synchronized_pool_resource(memory_resource* upstream);
    synchronized_pool_resource() :() {
        synchronized_pool_resource(opts, get_delete_resource());
    }

    synchronized_pool_resource(const pool_resource&) = delete;
    virtual ~synchronized_pool_resource();

    synchronized_pool_resource& operator=(const pool_resource&) = delete;

    void release();
    memory_resource* upstream_resource() const;
    pool_options options() const;

protected:
    void* _do_allocate(size_t bytes, size_t alignment) override;
    void _do_deallocate(void* p, size_t bytes, size_t alignment) override;
    bool _is_equal(const memory_resource& other) const noexcept;
};
```

```cpp
class unsynchronized_pool_resource : memory_resource {
public:
    unsynchronized_pool_resource(const pool_options& opts, memory_resource* upstream);

    unsynchronized_pool_resource();
    unsynchronized_pool_resource(const pool_options& opts);
    unsynchronized_pool_resource(memory_resource* upstream);
    unsynchronized_pool_resource() :() {
        unsynchronized_pool_resource(opts, get_delete_resource());
    }

    unsynchronized_pool_resource(const pool_resource&) = delete;
    virtual ~unsynchronized_pool_resource();

    unsynchronized_pool_resource& operator=(const pool_resource&) = delete;

    void release();
    memory_resource* upstream_resource() const;
    pool_options options() const;

protected:
    void* _do_allocate(size_t bytes, size_t alignment) override;
    void _do_deallocate(void* p, size_t bytes, size_t alignment) override;
    bool _is_equal(const memory_resource& other) const noexcept;
};
```

## 23.12.2 pool_options 数据成员 [mem.res.options]

- 1 pool_options 的成员组成用于池资源的一组选项。每个选项对池行为的影响描述如下：
size_t max_blocks_per_chunk;
2 从上游内存资源一次性分配的最大块数（23.12.6）以补充池。如果 max_blocks_per_chunk 为 0 或大于实现的限制，则使用该限制。实现可能会选择比该字段更小的值。
size_t largest_required_pool_block;
3 由池化机制满足的最大分配大小。超过此阈值的分配尝试将直接从上游内存资源分配。如果 largest_required_pool_block 为 0 或大于实现的限制，则使用该限制。实现可能会选择比该字段更大的值。

## 23.12.3 池资源构造函数和析构函数 [mem.res.pool.ctor]

- synchronized_pool_resource(const pool_options& opts, memory_resource* upstream);
- 1 要求：有效的内存资源地址。
- 2 效果：构造一个池资源对象，当池资源无法从内部数据结构满足内存请求时，从上游获取内存。生成的对象持有 upstream 的拷贝，但不拥有 upstream 所指向的资源。[注：大多数情况下，对 upstream->allocate() 的调用远少于 this->allocate() 的调用 — 结束]。池化机制的行为通过构造函数的 opts 参数进行调整，该构造函数调用了 upstream->allocate()；
- 3 抛出：除非 upstream->allocate() 抛出异常。不确定或在什么情况下，

```cpp
virtual ~synchronized_pool_resource();
virtual ~unsynchronized_pool_resource();
```

- 4 效果：调用 release()

## 23.12.4 池资源成员 [mem.res.pool.mem]

```cpp
void release();
```

- 1 效果：必要时调用 upstream_resource()->deallocate() 以释放所有内存。[注：即使没有对分配的块调用 deallocate，也会通过调用 upstream_resource() 释放。 — 结束]
memory_resource* upstream_resource() = const;
- 2 返回：传递给对象构造函数的 upstream 参数的值。
pool_options options() const;
- 3 返回：控制此资源池行为的选项。

