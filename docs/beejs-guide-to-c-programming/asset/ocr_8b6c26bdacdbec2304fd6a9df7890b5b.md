# Chapter 39. Multithreading

thrd_create() takes a pointer to the function to run, and it's of type thrd_start_t, which is int (*void *). That's Greek for a 'pointer to a function that avoids void' as an argument, and returns an int.

Let's make a thread! We'll launch it from the main thread with thrd_create() to run a function, do some other things, then wait for it to complete with thrd_join(). I've named the thread's main function run(), but you can name it anything as long as the types match thrd_start_t.

```
#include <stdio.h>
#include <threads.h>
```

```
// This is the function that will run. It can be called anything.
```

```
// arg is the argument pointer passed to `thrd_create()`
```

```
// The parent thread will get the return value back from `thrd_join()`
```

```
// later.
```

```
int run(void *arg)
{
    int *a = arg; // We'll pass in an int* from thrd_create()
```

```
printf("THREAD: Running thread with %d\n", *a);

return 12; // Value to be picked up by thrd_join() (chose 12 at random)
```

```
int main(void)
{
    thrd_t t; // t will hold the thread ID
    int arg = 3490;
```

```
printf("Launching a thread\n");

// Launch a thread to the run() function, passing a pointer to 3490
// as an argument. Also stored the thread ID in t:
```

```
thrd_create(&t, run, &arg);

printf("Doing other things while the thread runs\n");

printf("Waiting for thread to complete...\n");
```

```
int res; // Holds return value from the thread exit

// Wait for the thread to complete; store the return value
// in res:
```

```
thrd_join(t, &res);

printf("Thread exited with return value %d\n", res);
}
```

See how we used the thrd_create() to call the run() function? Then we did other things in main() and then stopped and waited for the thread to complete with thrd_join().