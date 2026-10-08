# Chapter 40. Atomics

That is, the other will see the entire write of, say, a 32-bit value. Not half of it. There's no way for one thread to interrupt another that is in the middle of an atomic multi-byte write.

It's almost like there is a lock around the getting and setting of one variable. (And there might be See Lock-Free Atomic Variables, below.)

And on that note, you can get away without using atomics if you use mutexes to lock your critical sections. It's just that there are a class of lock-free data structures that always allow other threads to make progress instead of being blocked by a mutex... but these are tough to create from scratch, and one of the things that are beyond the scope of the guide, sadly.

That's only part of the story. But it's the part we'll start with.

Before we go further, how do you declare a variable to be atomic?

First, include <stdatomic.h>.

This gives us types as atomic_int.

And then we can simply declare variables to be of that type.

But let's do a demo when we have two threads. The first runs for a while and then sets a variable to a specific value, then it exits. The other runs until it sees that value set, and then it exits.

```
#include <stdio.h>
#include <threads.h>
#include <stdatomic.h>

atomic_int x; // THE POWER OF ATOMICS! BWHAHAHA!

int thread1(void *arg)
{
    printf("Thread 1: Sleeping for 1.5 seconds\n");
    thrd_sleep(&struct timespec){.tv_sec=1, .tv_nsec=500000000}, NULL);
    printf("Thread 1: Setting x to 3490\n");
    x = 3490;
    printf("Thread 1: Exiting\n");
    return 0;
}

int thread2(void *arg)
{
    (arg);
    printf("Thread 2: Waiting for 3490\n");
    while (x != 3490) {} // spin here
    printf("Thread 2: Got 3490--exiting!\n");
    return 0;
}

int main(void)
{
    x = 0;
```