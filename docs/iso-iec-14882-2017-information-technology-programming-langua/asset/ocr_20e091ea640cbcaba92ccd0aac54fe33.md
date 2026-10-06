# ISO/IEC 14882:2017(E)

Operations on an object of type atomic_flag shall be lock-free. [Note: Hence the operations should also be address-free. — end note].

The atomic_flag_INIT is a standard-layout struct. It has a trivial default constructor and a trivial destructor.

The macro ATOMIC_FLAG_INIT shall be defined in a way that it can be used to initialize an object of type atomic_flag to the clear state. The macro can be used in the form:

```
atomic_flag guard = ATOMIC_FLAG_INIT;
```

It is unspecified whether the macro can be used in other initialization contexts. For a static-duration object, initialization shall be specified. Unless initialized with ATOMIC_FLAG_INIT, it is unspecified whether an object has an initial value of set or clear.

```
bool atomic_flag_test_and_set(atomic_flag object) noexcept;
bool atomic_flag_test_and_set(volatile atomic_flag object, memory_order order) noexcept;
bool atomic_flag_test_and_set_explicit(volatile atomic_flag object, memory_order order) noexcept;
bool atomic_flag::test_and_set(memory_order order = memory_order_seq_cst) volatile noexcept;
bool atomic_flag::test_and_set(memory_order order = memory_order_seq_cst) noexcept;
```

+   5 Effects: Sets the value pointed to by object or by this true. Memory is affected according to the value of order. These operations are atomic-modify-write operations (4).

+   6 Returns: The value of the object immediately before the fence. 

```
void atomic_flag_clear(atomic atomic_flag object) noexcept;
void atomic_flag_clear(volatile atomic_flag object) noexcept;
void atomic_flag_clear_explicit(volatile atomic_flag object, memory_order order) noexcept;
void atomic_flag::clear(memory_order order = memory_order_seq_cst) volatile noexcept;
void atomic_flag::clear(memory_order order = memory_order_seq_cst) noexcept;
```

+   7 Requires: The order specified shall not be memory_order_consume, memory_order_acquire, nor memory_order_acrl.

+   8 Effects: Sets the value pointed to by object or by this to false. Memory is affected according to the value of order.

# 32.9 Fences [atomics.fences]

This section introduces synchronization primitives called fences. Fences can have acquire semantics, release semantics, or both. A fence with acquire semantics is called an acquire fence. A fence with release semantics is called a release fence.

+   A release synchronizes with an acquire fence B if there exists atomic operations X and Y, both performing on atomic object M, that A is sequenced before B, X modifies M, and Y is sequenced before B, and Y reads the value written by X or a value written by any side effect in the hypothetical sequence X if it were a release operation.

+   An acquire synchronizes with a release operation B that performs an atomic operation on atomic object M if there exists some atomic operation X that is sequenced before B, X modifies M, and B reads the value written by X or a value written by any side effect in the hypothetical release sequence X if it were a release operation.

+   An atomic operation A that is a release operation on atomic object M synchronizes with an acquire fence B if there exists some atomic operation on M such that X is sequenced before B and reads the value written by A or a value written by any side effect in the release sequence headed by A.