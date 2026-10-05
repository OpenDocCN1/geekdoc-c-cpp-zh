
- is an acquire fence, if order == memory_order_acquire or order == memory_order_consume;

- is a release fence, if order == memory_order_release;

- is both an acquire fence and a release fence, if order == memory_order_acq_rel;

- is a sequentially consistent acquire and release fence, if order == memory_order_seq_cst.

# Returns

The atomic_thread_fence function returns no value.

## 7.17.4.2 The atomic_signal_fence function

# Synopsis

```
#include <atomic>
void atomic_signal_fence(memory_order order);
```

# Description

Equivalent to atomic_thread_fence(order), except the resulting ordering constraints are established only between a thread and a signal handler executed in the same thread.

NOTE 1 The atomic_signal_fence function can be used to specify in which actions performed by the thread become visible to the signal handler.

NOTE 2 Compiler optimizations and reorderings of loads and stores are inhibited in the same way as atomic_thread_fence, but the hardware fence instructions that atomic_thread_fence would have inserted are not emitted.

# Returns

The atomic_signal_fence function returns no value.

## 7.17.5 Lock-free property

The atomic-free macros indicate the lock-free property of integer and address atomic types. A value of 0 indicates that the type is never lock-free; a value of 1 indicates that the type is sometimes lock-free; a value of 2 indicates that the type is always lock-free.

NOTE Operations that are lock-free also be address-free. That is, atomic operations on the same memory location via two different addresses will communicate atomically. The implementation should not depend on any per-process state. This restriction enables communication via memory mapped into a process more than once and memory shared between two processes.

### 7.17.5.1 The atomic_is_lock_free generic function

# Synopsis

```
#include <atomic.h>
Bool atomic_is_lock_free(const volatile A *obj);
```

Description

The atomic_is_lock_free generic function indicates whether or not the object pointed to by obj is lock-free.

#Returns

The atomic_is_lock_free generic function returns nonzero (true) if and only if the object's operations are lock-free. The result of a lock-free query on one object cannot be inferred from the result of a lock-free query on another object.

## 7.17.6 Atomic integer types

For each line in the following table,257) the atomic type name is declared as a type that has the same representation and alignment requirements as the corresponding direct type.258)

> 257) See “future library directions” (7.31.8).

> 258) The same representation and alignment requirements are meant to imply interchangeability as arguments to functions, return values from functions, and members of unions.

| Atomic type name | Direct type |
| --- | --- |
| atomic_bool | _Atomic_Bool |
| atomic_char | _Atomic char |
| atomic_schar | _Atomic signed char |
| atomic_uchar | _Atomic unsigned char |
| atomic_short | _Atomic short |
| atomic_ushort | _Atomic unsigned short |
| atomic_int | _Atomic int |
| atomic_uint | _Atomic unsigned int |
| atomic_long | _Atomic long |
| atomic_ulong | _Atomic unsigned long |
| atomic_llong | _Atomic long long |
| atomic_ullong | _Atomic unsigned long long |
| atomic_char16_t | _Atomic char16_t |
| atomic_char32_t | _Atomic char32_t |
| atomic_wchar_t | _Atomic wchar_t |
| atomic_int_least8_t | _Atomic int_least8_t |
| atomic_uint_least8_t | _Atomic uint_least8_t |
| atomic_int_least16_t | _Atomic int_least16_t |
| atomic_uint_least16_t | _Atomic uint_least16_t |
| atomic_int_least32_t | _Atomic int_least32_t |
| atomic_uint_least32_t | _Atomic uint_least32_t |
| atomic_int_least64_t | _Atomic int_least64_t |
| atomic_uint_least64_t | _Atomic uint_least64_t |
| atomic_int_fast8_t | _Atomic int_fast8_t |
| atomic_uint_fast8_t | _Atomic uint_fast8_t |
| atomic_int_fast16_t | _Atomic int_fast16_t |
| atomic_uint_fast16_t | _Atomic uint_fast16_t |
| atomic_int_fast32_t | _Atomic int_fast32_t |
| atomic_uint_fast32_t | _Atomic uint_fast32_t |
| atomic_int_fast64_t | _Atomic int_fast64_t |
| atomic_uint_fast64_t | _Atomic uint_fast64_t |
| atomic_intptr_t | _Atomic intptr_t |
| atomic_uintptr_t | _Atomic uintptr_t |
| atomic_size_t | _Atomic size_t |
| atomic_ptrdiff_t | _Atomic ptdiff_t |
| atomic_intmax_t | _Atomic intmax_t |
| atomic_uintmax_t | _Atomic uintmax_t |

