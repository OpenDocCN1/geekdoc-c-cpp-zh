340

LOCKS

```
int CompareAndSwap(int *ptr, int expected, int new) {
    int original = *ptr;
    if (original == expected)
        *ptr = new;
    return original;
}
```

Figure 28.4: Compare-and-swap

goes as follows: imagine Thread A on CPU 1 and Thread B on CPU 2, both contending for a lock. If Thread A (CPU 1) grabs the lock, and Thread B tries to, B will spin on (CPU 2). However, presumably the critical section is short, and thus the lock becomes available, and is acquired by Thread B. Spinning to wait for another processor doesn't waste cycles in this case, and thus can be effective.

# 28.9 Compare-And-Swap

Another hardware primitive that systems provide is known as the compare-and-swap (it is called in SPARC, for example), or compare-and-exchange (it is called on x86). The C pseudocode for this single instruction is found in Figure 28.4.

The basic idea is for compare-and-swap to test whether the value at the address specified by ptr is equal to expected; if so, update the memory location pointed to ptr with the new value. If not, do nothing. In either case, return the original value at memory location, allowing the calling compare-and-swap to work whether it succeeded or not.

With the compare-and-swap instruction, we can build a lock in a manner similar to test-and-set, and we could just replace the lock() routine above with the following:

```
void lock(lock_t *lock) {
    while (CompareAndSwap(&lock->flag, 0, 1) == 1)
        // spin;
}
```

The rest of the code is the same as the test-and-set example. This code works similarly; it simply checks if the flag is 0 and if so, atomically swaps in a 1 acquiring the lock. While the lock is held it will get stuck spinning until the lock is finally released.

If you want to see how to make a C-callable x86-version of compare-and-swap, the code sequence (from [S05]) might be useful.

Finally, as you have sensed, compare-and-swap is a more powerful instruction than test-and-set. We will make some use of this power in

> *github.com/remzi-arpacisseau/ostep-code/tree/master/threads-locks

OPERATING SYSTEMS [VERSION 1.01]

WWW.OSTEP.ORG