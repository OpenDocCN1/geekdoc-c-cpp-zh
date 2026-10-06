
# ISO/IEC 14882:2017(E)

```cpp
T* operator++(int) volatile noexcept;
T* operator++(int) noexcept;
T* operator--(int) volatile noexcept;
T* operator--(int) noexcept;
T* operator++() volatile noexcept;
T* operator++() noexcept;
T* operator--() noexcept;
T* operator++(ptrdriff_t) volatile noexcept;
T* operator++(ptrdriff_t) noexcept;
T* operator--=(ptrdriff_t) volatile noexcept;
T* operator--=(ptrdriff_t) noexcept;
};
```

+ 1 There is a partial specialization of the atomic class template for pointers. Specializations of this partial specialization are standard-layout structs. Each have a trivial default constructor and a trivial destructor.

+ 2 Descriptions are provided below for members that differ from the primary template.

+ 3 The following operations perform arithmetic. The key, operator, and computation correspondence is:

| Key add | Op addition | Key sub | Computation subtraction |
|---|---|---|---|

```cpp
T* fetch_key(ptrdriff_t operand, memory_order order = memory_order_seq_cst) volatile noexcept;
T* fetch_key(ptrdriff_t operand, memory_order order = memory_order_seq_cst) noexcept;
```

+ 4 Requires: T to be an object, otherwise the program is ill-formed. [Note: Pointer arithmetic on void or pointers is ill-defined. — end note]

+ 5 Effects: Atomic replaces the value pointed to by this with the result of the computation applied to the value pointed to this and the given order. These operations are atomic read-modify-write operations (4.7).

+ 6 Returns: Atomically, the value pointed to by this immediately before the effects.

+ 7 Remarks: The result may be an undefined address, but the operations otherwise have no undefined behavior.

```cpp
T* operator op=(ptrdriff_t operand) volatile noexcept;
T* operator+=(ptrdriff_t operand) noexcept;
```

+ 8 Effects: Equivalent to return fetch_key(operand) op;

# 32.6.4 Member operations to integers and pointers to objects [atomics.type.mem]

```cpp
T operator++(int) volatile noexcept;
T operator++(int) noexcept;

Effects: Equivalent to return fetch_add(1);
```

```cpp
T operator--(int) volatile noexcept;
T operator--(int) noexcept;

Effects: Equivalent to return fetch_sub(1);
```

