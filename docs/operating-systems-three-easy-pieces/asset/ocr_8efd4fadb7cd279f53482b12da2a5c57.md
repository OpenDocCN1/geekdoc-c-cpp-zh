# COMMON CONCURRENCY PROBLEMS

along the way, it must make sure to carefully release them as well; for example, if after acquiring L1, the code had some memory, it would have to release that memory upon failure to acquire L2, before jumping back to the top to try the entire sequence. However, in limited circumstances (e.g., the Java vector method mentioned earlier), this type of approach could work.

You might notice that this approach doesn't add preemption (the forcible action of taking a lock away from a thread that owns it), but rather uses the trylock approach to allow a developer to back out of lock ownership (i.e., preempt their ownership) in a graceful way. However, it is a practical approach, and thus we include it here, despite its imperfection in the draft.

# Mutual Exclusion

The final technique would be to avoid the mutual exclusion at all. In general, we know this is difficult, because the code we wish to run does critical sections. What can we do?
heri has the idea that we could design various data structures without locks at [H91, H93]. The idea behind these lock-free (and wait-free) approaches here is: using powerful hardware instructions, you can build data structures in a manner that does not require explicit locking.
As a simple example, let us assume we have a compare-and-swap instruction, which may be an atomic instruction provided by the hardware that does the following:

```
1 int CompareAndSwap(int *address, int expected, int new) {
2   if (*address == expected) {
3     *address = new;
4     return 1; // success
5   }
6   return 0; // failure
7}
```

Imagine we wanted to atomically increment a value by a certain amount, using compare-and-swap. We could do so with the following simple function:

```
1 void AtomicIncrement(int *value, int amount) {
2   do {
3     int old = *value;
4   } while (CompareAndSwap(value, old, old + amount) == 0);
5 }
```

Instead of acquiring a lock, doing the update, and then releasing it, we have built an approach that repeatedly tries to update the value to the new amount and uses the compare-and-swap to do so. In this manner,

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG