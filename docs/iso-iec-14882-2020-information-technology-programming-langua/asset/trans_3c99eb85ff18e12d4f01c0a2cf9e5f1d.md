

# ISO/IEC 14882:2020(E)

```
explicit synchronized_pool_resource(const pool_options& opts)
  : synchronized_pool_resource(opts, get_default_resource()) {}

synchronized_pool_resource(const synchronized_pool_resource&) = delete;
virtual ~synchronized_pool_resource();

synchronized_pool_resource& operator=(const synchronized_pool_resource&) = delete;

void release();
memory_resource* upstream_resource() const;
pool_options options() const;

protected:
void* do_allocate(size_t bytes, size_t alignment) override;
void do_deallocate(void* p, size_t bytes, size_t alignment) override;

bool do_is_equal(const memory_resource& other) const noexcept override;
};
```

```
class unsynchronized_pool_resource : public memory_resource {
public:
  unsynchronized_pool_resource(const pool_options& opts, memory_resource* upstream);

  unsynchronized_pool_resource()
    : unsynchronized_pool_resource(pool_options(), get_default_resource()) {}
  explicit unsynchronized_pool_resource(memory_resource* upstream)
    : unsynchronized_pool_resource(pool_options(), upstream) {}
  explicit unsynchronized_pool_resource(const pool_options& opts)
    : unsynchronized_pool_resource(opts, get_default_resource()) {}

  unsynchronized_pool_resource(const unsynchronized_pool_resource&) = delete;
  virtual ~unsynchronized_pool_resource();

  unsynchronized_pool_resource& operator=(const unsynchronized_pool_resource&) = delete;

  void release();
  memory_resource* upstream_resource() const;
  pool_options options() const;

protected:
  void* do_allocate(size_t bytes, size_t alignment) override;
  void do_deallocate(void* p, size_t bytes, size_t alignment) override;

  bool do_is_equal(const memory_resource& other) const noexcept override;
};
```

# 20.12.5.2 pool_options 数据成员 [mem.res.pool.options]

1 pool_options 的成员组成了一组用于池资源的构造函数选项。每个选项对池资源行为的影响如下所述：

```
size_t max_blocks_per_chunk;
```

2 将一次性从上游内存资源（20.12.6）分配以补充池的最大块数。如果 max_blocks_per_chunk 的值为零或大于实现定义的限制，则改用该限制。实现可以选择使用小于此字段指定的值，并且可以为不同的池使用不同的值。

```
size_t largest_required_pool_block;
```

3 需要使用池化机制满足的最大分配大小。尝试分配大于此阈值的单个块将直接从上游内存资源分配。如果 largest_required_pool_block 为零或大于实现定义的限制，

# 20.12.6 类 `monotonic_buffer_resource`

# 20.12.6.1 通用

`monotonic_buffer_resource` 是一种专用内存资源，旨在在内存用于构建少量对象然后在内存资源对象被销毁时一次性释放的情况下实现非常快的内存分配。它具有以下特性：

- 对 `deallocate` 的调用无效，因此消耗的内存量在资源被销毁之前单调递增。
- 程序可以提供一个初始缓冲区，分配器用它来满足内存请求。
- 当初始缓冲区（如果有）耗尽时，它会从构造时提供的 *上游* 内存资源获取额外的缓冲区。每个额外缓冲区都大于前一个缓冲区，遵循几何级数。
- 它 intended 用于一次由一个控制线程访问。具体来说，对 `allocate` 和 `deallocate` 的调用彼此之间不进行同步。
- 它在销毁时释放已分配的内存，即使某些已分配块未从该资源调用 `deallocate`。

```
namespace std::pmr {
  class monotonic_buffer_resource : public memory_resource {
    memory_resource* upstream_rsrc;     // exposition only
    void* current_buffer;               // exposition only
    size_t next_buffer_size;            // exposition only

  public:
    explicit monotonic_buffer_resource(memory_resource* upstream);
    monotonic_buffer_resource(size_t initial_size, memory_resource* upstream);
    monotonic_buffer_resource(void* buffer, size_t buffer_size, memory_resource* upstream);

    monotonic_buffer_resource()
      : monotonic_buffer_resource(get_default_resource()) {}
    explicit monotonic_buffer_resource(size_t initial_size)
      : monotonic_buffer_resource(initial_size, get_default_resource()) {}
    monotonic_buffer_resource(void* buffer, size_t buffer_size)
      : monotonic_buffer_resource(buffer, buffer_size, get_default_resource()) {}

    monotonic_buffer_resource(const monotonic_buffer_resource&) = delete;

    virtual ~monotonic_buffer_resource();

    monotonic_buffer_resource& operator=(const monotonic_buffer_resource&) = delete;

    void release();
    memory_resource* upstream_resource() const;

  protected:
    void* do_allocate(size_t bytes, size_t alignment) override;
    void do_deallocate(void* p, size_t bytes, size_t alignment) override;

    bool do_is_equal(const memory_resource& other) const noexcept override;
  };
}
```

