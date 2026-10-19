

```cpp
template<class Y>
    weak_ptr(const weak_ptr<Y>& r) noexcept;
weak_ptr(weak_ptr&& r) noexcept;
template<class Y>
    weak_ptr(weak_ptr<Y>&& r) noexcept;

// 20.11.4.3, destructor
~weak_ptr();

// 20.11.4.4, assignment
weak_ptr& operator=(const weak_ptr& r) noexcept;
template<class Y>
    weak_ptr& operator=(const weak_ptr<Y>& r) noexcept;
template<class Y>
    weak_ptr& operator=(const shared_ptr<Y>& r) noexcept;
weak_ptr& operator=(weak_ptr&& r) noexcept;
template<class Y>
    weak_ptr& operator=(weak_ptr<Y>&& r) noexcept;

// 20.11.4.5, modifiers
void swap(weak_ptr& r) noexcept;
void reset() noexcept;

// 20.11.4.6, observers
long use_count() const noexcept;
bool expired() const noexcept;
shared_ptr<T> lock() const noexcept;
template<class U>
    bool owner_before(const shared_ptr<U>& b) const noexcept;
template<class U>
    bool owner_before(const weak_ptr<U>& b) const noexcept;
};

template<class T>
    weak_ptr(shared_ptr<T>) -> weak_ptr<T>;

// 20.11.4.7, specialized algorithms
template<class T>
    void swap(weak_ptr<T>& a, weak_ptr<T>& b) noexcept;
}
```

2 `weak_ptr` 的特化应为 Cpp17CopyConstructible 和 Cpp17CopyAssignable，以便在标准容器中使用。`weak_ptr` 的模板参数 T 可以是不完全类型。

## 20.11.4.2 构造函数 [util.smartptr.weak.const]

```cpp
constexpr weak_ptr() noexcept;
```

1 效果：构造一个空的 `weak_ptr` 对象。

2 后置条件：`use_count() == 0`。

```cpp
weak_ptr(const weak_ptr& r) noexcept;
template<class Y> weak_ptr(const weak_ptr<Y>& r) noexcept;
template<class Y> weak_ptr(const shared_ptr<Y>& r) noexcept;
```

3 约束：对于第二个和第三个构造函数，`Y*` 与 `T*` 兼容。

4 效果：如果 `r` 为空，则构造一个空的 `weak_ptr` 对象；否则，构造一个与 `r` 共享所有权的 `weak_ptr` 对象并存储 `r` 中存储的指针的副本。

5 后置条件：`use_count() == r.use_count()`。

```cpp
weak_ptr(weak_ptr&& r) noexcept;
template<class Y> weak_ptr(weak_ptr<Y>&& r) noexcept;
```

6 约束：对于第二个构造函数，`Y*` 与 `T*` 兼容。

7 效果：从 `r` 移动构造一个 `weak_ptr` 实例。

```cpp
public:
    shared_ptr<T> shared_from_this();
    shared_ptr<T const> shared_from_this() const;
    weak_ptr<T> weak_from_this() noexcept;
    weak_ptr<T const> weak_from_this() const noexcept;

private:
    mutable weak_ptr<T> weak_this;  // exposition only
};
}
```

3 `enable_shared_from_this` 的模板参数 T 可以是不完全类型。

```cpp
constexpr enable_shared_from_this() noexcept;
enable_shared_from_this(const enable_shared_from_this<T>&) noexcept;
```

4 效果：值初始化 `weak_this`。

```cpp
enable_shared_from_this<T>& operator=(const enable_shared_from_this<T>&) noexcept;
```

5 返回：`*this`。

6 [注 1：`weak_this` 不会被更改。——注结束]

```cpp
shared_ptr<T>     shared_from_this();
shared_ptr<T const> shared_from_this() const;
```

7 返回：`shared_ptr<T>(weak_this)`。

```cpp
weak_ptr<T>     weak_from_this() noexcept;
weak_ptr<T const> weak_from_this() const noexcept;
```

