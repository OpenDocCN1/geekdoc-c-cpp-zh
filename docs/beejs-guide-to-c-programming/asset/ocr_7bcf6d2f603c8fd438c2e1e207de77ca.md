# Chapter 39. Multithreading

Thread 1: Craziness! x != foo! 10 != 11
Thread 2: x = 12, foo = 12
Thread 4: x = 13, foo = 13
Thread 3: x = 14, foo = 14

In thread 1, between the two printf(), the value of foo somehow changed from 10 to 11, even though clearly there's no increment between the printf()

It was another thread that (probably thread 0, from the look of it) and incremented the value of foo behind thread 1's back!

Let's solve this different ways. (If you want all the threads to share the variable and not step on each other's, you will have to read the next section.)

# 39.6.1 _Thread_local_Storage-Class

First things first, let's just look at the easy way around this: _Thread_local_storage-class.

Basically we're just going to slip on this of our block static variable and things will work! It tells C every thread should have its own version of this static, none of them step on each other toes.

The <threads.h> header defines thread_local as an alias to _Thread_local so each thread's code doesn't have to look so ugly.

Let's take the previous example and make foo into a thread_local variable so that we don't share that data.

```
int run(void *arg)
 n = *(int*)arg; // Thread number for humans to differentiate

free(arg);

thread_local static int foo = 10; // No longer shared!!
```

And running we get:

Thread 0: x = 10, foo = 10
Thread 1: x = 10, foo = 10
Thread 2: x = 10, foo = 10
Thread 4: x = 10, foo = 10
Thread 3: x = 10, foo = 10

No more weird problems!

One thing: if a thread_local variable is block scope, it must be static. Them's the rules. (But this is OK because non-static variables are per-thread already since each thread's its own non-static variables.)

A bit of a lie there: block scope thread_local variables can also be extern.

# 39.6.2 Another Option: Thread-Specific Storage

Thread-specific storage (TSS) is another way of getting per-thread data.
One additional feature is that these functions allow you to define a destructor that will be called on the data when the TSS variable is deleted. Commonly this destructor is free() to automatically clean up malloc()d per-thread data. OR NULL if you don't need to destroy anything.