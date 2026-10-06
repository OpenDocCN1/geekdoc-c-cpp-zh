
# ISO/IEC 14882:2017(E)

```cpp
using atomic_uint_fast16_t = atomic<uint_fast16_t>;
using atomic_int_fast32_t = atomic<int_fast32_t>;
using atomic_uint_fast32_t = atomic<uint_fast32_t>;
using atomic_int_fast64_t = atomic<int_fast64_t>;
using atomic_uint_fast64_t = atomic<uint_fast64_t>;

using atomic_uintptr_t = atomic<uintptr_t>;
using atomic_intptr_t = atomic<intptr_t>;
using atomic_size_t = atomic<size_t>;
using atomic_generic_t = atomic<generic_t>;
using atomic_intmax_t = atomic<intmax_t>;
using atomic_uintmax_t = atomic<uintmax_t>;
```

```cpp
// 32.8. flag type and operations
struct atomic_flag;
bool atomic_flag_test_and_set(volatile atomic_flag*) noexcept;
bool atomic_flag_test_and_set(atomic_flag*) noexcept;
bool atomic_flag_test_and_set_explicit(atomic_flag*, memory_order) noexcept;
void atomic_flag_clear(volatile atomic_flag*) noexcept;
void atomic_flag_clear(atomic_flag*) noexcept;
void atomic_flag_clear_explicit(atomic_flag*, memory_order) noexcept;
# ATOMIC_FLAG_INIT //define ATOMIC_FLAG_INIT see below
```

```cpp
// 32.9. fences
extern "C" void atomic_thread_fence(memory_order) noexcept;
extern "C" void atomic_signal_fence(memory_order) noexcept;
```

## 32.3 Type aliases [atomic.alias]

- 1 The type aliases atomic_intN_t, atomic_uintN_t, atomic_intptr_t, and atomic_uintptr_t are defined if and only if int_fastN_t, uint_fastN_t, intptr_t, and uintptr_t are defined, respectively.

## 32.4 Order and consistency [atomic.order]

```cpp
namespace std {
 memory_order {
 memory_order_relaxed, memory_order_acquire, memory_order_consume, memory_order_release, memory_order_acq_rel, memory_order_seq_cst
 };
}
```

- 1 The enumeration memory_order specifies the detailed (non-atomic) memory synchronization order as defined in 4.7 and may provide for operation ordering. Its enumerated values and their meanings are as follows:

- (1.1) memory_order_relaxed: no operation orders memory.

- (1.2) memory_order_release, memory_order_acq_rel and memory_order_seq_cst: a store operation performs a release on the affected memory location.

- (1.3) memory_order_consume: a load operation performs a consume on the affected memory location. [Note: Prefer memory_order_acquire, which provides stronger guarantees than memory_order_consume. Implementations have found it infeasible to perform better than that of memory_order_acquire. Specification revisions are under consideration. —end note]

- (1.4) memory_order_acquire, memory_order_acq_rel, and memory_order_seq_cst: a load operation performs an acquire operation on the affected memory location.

> [Note: Atomic operations specifying memory_order_relaxed are relaxed with respect to memory ordering. Implementations must guarantee that any atomic access to a particular atomic object is invisible with respect to all other atomic accesses to that object.—end note]

- 2 An atomic operation A performs a release operation on an atomic object M synchronizes with an atomic operation B that performs an acquire operation on M and takes its value from any side sequenced by A.

- 3 There shall be a single order S on all memory_order_seq_cst operations, consistent with the “happens before” order and modification orders for all affected locations, such that each memory_order_seq_cst operation B loads a value from an atomic object M one of the following:

- (3.1) the result of the last modification of M that precedes B in S, if it exists,

- (3.2) if A exists, the result of modification of M that is not memory_order_seq_cst and does not happen before A, or

- (3.3) if A does not exist, the result of modification of M that is memory_order_seq_cst.

> [Note: It is not required that S includes lock, it can always be extended to an order order, unless the ordering between those is already included in the “happens before” order.—end note]

- 4 For an atomic operation B reads the value of an atomic object M, if there is a memory_order_seq_cst fence X sequenced before B, then B observes the memory_order_seq_cst modification of M preceding X in S or a later modification of M in its modification order.

- 5 For atomic operations A and B on an atomic object M, where A modifies and B takes its value, if there are a memory_order_seq_cst fence X that A is sequenced before X and B follows X in S, then B observes either the effects of A or a later modification of M in its modification order.

- (7.1) the result of the last modification of M that precedes B in S, if it exists,

- (7.2) if A exists, the result of modification of M that is not memory_order_seq_cst and does not happen before A, or

- (7.3) if A does not exist, the result of modification of M that is memory_order_seq_cst.

> [Note: Atomic operations specifying memory_order_relaxed are relaxed with respect to memory ordering. Implementations must guarantee that any atomic access to a particular atomic object is invisible with respect to all other atomic accesses to that object.—end note]

- 8 For an atomic operation B reads the value of an atomic object M, if there is a memory_order_seq_cst fence X sequenced before B, then B observes the memory_order_seq_cst modification of M preceding X in S or a later modification of M in its modification order.

- 9 For atomic operations A and B on an atomic object M, where A modifies and B takes its value, if there are a memory_order_seq_cst fence X that A is sequenced before X and B follows X in S, then B observes either the effects of A or a later modification of M in its modification order.

- 10 Atomic-modify-write operations should always read the last value (in the modification order) before the write is associated with the read-write operation.

- 11 Implementations should allow atomic stores to atomic locations within a reasonable amount of time.

- 12 Returns:

## 32.5 Lock-free property

```cpp
#define ATOMIC_BOOL_LOCK_FREE undefined
#define ATOMIC_CHAR_LOCK_FREE undefined
#define ATOMIC_CHAR16_LOCK_FREE undefined
#define ATOMIC_SHORT_LOCK_FREE undefined
#define ATOMIC_CHAR32_LOCK_FREE undefined
#define ATOMIC_WCHAR_T_LOCK_FREE undefined
#define ATOMIC_SHORT_INT_LOCK_FREE undefined
#define ATOMIC_LONG_LOCK_FREE undefined
#define ATOMIC_LONG_LOCK_FREE undefined
#define ATOMIC_POINTER_LOCK_FREE undefined
```

- 1 The ATOMIC ... _LOCK_FREE macros indicate the lock-free property of corresponding types, with the signed and unsigned values. The properties also apply to (partial) specializations of the atomic. A value of 0 indicates that the types are not lock-free. A value of 2 indicates that the types are always lock-free.

- 2 The function atomic_is_lock_free (3.2.6) indicates whether the object is lock-free. In any program execution, the result of the lock-free query shall be consistent for all pointers of the type.

- 3 Atomic operations that are not lock-free should be considered to potentially block (4.7.2).
