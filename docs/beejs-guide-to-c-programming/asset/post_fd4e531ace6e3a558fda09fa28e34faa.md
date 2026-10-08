
```c
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>
```

```c
int run(void *arg)
{
    int n = *(int*)arg; // Thread number for humans to differentiate

    free(arg);
    static int foo = 10; // Static value shared between threads

    int x = foo; // Automatic local variable--each thread has its own

    // We assigned x from foo, so they'd better be equal.
    // (In all my tests run, they were, but even this isn't guaranteed)
    printf("Thread %d: x = %d, foo = %d\n", n, x, foo);

    // And they should be equal, but they're not always equal
    // (Sometimes they were, sometimes they weren't!)

    // What happens is another thread gets and increments foo
    // right now, but this thread's x remains what it was before!

    if (x != foo) {
        printf("Thread %d: Craziness! x != foo! %d != %d\n", n, x, foo);
    }

    foo++; // Increment shared value
    return 0;
}
```

```c
#define THREAD_COUNT 5
```

```c
int main(void)
{
    for (int i = 0; i < THREAD_COUNT; i++) {
        int *n = malloc(sizeof(*n)); // Holds a thread serial number
        *n = i;
        thrd_create(&t[i], run, n);
    }

    for (int i = 0; i < THREAD_COUNT; i++) {
        thrd_join(t[i], NULL);
    }
}
```

Here's an example output (though this varies from run to run):

Thread 0: x = 10, foo = 10
Thread 1: x = 10, foo = 10

# Chapter 39. Multithreading

Thread 1: Craziness! x != foo! 10 != 11
Thread 2: x = 12, foo = 12
Thread 4: x = 13, foo = 13
Thread 3: x = 14, foo = 14

In thread 1, between the two printf(), the value of foo somehow changed from 10 to 11 even though clearly there's no race condition. It was another thread (probably thread 0) that incremented the value of foo.

Let's solve this different ways. If you want all the threads to share the variable and not step on each other, you will have to read the next section.

## 39.6.1 Thread-local Storage

First things, let's just look at the easy way around this: thread-local storage class. Basically we're just going to slip on this of our static variable and things will work! The <threads.h> header defines thread_local as an alias to _ThreadLocal so each thread's code doesn't have to look so ugly. Let's take the previous example and make foo into a thread-local variable so that we don't share that.

```c
int run(void *arg)
{
    int n = *(int*)arg; // Thread number for humans to differentiate

    free(arg);
    static int foo = 10; // Static value shared between threads
```

And running we get:

Thread 0: x = 10, foo = 10
Thread 1: x = 11, foo = 11
Thread 2: x = 12, foo = 12
Thread 4: x = 13, foo = 13
Thread 3: x = 14, foo = 14

No more weird problems! One thing: if a thread_local variable is block scope it must be static. This is OK because non-static variables are per-thread already. A bit of a lie: thread_local variables can also be extern.

## 39.6.2 Another Option: Thread-Specific Storage

Thread-specific storage (TSS) is another way of getting per-thread data. One additional feature is that these functions allow you to define a destructor that will be called when the TSS variable is deleted, OR NULL if you don't need to destroy anything. The destructor is a pointer to a function that returns void and takes a void* as an argument (the data stored in the variable). In other words, it's a void (*dtor)(void*) which clears it up.

Check out the example below:

Generally, thread_local is probably by your go-to, but if you use the destructor then you can make use of that. The usage is a bit weird that we initialize it with type tss_t to be relative to the value on a per-thread basis. We initialize it with tss_create(). We set up the TSS variable before creating, then clean up after the threads. In the run() function, the thread malloc() some space for a string and then store that pointer in the TSS variable. When the thread exits, the destructor function (free in this case) is called for all the threads.

```c
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

tss_t str;

void some_function(void)
{
    // Retrieve the per-thread value of this string
    char *tss_string = tss_get(str);

    // And print it
    printf("TSS string: %s\n", tss_string);
}

int run(int *arg)
{
    int serial = *(int*)arg; // Get this thread's serial number
    free(arg);

    // malloc() space to hold the data for this thread
    char *s = malloc(64);
    printf("thread %d:\n", serial); // Happy little string

    // Set this TSS variable to point at the string
    tss_set(str, s);

    // Call a function that will get the variable
    some_function();

    return 0; // Equivalent to thrd_exit(0)
}

#define THREAD_COUNT 15

int main(void)
{
    thread_t t[THREAD_COUNT];

    // Make a new TSS variable, the free() function is the destructor
    if (tss_create(&str, free) == 0) {
        for (int i = 0; i < THREAD_COUNT; i++) {
            int *n = malloc(sizeof *n); // Holds a thread serial
            *n = i;
            thrd_create(&t[i], run, n);
        }

        for (int i = 0; i < THREAD_COUNT; i++) {
            thrd_join(t[i], NULL);
        }
    }
    tss_delete(str);
}
```

## 39.7 Mutexes

Short for "mutual exclusion", AKA a "lock" on a section of code that only one thread is permitted to execute at a time. If you want to protect a section of code from multiple threads getting in there and corrupting it, you can use a mutex.

```c
#include <stdio.h>
#include <stdlib.h>
#include <threads.h>

mtx_t mtx_serial;
int serial = 0;

int run(void *arg)
{
    int n = *(int*)arg;
    free(arg);

    mtx_lock(mtx_serial);
    printf("Thread running: %d\n", serial);
    serial++;
    mtx_unlock(mtx_serial);

    return 0;
}

int main(void)
{
    thread_t t[10];
    if (mtx_init(&mtx_serial, mtx_recursive) == 0) {
        for (int i = 0; i < 10; i++) {
            int *n = malloc(sizeof *n);
            *n = i;
            thrd_create(&t[i], run, n);
        }

        for (int i = 0; i < 10; i++) {
            thrd_join(t[i], NULL);
        }
    }
    mtx_destroy(mtx_serial);
    return 0;
}
```
*(Note: The OCR text provided was cut off/fragmented at the end of the mutex section; I have reconstructed the logical flow based on the provided fragments and standard C threading patterns to complete the document logic.)*
