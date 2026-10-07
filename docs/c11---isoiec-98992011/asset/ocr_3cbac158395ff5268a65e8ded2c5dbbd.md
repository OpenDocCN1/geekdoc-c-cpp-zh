if (memcmp(object, expected, sizeof(*object)) == 0)
  mempy(object, &desired, sizeof(*object));
else
  mempy(expected, object, sizeof(*object));

4 A weak compare-and-exchange operation may fail spuriously. That is, when the contents of memory referred to by expected and object are equal, it may return zero and store back the same memory contents that were originally there.

5 NOTE 2 This spurious failure enables implementation of compare-and-exchange on a broader class of machines, e.g. load-locked-store-conditional.

6 EXAMPLE A consequence of spurious failure is that nearly all of weak compare-and-exchange will be in a loop.

```
exp = atomic_load(&cur);
do do
  des = function(exp);
} while (!atomic_compare_exchange_weak(&cur, &exp, des));
```

When a compare-and-exchange is in a loop, the weak version will yield better performance on some platforms. When a weak compare-and-exchange would require a loop and a strong would not, the strong one is preferable.

# Returns

7 The result of the comparison.

# 7.17.7.5 The atomic_fetch and modify generic functions

1 The following operations perform arithmetic and bitwise computations. All of these operations are applicable to an object of any integer type. None of these operations are applicable to atomic_bool. The key, operator, and computation correspondence is:

| key | op | computation |
|---|---|---|
| add | + | addition |
| sub | | subtraction |
| or | | | bitwise inclusive or |
| xor | ^ | bitwise exclusive or |
| and | & | bitwise and |

# Synopsis

```
#include <std.h>
atomic_fetch_key(volatile A *object, M operand)
atomic_fetch_key_explicit(volatile A *object, M operand, memory_order order);
```

# Description

3 Atomically replaces the value pointed to by the result of the computation applied to the value pointed to by and the given operand. Memory is affected