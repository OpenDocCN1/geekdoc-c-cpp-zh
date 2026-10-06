# ISO/IEC 14882:2017(E)

replaced with implementation-defined defaults, and sizes may be rounded to unspecified granularity.

```
void* allocate(size_t bytes, size_t alignment) override;
```

+   4 Returns: A pointer to allocated storage (6.7.4.2) with a size of at least bytes. The size and alignment of the allocated memory shall meet the requirements for a class derived from memory_resource (23.12).

+   5 Effects: If the pool selected for a block of bytes is unable to satisfy the memory request from its internal data structures, it will call upstream_resource()->allocate() to obtain more memory. If bytes is larger than the largest pool can handle, then memory will be allocated using upstream_resource()->allocate().

+   6 Throws: Not unless upstream_resource()->allocate() throws.

```
void deallocate(void* p, size_t bytes, size_t alignment) override;
```

+   7 Effects: Returns the memory to the pool. If it is unspecified, or under what circumstances, this operation will run in a call to upstream_resource()->deallocate().

+   8 Throws: Nothing.

```
bool unsynchronized_pool_resource::do_is_equal(
const memory_resource* const other) noexcept override;
```

```
bool unsynchronized_pool_resource::do_is_equal(
const memory_resource* const other) noexcept
```

```
9 Returns: this == dynamic_cast<const unsynchronized_pool_resource*>(other).
```

# 23.16 Class monotonic_buffer_resource [mem.monotonic.buffer]

A monotonic_buffer_resource is a special-purpose memory resource intended for very fast memory allocation in situations where memory is used to build a few objects and is released all at once when the memory resource is destroyed. It has the following characteristics:

+   (1.1) A call to deallocate has no effect, the amount of memory consumed increases monotonically until the resource is destroyed.

+   (1.2) The program may the initial buffer (if any) is exhausted, it obtains additional buffers from an upstream resource supplied at construction. Each additional buffer is larger than the previous one, following a geometric progression.

+   (1.4) It is intended for access from one thread of at a time. Specific, calls to allocate and deallocate do not synchronize with one another.

+   (1.5) It frees the allocated memory on destruction, if deallocate has not been called for some of the allocated blocks.

```
class monotonic_buffer_resource : public memory_resource {
memory_resource* upstream_rsrc; // exhaustion only
void* buffer; // exhaustion only
size_t buffer_size; // exhaustion only
```

```
public:
explicit monotonic_buffer_resource(memory_resource* upstream);
monotonic_buffer_resource(size_t initial_size, memory_resource* upstream);
motonic_buffer_resource(void* buffer, size_t buffer_size, memory_resource* upstream);
```