8 返回：`weak_this`。

## 20.11.7 智能指针哈希支持 [util.smartptr.hash]

```cpp
template<class T, class D> struct hash<unique_ptr<T, D>>;
```

1 令 `UP` 为 `unique_ptr<T,D>`，特化 `hash<UP>` 在 `hash<typename UP::pointer>` 被启用时才启用（20.14.19）。启用时，对于类型为 `UP` 的对象 `p`，`hash<UP>()(p)` 的求值结果与 `hash<typename UP::pointer>()(p.get())` 相同。成员函数不保证为 `noexcept`。

```cpp
template<class T> struct hash<shared_ptr<T>>;
```

2 对于类型为 `shared_ptr<T>` 的对象 `p`，`hash<shared_ptr<T>>()(p)` 的求值结果与 `hash<typename shared_ptr<T>::element_type*>()(p.get())` 相同。

## 20.12 内存资源 [mem.res]

### 20.12.1 头文件 `<memory_resource>` 概要 [mem.res.syn]

```cpp
namespace std::pmr {
    // 20.12.2, class memory_resource
    class memory_resource;

    bool operator==(const memory_resource& a, const memory_resource& b) noexcept;

    // 20.12.3, class template polymorphic_allocator
    template<class Tp = byte> class polymorphic_allocator;

    template<class T1, class T2>
        bool operator==(const polymorphic_allocator<T1>& a,
                        const polymorphic_allocator<T2>& b) noexcept;

    // 20.12.4, global memory resources
    memory_resource* new_delete_resource() noexcept;
    memory_resource* null_memory_resource() noexcept;
    memory_resource* set_default_resource(memory_resource* r) noexcept;
    memory_resource* get_default_resource() noexcept;

    // 20.12.5, pool resource classes
    struct pool_options;
    class synchronized_pool_resource;
    class unsynchronized_pool_resource;
    class monotonic_buffer_resource;
}
```

### 20.12.2 类 memory_resource [mem.res.class]

#### 20.12.2.1 通用 [mem.res.class.general]

1 `memory_resource` 类是对封装内存资源的无界集合的抽象接口。

```cpp
namespace std::pmr {
class memory_resource {
  static constexpr size_t max_align = alignof(max_align_t);  // exposition only

public:
  memory_resource() = default;
  memory_resource(const memory_resource&) = default;
  virtual ~memory_resource();

  memory_resource& operator=(const memory_resource&) = default;

  [[nodiscard]] void* allocate(size_t bytes, size_t alignment = max_align);
  void deallocate(void* p, size_t bytes, size_t alignment = max_align);

  bool is_equal(const memory_resource& other) const noexcept;

private:
  virtual void* do_allocate(size_t bytes, size_t alignment) = 0;
  virtual void do_deallocate(void* p, size_t bytes, size_t alignment) = 0;

  virtual bool do_is_equal(const memory_resource& other) const noexcept = 0;
};
}
```

#### 20.12.2.2 公有成员函数 [mem.res.public]

```cpp
~memory_resource();
```

1 效果：销毁此 `memory_resource`。

```cpp
[[nodiscard]] void* allocate(size_t bytes, size_t alignment = max_align);
```

2 效果：等价于：`return do_allocate(bytes, alignment);`

```cpp
void deallocate(void* p, size_t bytes, size_t alignment = max_align);
```

3 效果：等价于 `do_deallocate(p, bytes, alignment)`。

```cpp
bool is_equal(const memory_resource& other) const noexcept;
```

4 效果：等价于：`return do_is_equal(other);`

#### 20.12.2.3 私有虚成员函数 [mem.res.private]

```cpp
virtual void* do_allocate(size_t bytes, size_t alignment) = 0;
```

1 前置条件：`alignment` 为 2 的幂。

2 返回：派生类应实现此函数以返回指向分配存储的指针（6.7.5.5.2），其大小至少为 `bytes`，对齐到指定的 `alignment`。

3 抛出：派生类实现如果无法以请求的<|message|>