# 20.12.6.2 构造函数和析构函数

```
explicit monotonic_buffer_resource(memory_resource* upstream);
monotonic_buffer_resource(size_t initial_size, memory_resource* upstream);
```

- **前置条件：** `upstream` 是有效内存资源的地址。`initial_size`，如果指定，则大于零。
- **效果：** 将 `upstream_rsrc` 设置为 `upstream`，并将 `current_buffer` 设置为 `nullptr`。如果指定了 `initial_size`，则将 `next_buffer_size` 设置为至少为 `initial_size`；否则将 `next_buffer_size` 设置为实现定义的大小。

```
monotonic_buffer_resource(void* buffer, size_t buffer_size, memory_resource* upstream);
```

前置条件：upstream 是有效内存资源的地址。buffer_size 不大于 buffer 中的字节数。

效果：将 upstream_rsrc 设置为 upstream，current_buffer 设置为 buffer，并将 next_buffer_size 设置为 buffer_size（但不小于 1），然后按实现定义的增长因子增加 next_buffer_size（该因子不必是整数）。

```
~monotonic_buffer_resource();
```

效果：调用 release()。

# 20.12.6.3 成员 [mem.res.monotonic.buffer.mem]

```
void release();
```

效果：根据需要调用 upstream_rsrc->deallocate() 以释放所有已分配的内存。

[注意 1：即使某些从该资源分配的块尚未从该资源释放，内存也会被释放回 upstream_rsrc。——注意结束]

```
memory_resource* upstream_resource() const;
```

返回：upstream_rsrc 的值。

```
void* do_allocate(size_t bytes, size_t alignment) override;
```

返回：指向已分配存储（6.7.5.5.2）的指针，其大小至少为 bytes。已分配内存的大小和对齐方式应满足派生自 memory_resource 的类的要求（20.12.2）。

效果：如果 current_buffer 中的未使用空间可以容纳具有指定 bytes 和 alignment 的块，则从 current_buffer 分配返回块；否则将 current_buffer 设置为 upstream_rsrc->allocate(n, m)，其中 n 不小于 max(bytes, next_buffer_size)，m 不小于 alignment，并按实现定义的增长因子增加 next_buffer_size（该因子不必是整数），然后从新分配的 current_buffer 中分配返回块。

抛出：除非 upstream_rsrc->allocate() 抛出，否则不抛出。

```
void do_deallocate(void* p, size_t bytes, size_t alignment) override;
```

效果：无。

抛出：无。

说明：此资源使用的内存在销毁之前单调递增。

```
bool do_is_equal(const memory_resource& other) const noexcept override;
```

返回：this == &other。

# 20.13 类模板 scoped_allocator_adaptor [allocator.adaptor]

# 20.13.1 头文件 <scoped_allocator> 概要 [allocator.adaptor.syn]

```
namespace std {
    // class template scoped allocator adaptor
    template<class OuterAlloc, class... InnerAlloc>
    class scoped_allocator_adaptor;

    // 20.13.5, scoped allocator operators
    template<class OuterA1, class OuterA2, class... InnerAllocs>
    bool operator==(const scoped_allocator_adaptor<OuterA1, InnerAllocs...>& a,
                    const scoped_allocator_adaptor<OuterA2, InnerAllocs...>& b) noexcept;
}
```

类模板 scoped_allocator_adaptor 是一个分配器模板，它指定一个分配器资源（外部分配器）供容器使用（如同其他分配器一样），并且还指定一个内部分配器资源传递给容器中每个元素的构造函数。此适配器使用一个外部和零个或多个内部分配器类型实例化。如果仅使用一种分配器类型实例化，则内部分配器变为 scoped_allocator_adaptor 本身，从而为容器及其内部的每个元素使用相同的分配器资源，如果元素本身是容器，则递归地为其每个元素使用。如果使用多个分配器，则第一个分配器是外部分配器，用于

