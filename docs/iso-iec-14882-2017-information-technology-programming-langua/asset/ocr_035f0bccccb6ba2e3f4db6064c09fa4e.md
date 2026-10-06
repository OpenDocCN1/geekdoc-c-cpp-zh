# ISO/IEC 14882:2017(E)

```
monotonic_buffer_resource()
    : monotonic_buffer_resource(get_default_resource()) {}
explicit monotonic_buffer_resource(size_t initial_size)
    : monotonic_buffer_resource(initial_size, get_default_resource()) {}
motonic_buffer_resource(void* buffer, size_t size, size_t alignment)
    : monotonic_buffer_resource(buffer, size, get_default_resource()) {}

motonic_buffer_resource(const monotonic_buffer_resource&) = delete;

virtual ~monotonic_buffer_resource();

monotonic_buffer_resource()
operator=(const monotonic_buffer_resource&) = delete;

void release();
memory_resource* upstream_resource() const;

protected:
    void* allocate(size_t bytes, size_t alignment) override;
    void deallocate(void* p, size_t bytes, size_t alignment) override;
```

# 23.12.6.1 monotonic_buffer_resource constructor and destructor [mem.res.monotonic.buffer.ctoror]

```
explicit monotonic_buffer_resource(memory_resource* upstream);
motonic_buffer_resource(size_t initial_size, memory_resource* upstream);
```

+   1 Requires: upstream shall be the address of a valid memory resource. initial_size, if specified, shall be greater than zero.

+   2 Effects: Sets next_buffer_resource->rsrc to upstream and current_buffer to nullptr. If initial_size is
specified, sets next_buffer_size to at least initial_size; otherwise sets next_buffer_size to an
implementation-defined size.

+   3 monotonic_buffer_resource(void* buffer, size_t buffer_size, memory_resource* upstream);
Requires: buffer shall be the address of a valid memory resource. buffer_size shall be no larger
than the number of bytes in buffer.

+   4 Effects: Sets next_buffer_resource->rsrc to upstream, current_buffer to buffer, and next_buffer_size to
buffer_size (by not less than 1), then increases next_buffer_size by an implementation-defined
g factor (which may not be integral).

+   -monotonic_buffer_resource();
5 Effects: Release().

# 23.12.6.2 monotonic_buffer_resource [mem.res.monotonic.buffer.mem]

+   void release();
1 Effects: Calls upstream_rsrc->deallocate() as necessary to release all allocated memory.

+   2 [Note: The memory is released back to upstream_rsrc if some blocks that were allocated from
this have not been deallocated from this.— end note]