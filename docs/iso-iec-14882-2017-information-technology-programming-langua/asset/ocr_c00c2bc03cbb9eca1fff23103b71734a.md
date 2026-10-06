# ISO/IEC 14882:2017(E)

memory_resource* null_memory_resource() noexcept;

Returns: A pointer to a static-duration object of a type derived from memory_resource for which allocate() throws bad_alloc and which deallocate() has no effect. The same value is returned every time this function is called. For a return value p and a memory resource r, p->is_equal(r) returns r == p.

3 The default memory resource pointer is a pointer to a memory resource that is used by certain facilities when an explicit memory resource is not supplied through the interface. Its initial value is the return value of new_delete_resource().

memory_resource* set_delete_resource(memory_resource* r) noexcept;

4 Effects: If r is non-null, the value of the default memory resource pointer to r, otherwise sets the default memory resource pointer to new_delete_resource().

5 Postconditions: get_delete_resource() == r.

6 Returns: The return value of the default memory resource pointer.

7 Remarks: Calling the set_delete_resource and get_delete_resource functions shall not incur a data race. A call to the set_delete_resource function shall synchronize with subsequent calls to the set_delete_resource and get_delete_resource functions.

memory_resource* get_delete_resource() noexcept;

8 Returns: The current value of the default memory resource pointer.

# 23.12.5 Pool resource classes

# 23.12.1 synchronized_pool_resource and unsynchronized_pool_resource [mem.res_pool.overview]

+   1 The synchronized_pool_resource and unsynchronized_pool_resource classes (collectively pool resource classes) are general-purpose memory resources having the following:

+   - Each resource frees its allocated memory on destruction, if deallocate has not been called for some of the blocks.

+   - A pool resource consists of pools, serving for different block sizes. Each individual pool manages a collection of chunks that are divided into blocks of uniform size, returned via calls to allocate(). Each call to allocate(size, alignment) is dispatched to the pool serving accommodating at least block sizes.

+   - When a pool is exhausted, allocating a block from the pool results in the allocation of an additional chunk from the upstream allocator (supplied at construction), replenishing the pool. With each successful replenishment, the chunk size increases geometrically. [Note: By allocating in chunks, the pooling strategy increases the chance that consecutive allocations will be closer in size and not wasted].

+   - Allocation requests exceeding the largest block size of any pool are fully satisfied directly from the upstream allocator.

+   - A_options struct may be passed to the pool resource constructors to tune the largest block size and the maximum chunk size.

2 A synchronized_pool_resource may be accessed from multiple threads without external synchronization and may have thread-safe pools to reduce synchronization costs. An unsynchronized_pool_resource class may not be accessed from multiple threads simultaneously and thus avoids the cost of synchronization entirely in single-threaded applications.

§ 23.12.5.1

© ISO/IEC 2017 - All rights reserved

640