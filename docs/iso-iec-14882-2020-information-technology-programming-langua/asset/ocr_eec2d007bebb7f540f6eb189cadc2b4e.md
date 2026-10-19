# 20.12.2 Class memory_resource [mem.res.class]

# 20.12.2.1 General [mem.res.class.general]

1 The memory_resource class is an abstract interface to an unbounded set of classes encapsulating memory resources.

```
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

# 20.12.2.2 Public member functions [mem.res.public]

```
~memory_resource();
```

1 Effects: Destroys this memory_resource.

```
[[nodiscard]] void* allocate(size_t bytes, size_t alignment = max_align);
```

2 Effects: Equivalent to: return do_allocate(bytes, alignment);

```
void deallocate(void* p, size_t bytes, size_t alignment = max_align);
```

3 Effects: Equivalent to do_deallocate(p, bytes, alignment).

```
bool is_equal(const memory_resource& other) const noexcept;
```

4 Effects: Equivalent to: return do_is_equal(other);

# 20.12.2.3 Private virtual member functions [mem.res.private]

```
virtual void* do_allocate(size_t bytes, size_t alignment) = 0;
```

1 Preconditions: alignment is a power of two.

2 Returns: A derived class shall implement this function to return a pointer to allocated storage (6.7.5.5.2) with a size of at least bytes, aligned to the specified alignment.

3 Throws: A derived class implementation shall throw an appropriate exception if it is unable to allocate memory with the requested size and alignment.

```
// 20.12.5, pool resource classes
struct pool_options;
class synchronized_pool_resource;
class unsynchronized_pool_resource;
class monotonic_buffer_resource;
}
```