The semantics of the operations on these types are defined in 7.17.7.

NOTE The representation of atomic integers need not have the same size as their corresponding regular types. They should have the same size whenever possible, as it eases effort required to port existing code.

## 7.17.7 Operations on atomic types

There are only a few kinds of operations on atomic types, though there are instances of those kinds. This subclause specifies each general kind.

### 7.17.7.1 The atomic_store generic functions

# Synopsis

```
#include <atomic.h>
void atomic_store(volatile A *object, C desired);
void atomic_store_explicit(volatile A *object,
  C desired, memory_order_order);
```

Description

The order argument shall not be memory_order_acquire, memory_order_consume, nor memory_order_acq_rel. Atomically replace the value pointed by object with the value of desired. Memory is affected according to the value of order.

# Returns

The atomic_store generic functions return no value.

### 7.17.7.2 The atomic_load generic functions

# Synopsis

```
#include <atomic.h>
C atomic_load(volatile A *object);
C atomic_load_explicit(volatile A *object,
  memory_order_order);
```

Description

The order argument shall not be memory_order_release nor memory_order_acq_rel. Memory is affected according to the value of order.

# Returns

Atomically returns the value pointed to by object.

### 7.17.7.3 The atomic_exchange generic functions

# Synopsis

```
#include <atomic.h>
C atomic_exchange(volatile A *object, C desired);
C atomic_exchange_explicit(volatile A *object,
C desired, memory_order);
```

Description

Atomically replaces the value pointed to by object with desired. Memory is affected according to the value of order. These operations are atomic-modify-write (5.1.4).

# Returns

Atomically returns the value pointed to by object before the exchange.

## 7.17.7.4 The atomic_compare_exchange generic functions

# Synopsis

```
#include <atomic.h>
Bool atomic_compare_exchange_strong(volatile A *object, C desired);
Bool atomic_compare_exchange_explicit(volatile A *object,
C desired, memory_order order);
Bool atomic_compare_exchange_weak(volatile A *object, C desired);
Bool atomic_compare_exchange_weak_explicit(volatile A *object,
C desired, memory_order order);
```

Description

The order argument shall not be memory_order_acquire, memory_order_consume, nor memory_order_acq_rel. The failure argument shall be no stronger than the success argument. Atomically, compares the value pointed to object for equality with that in expected, and if true, replaces the value pointed by object with desired, and if false, updates expected with the value in object. These operations are atomic-modify-write (5.24).

NOTE 1 For example, the effect of atomic_compare_exchange_strong is

```
if (memcmp(object, expected, sizeof(*object)) == 0)
    memcmp(object, &desired, sizeof(*object));
else
    memcmp(expected, object, sizeof(*object));
```

A weak compare-and-exchange operation may fail spuriously; that is, even when contents of memory referred by expected and object are equal, it may return zero and store back to expected the same contents that were there.

NOTE 2 This spurious failure enables implementation of compare-and-exchange on a broader class of objects, e.g. load-store-conditional machines.

EXAMPLE A consequence of spurious failure is nearly all uses of weak compare-and-exchange will be in a loop.

```
exp = atomic_load(&cur);
do {
    des = function(exp);
} while (!atomic_compare_exchange_weak(&cur, &exp, &des));
```

When a compare-and-exchange is in a loop, the weak version will yield better performance on some platforms. When a weak compare-and-exchange would require a loop and a strong one would not, the strong one is preferable.

# Returns

The result of the comparison.

### 7.17.7.5 The atomic_fetch and modify generic functions

The following operations perform arithmetic and bitwise computations. All of these operations are applicable to an object of any atomic integer type. None of these operations are applicable to **atomic_bool**. The key, operator, and computation correspondence is:

| key | op | computation |
| --- | --- | --- |
| add | + | addition |
| sub | - | subtraction |
| or | | | bitwise inclusive or |
| xor | ^ | bitwise exclusive or |
| and | & | bitwise and |

# Synopsis

```
#include <atomic.h>
atomic_fetch_key(volatile A *object, M operand);
atomic_fetch_key_explicit(volatile A *object, M operand, memory_order order);
```

Description

Atomically replaces the value pointed to by **object** with the result of the computation applied to the value pointed to by **object** and the given operand. Memory is affected
