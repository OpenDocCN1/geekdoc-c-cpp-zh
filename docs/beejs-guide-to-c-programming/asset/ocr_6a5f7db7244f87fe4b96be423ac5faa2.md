# Chapter 40. Atoms

The spec is a vague, in my read, about the memory order when it comes to acquiring or releasing atomic variables in the signal handler. C++ says, and it makes sense, that accesses are unsequenced with respect to the rest of the program. The signal can be raised, after all, at any time. I'm assuming C's behavior is similar.

# 40.10 Atomic Flags

There's only one type the standard guarantees be a lock-free: atomic_flag. This is an opaque type for test-and-set operations.

It can be either set or clear. You can initialize it to clear:

```
atomic_flag f = ATOMIC_INIT;
```

You can set the flag atomically with atomic_flag_test_and_set(), which will set the flag and return its previous status as a Bool (true for set).

You can clear the flag atomically with atomic_flag_clear().

Here's an example where we init the flag, set it twice, then clear it again.

```
#include <stdio.h>
#include <stdbool.h>
#include <atomic.h>

atomic_flag f = ATOMIC_INIT;

int main(void) {
    bool r = atomic_flag_test_and_set(&f);
    printf("Value: %d\n", r); // 0

    r = atomic_flag_test_and_set(&f);
    printf("Value: %d\n", r); // 1

    atomic_flag_clear(&f);
    r = atomic_flag_test_and_set(&f);
    printf("Value: %d\n", r); // 0
}
```

# 40.11 Atomic structs and unions

Using the _Atomic qualifier or specifier, you can make atomic structs or unions! Pretty astounding.,

If there's not a lot of data in there (a handful of bytes), the resulting atomic type may be lock-free. Test it with atomic_is_lock_free().

```
#include <stdio.h>
#include <atomic.h>

int main(void) {
    struct point {
        float x, y;
    }
```

> C++ elaborates that if the signal is the result of a call to raise(), it is sequenced after the raise().

> https://en.wikipedia.org/wiki/Test-and-set