```cpp
operator++() volatile noexcept;
operator++() noexcept;

+ 1 Effects: Equivalent to a return: fetch_add(1) + 1;

operator--() volatile noexcept;
operator--() noexcept;

+ 2 Effects: Equivalent to a return: fetch_sub(1) - 1;

# 32.7 Non-function functions

A non-member function template whose name matches the pattern atomic_f or the pattern atomic_f_-explicit invokes the function f, with the value of the first parameter as the object expression and the value of the remaining parameters (if any) as the member function call, in order. For an argument of type atomic<T>::value_type is generated when passed to the member function call. If no such member function exists, the program is ill-formed.

```cpp
template<class T>
void atomic_init(atomic<T>* object, atomic<T>::value_type desired) noexcept;
template<class T>
void atomic_init(const atomic<T>* object, typename atomic<T>::value_type desired) noexcept;
```

> Effects: Non-atomic initializes with desired value to objects that have been constructed, even once. [Note: These semantics ensure compatibility with C. — end note][Note: Access from another thread, even via an atomic operation, constitutes a data race. — end note]

# 32.8 Flag type and operations

```cpp
namespace std {
struct atomic_flag {
bool test_set(memory_order order = memory_order_seq_cst) volatile noexcept;
bool test_and_set(memory_order order = memory_order_seq_cst) noexcept;
void clear(memory_order order = memory_order_seq_cst) volatile noexcept;
void clear(memory_order order = memory_order_seq_cst) noexcept;

atomic_flag() = default;
atomic_flag(const atomic_flag&) = delete;
atomic_flag& operator=(const atomic_flag&) = delete;
atomic_flag& operator=(const atomic_flag&) volatile = delete;

bool test_set(volatile atomic_flag*) noexcept;
bool test_and_set(atomic_flag*, memory_order order) noexcept;
bool test_and_set_explicit(volatile atomic_flag*, memory_order order) noexcept;
bool test_and_set_explicit(atomic_flag*, memory_order order) noexcept;
void clear(volatile atomic_flag*, memory_order order) noexcept;
void clear(atomic_flag*, memory_order order) noexcept;
void clear_explicit(volatile atomic_flag*, memory_order order) noexcept;
void clear_explicit(atomic_flag*, memory_order order) noexcept;
};
}
```

+ 1 The atomic_flag type provides the classic test-and-set functionality. It has two states, set and clear.

Operations on an object of type atomic_flag shall be lock-free. [Note: Hence the operations should also be address-free. — end note].

The atomic_flag_INIT is a standard-layout struct. It has a trivial default constructor and a trivial destructor.

The macro ATOMIC_FLAG_INIT shall be defined in a way that it can be used to initialize an object of type atomic_flag to the clear state. The macro can be used in the form:

```cpp
atomic_flag guard = ATOMIC_FLAG_INIT;
```

It is unspecified whether the macro can be used in other initialization contexts. For a static-duration object, initialization shall be specified. Unless initialized with ATOMIC_FLAG_INIT, it is unspecified whether an object has an initial value of set or clear.

```cpp
bool atomic_flag_test_set(volatile atomic_flag*) noexcept;
bool atomic_flag_test_and_set(atomic_flag*, memory_order order) noexcept;
bool atomic_flag_test_and_set_explicit(volatile atomic_flag*, memory_order order) noexcept;
bool atomic_flag_test_and_set_explicit(atomic_flag*, memory_order order) noexcept;
void atomic_flag_clear(volatile atomic_flag*, memory_order order) noexcept;
void atomic_flag_clear(atomic_flag*, memory_order order) noexcept;
void atomic_flag_clear_explicit(volatile atomic_flag*, memory_order order) noexcept;
void atomic_flag_clear_explicit(atomic_flag*, memory_order order) noexcept;
```
*(Note: The OCR for the last code block above was heavily mangled in the source; I have reconstructed it based on the preceding struct definition and standard C++ patterns.)*

+ 5 Effects: Atomic replaces the value pointed to by this with the result of the computation applied to the value pointed to this and the given order. These operations are atomic read-modify-write operations (4.7).

+ 6 Returns: Atomically, the value pointed to by this immediately before the effects.

+ 7 Remarks: The result may be an undefined address, but the operations otherwise have no undefined behavior.

+ 8 Effects: Equivalent to return fetch_key(operand) op;

# 32.9 Fences [atomics.fences]

This section introduces synchronization primitives called fences. Fences can have acquire semantics, release semantics, or both. A fence with acquire semantics is called an acquire fence. A fence with release semantics is called a release fence.

- A release synchronizes with an acquire fence if there exists atomic operations X and Y, both performing on atomic M, that A is sequenced before B, X modifies M, and Y is sequenced before B, and Y reads the value written by X or a value written by any side effect in the hypothetical sequence X if it were a release operation.

- An acquire synchronizes with a release operation B that performs an atomic operation on atomic M if there exists some atomic operation X that is sequenced before B, X modifies M, and B reads the value written by X or any side effect.

- An atomic operation A that is a release operation on atomic M synchronizes with an acquire fence B if there exists some atomic operation on M such that X is sequenced before B and reads the value written by A.

void atomic_thread_fence(memory_order order) noexcept;

5 **Effects:** Depending on the value of order, this operation:

- (5.1) has no effects, if `order == memory_order_relaxed` or `order == memory_order_relaxed`;

- (5.2) is an acquire fence, if `order == memory_order_acquire || order == memory_order_consume`;

- (5.3) is a release fence, if `order == memory_order_release`;

- (5.4) is a sequentially consistent acquire and release fence, if `order == memory_order_acq_cst`;

- (5.5) is both an acquire fence and release fence, if `order == memory_order_seq_cst`.

void atomic_signal_fence(memory_order order) noexcept;

6 **Effects:** Equivalent to `atomic_thread_fence(order)`, except that the resulting ordering constraints are established only between a thread and a signal handler executed in the same thread.

7 [Note: `atomic_signal_fence` can be used to specify the order in which actions performed by the thread become visible to the signal handler. Compiler optimizations and reorderings of loads and stores are inhibited in the same way as `atomic_thread_fence`, but the hardware fence instructions that `atomic_thread_fence` would have inserted are not emitted. -- end note]
