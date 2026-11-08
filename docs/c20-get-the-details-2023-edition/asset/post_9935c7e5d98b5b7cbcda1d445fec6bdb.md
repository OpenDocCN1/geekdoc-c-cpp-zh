
```cpp
    std::cout << '\n';
}
```

Now, the value of counter is as expected:

![](img/c60a87adb7f61e2e82071d081bbb389a_483_0.png)

The expected result with `std::atomic_ref`

In keeping with `std::atomic`<sup>19</sup>, type `std::atomic_ref` can be specialized and supports specializations for the built-in data types.

## 6.2.1.2 Specializations of `std::atomic_ref` (C++20)

You can specialize `std::atomic_ref` for user-defined types, use partial specializations for pointer types, or full specializations for arithmetic types such as integral or floating-point types.

### 6.2.1.2.1 Primary Template

The primary template `std::atomic_ref` can be instantiated with a `TriviallyCopyable`<sup>20</sup> type T.

```cpp
struct Counters {
    int a;
    int b;
};

Counters counter;
std::atomic_ref<Counters> cnt(counter);
```

### 6.2.1.2.2 Partial Specializations for Pointer Types

The standard provides partial specializations for a pointer type: `std::atomic_ref<T*>`.

- 19. https://en.cppreference.com/w/cpp/atomic/atomic
- 20. https://en.cppreference.com/w/cpp/types/is_trivially_copyable

### 6.2.1.2.3 Specializations for Arithmetic Types

The standard provides specialization for the integral and floating-point types: `std::atomic_ref<arithmetic type>`.

- Character types: `char`, `char8_t` (C++20), `char16_t`, `char32_t`, and `wchar_t`
- Standard signed-integer types: `signed char`, `short`, `int`, `long`, and `long long`
- Standard unsigned-integer types: `unsigned char`, `unsigned short`, `unsigned int`, `unsigned long`, and `unsigned long long`
- Additional integer types, defined in the header `<cstdint>`:
  - `int8_t`, `int16_t`, `int32_t`, and `int64_t` (signed integer with exactly 8, 16, 32, and 64 bits)
  - `uint8_t`, `uint16_t`, `uint32_t`, and `uint64_t` (unsigned integer with exactly 8, 16, 32, and 64 bits)
  - `int_fast8_t`, `int_fast16_t`, `int_fast32_t`, and `int_fast64_t` (fastest signed integer with at least 8, 16, 32, and 64 bits)
  - `uint_fast8_t`, `uint_fast16_t`, `uint_fast32_t`, and `uint_fast64_t` (fastest unsigned integer with at least 8, 16, 32, and 64 bits)
  - `int_least8_t`, `int_least16_t`, `int_least32_t`, and `int_least64_t` (smallest signed integer with at least 8, 16, 32, and 64 bits)
  - `uint_least8_t`, `uint_least16_t`, `uint_least32_t`, and `uint_least64_t` (smallest unsigned integer with at least 8, 16, 32, and 64 bits)
  - `intmax_t` and `uintmax_t` (maximum signed and unsigned integer)
  - `intptr_t` and `uintptr_t` (signed and unsigned integer for holding a pointer)
- Standard floating-point types: `float`, `double`, and `long double`

### 6.2.1.2.4 All Atomic Operations

First, here is the list of all operations on `atomic_ref`.

### All operations on `atomic_ref`

| Function | Description |
|---|---|
| `is_lock_free`<br>`atomic_ref<T>::is_always_lock_free` | Checks if the `atomic_ref` object is lock-free.<br>Checks at compile time if the atomic type is always lock-free. |
| `load`<br>`operator T` | Atomically returns the value of the referenced object.<br>Atomically returns the value of the atomic. Equivalent to `atom.load()`. |
| `store` | Atomically replaces the value of the referenced object with a non-atomic value. |
| `exchange` | Atomically replaces the value of the referenced object with the new value. |
| `compare_exchange_strong` | Atomically compares and eventually exchanges the value of the referenced object. |
| `compare_exchange_weak` |  |
| `fetch_add, +=` | Atomically adds (subtracts) the value to (from) the referenced object. |
| `fetch_sub, -=` |  |
| `fetch_or, \|=` | Atomically performs bitwise (AND, OR, and XOR) operation on the referenced object. |
| `fetch_and, &=` |  |
| `fetch_xor, ^=` |  |
| `++, --` | Increments or decrements (either pre- and post-increment) the referenced object. |
| `notify_one` | Notifies one atomic wait operation. |
| `notify_all` | Notifies all atomic wait operations. |
| `wait` | Blocks until it is notified.<br>Compares itself with the old value to protect against spurious wakeups.<br>If the value is different from the old value, returns. |

The composite assignment operators (`+=`, `-=`, `|=`, `&=`, or `^=`) return the new value; the fetch variations return the old value.

Thanks to the constexpr function `atomic_ref<type>::is_always_lock_free`, you can check for each atomic type if it’s lock-free on all supported hardware that the executable might run on. This check returns only true if it is true for all supported hardware. The check is performed at compile-time and is available since C++17.

Each function supports an additional memory-ordering argument. The default for the memory-ordering argument is `std::memory_order_seq_cst`, but you can also use `std::memory_order_relaxed`, `std::memory_order_consume`, `std::memory_order_acquire`, `std::memory_order_release`, or `std::memory_order_acq_rel`. The `compare_exchange_strong` and `compare_exchange_weak` member functions can be parameterized with two memory orderings, one for the success case, and the other for the failure case. Both calls perform an atomic exchange if equal and an atomic load if not. They return true in the success case, false otherwise. If you only explicitly provide one memory ordering, it is used for both the success and the failure case. Here are the details for [memory ordering](https://en.cppreference.com/w/cpp/atomic/memory_order).

Of course, not all operations are available for all types referenced by `std::atomic_ref`. The table shows the list of all atomic operations, depending on the type referenced by `std::atomic_ref`.

**All atomic operations, depending on the type referenced by `std::atomic_ref`**

| Function | `atomic_ref<T>` | `atomic_ref<float>` | `atomic_ref<T*>` | `atomic_ref<integral>` |
|---|---:|---:|---:|---:|
| `is_lock_free` | yes | yes | yes | yes |
| `load` | yes | yes | yes | yes |
| `operator T` | yes | yes | yes | yes |
| `store` | yes | yes | yes | yes |
| `exchange` | yes | yes | yes | yes |
| `compare_exchange_strong` | yes | yes | yes | yes |
| `compare_exchange_weak` | yes | yes | yes | yes |
| `fetch_add, +=` |  | yes | yes | yes |
| `fetch_sub, -=` |  | yes | yes | yes |
| `fetch_or, \|=` |  |  |  | yes |
| `fetch_and, &=` |  |  |  | yes |
| `fetch_xor, ^=` |  |  |  | yes |
| `++, --` |  |  | yes | yes |
| `notify_one` | yes | yes | yes | yes |
| `notify_all` | yes | yes | yes | yes |
| `wait` | yes | yes | yes | yes |

## 6.2.2 Atomic Smart Pointer

A [`std::shared_ptr`](https://en.cppreference.com/w/cpp/memory/shared_ptr) consists of a control block and its resource. The control block is thread-safe, but access to the resource is not. This means modifying the reference counter is an atomic operation, and you have the guarantee that the resource is deleted exactly once. These are the guarantees `std::shared_ptr` gives you.

- 22. https://en.cppreference.com/w/cpp/atomic/memory_order
- 23. https://en.cppreference.com/w/cpp/memory/shared_ptr

![](img/c60a87adb7f61e2e82071d081bbb389a_487_0.png)

### The Importance of Being Thread Safe

I want to take a short detour to emphasize how important it is that the `std::shared_ptr` has well-defined multithreading semantics. At first glance, using a `std::shared_ptr` does not appear to be a sensible choice for multithreaded code. It is by definition shared and mutable and is the ideal candidate for non-synchronized read and write operations and hence for undefined behavior. On the other hand, there is the guideline in modern C++: **Don't use raw pointers.** This means, consequently, that you should use smart pointers in multithreaded programs.

The proposal N4162<sup>24</sup> for atomic smart pointers directly addresses the deficiencies of the current implementation. The shortcomings boil down to these three points: consistency, correctness, and performance.

- **Consistency**: the atomic operations for `std::shared_ptr` are the only atomic operations for a non-atomic data type.
- **Correctness**: using global atomic operations is quite error-prone because the correct usage is based on discipline. It is easy to forget to use an atomic operation - such as using `ptr = localPtr` instead of `std::atomic_store(&ptr, localPtr)`. The result is undefined behavior because of a data race. If we used an atomic smart pointer instead, the type system would not allow it.
- **Performance**: the atomic smart pointers have a significant advantage compared to non-atomic versions. The atomic versions are designed for the particular use case and can internally have a `std::atomic_flag` as cheap spinlock<sup>25</sup>. Designing the non-atomic versions of the pointer functions to be thread-safe would be overkill when they are used in a single-threaded scenario. They would have a performance penalty.

The correctness argument is probably the most important one. Why? The answer lies in the proposal. The proposal presents a thread-safe singly-linked list that supports insertion, deletion, and searching of elements. This singly-linked list is implemented in a lock-free way.

- 24. https://wg21.link/n4162
- 25. https://en.wikipedia.org/wiki/Spinlock
