# ISO/IEC 14882:2017(E)

|— end example|

Implementations should ensure that value-and-exchange operations do not consistently return
false unless the atomic object has value different from expected or are concurrent
modifications to the atomic object.

Remarks: A weak-and-exchange operation may fail spuriously. That is, even when the
contents of memory referred to by expected and this are equal, it may return false and store
back to the same memory contents that were originally there. [Note: This spurious failure
enables implementation of compare-and-exchange on a broader class of machines, eg., load-linked-
store-conditional machines. A consequence of spurious failure is nearly all cases of weak-
exchange will be in a loop.

When a compare-and-exchange is in a loop, the weak version will yield better performance on
platforms. When a weak compare-and-exchange would require a loop and one would not, the
strong is preferable — end note |

[Note: The memory and order semantics of the compare-and-exchange operations may result in failed
comparisons for values equal if the underlying type has padding bits,
trip bits, or alternate representations of the same value. — end note]

# 32.6. Specializations for integers

[atomics.types.int]

There are specializations for the integral types char, signed char, unsigned
char, short, unsigned short, int, unsigned int, long, unsigned long, long, unsigned long
long, char16, char32, tchar, and any other types defined in the header <concepts>
For each such integral type, the specialization <integral> provides additional atomic
operations to integral types. [Note: For the specialization atomic<bool>, see 32.6. — end note]

```
namespace std {
```

```
struct atomic<integral> {
    using value_type = integral;
    using order_type = value_type;
    static const bool is_lock_free = implementation-defined;
    bool is_lock_free() const noexcept;
    void store(integral value, memory_order order = memory_order_seq_cst) volatile noexcept;
    void store(integral value, memory_order order = memory_order_seq_cst) const noexcept;
    integral load(memory_order order = memory_order_seq_cst) volatile noexcept;
    integral load(memory_order order = memory_order_seq_cst) const noexcept;
    integral load_exchange(integral value, memory_order order = memory_order_seq_cst) volatile noexcept;
    integral load_exchange(integral value, memory_order order = memory_order_seq_cst) const noexcept;
    bool compare_exchange(integral expected, memory_order order = memory_order_seq_cst) volatile noexcept;
    bool compare_exchange(integral expected, memory_order order = memory_order_seq_cst) const noexcept;
    bool compare_and_exchange(integral expected, memory_order order = memory_order_seq_cst) volatile noexcept;
    bool compare_and_exchange(integral expected, memory_order order = memory_order_seq_cst) const noexcept;
    bool compare_and_exchange(integral expected, memory_order order = memory_order_seq_cst) volatile noexcept;
    bool compare_and_exchange(integral expected, memory_order order = memory_order_seq_cst) const noexcept;
    bool compare_exchange_strong(integral expected, memory_order order = memory_order_seq_cst) volatile noexcept;
    bool compare_exchange_strong(integral expected, memory_order order = memory_order_seq_cst) const noexcept;
    bool compare_exchange_weak(integral expected, memory_order order = memory_order_seq_cst) volatile noexcept;
    bool compare_exchange_weak(integral expected, memory_order order = memory_order_seq_cst) const noexcept;
    bool compare_exchange_weak(integral expected, memory_order order = memory_order_seq_cst) volatile noexcept;
    bool compare_exchange_weak(integral expected, memory_order order = memory_order_seq_cst) const noexcept;
};
```

§ 32.6

ISO/IEC 2017 — All rights reserved

1348