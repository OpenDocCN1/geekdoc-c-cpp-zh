# Chapter 40. Atomics

```
thrd_t t1, t2;

thrd_create(&t1, thread1, NULL);
thrd_create(&t2, thread2, NULL);

thrd_join(t1, NULL);
thrd_join(t2, NULL);
```

```
printf("Main : Threads are done, so x will be 3490\n");
printf("Main : And indeed, x == %d\n", x);
```

The second thread spins in place, looking at the flag and waiting for it to set to the value 3490. And the first one does that:

+   And I get this output:
- Thread 1: Sleeping for 1.5 seconds
Thread 2: Waiting for 3490
Thread 1: Setting x to 3490
Thread 1: Exiting
Thread 2: Got 3490--exiting!
Main : Threads are done, so x will be 3490
Main : And indeed, x == 3490

Look, we're accessing a variable from different threads and not using a mutex! And that'll work fine thanks to the atomic nature of atomic variables.

You might be wondering what happens if it's a regular non-atomic int, instead. Well, on my system it works... unless I do an optimized build in case it hits on thread 2 waiting to set the 3490 to get set.

But that's just the beginning of the story. The next part is going to require more brain power and has to do with something synchronization.

# 40.3 Synchronization

The next part of our story is all about when memory writes in one thread become visible to those in another thread.

You might think, it's alright, right? But it's not. A number of things can go wrong. Weirdly wrong.
The compiler might have rearranged memory accesses that when you set a value relative to another might not be. And even if the compiler didn't, your CPU might do it on the fly. Or maybe there's something else about this that causes races on one CPU to be delayed before they're visible on another.

By way of example, what happens first in the following code, the write to x or the thread to write y?

```
int x, y; // global
```

> The reason for this is when optimized, my compiler has put the value of x in a register to make the while loop fast. The register has no way of knowing the variable was updated in another thread, so it never sees the 3490. This isn't really related to the all-or-nothing fact of atomicity, but is more related to the synchronization aspects in the next section.