```
```c
#include "apue.h"
#include <pthread.h>

pthread_t ntid;

void
printids(const char *s)
{
    pid_t       pid;
    pthread_t   tid;

    pid = getpid();
    tid = pthread_self();
    printf("%s pid %lu tid %lu (0x%lx)\n", s, (unsigned long)pid,
           (unsigned long)tid, (unsigned long)tid);
}

void *
thr_fn(void *arg)
{
    printids("new thread: ");
    return((void *)0);
}

int
main(void)
{
    int     err;

    err = pthread_create(&ntid, NULL, thr_fn, NULL);
    if (err != 0)
        err_exit(err, "can’t create thread");
    printids("main thread: ");
    sleep(1);
    exit(0);
}
```
```

This example has two oddities, which are necessary to handle races between the main thread and the new thread. (We’ll learn better ways to deal with these conditions later in this chapter.) The first is the need to sleep in the main thread. If it doesn’t sleep, the main thread might exit, thereby terminating the entire process before the new thread gets a chance to run. This behavior is dependent on the operating system’s threads implementation and scheduling algorithms.

The second oddity is that the new thread obtains its thread ID by calling pthread_self instead of reading it out of shared memory or receiving it as an argument to its thread-start routine. Recall that pthread_create will return the

Figure 11.2 creates one thread and prints the process and thread IDs of the new thread and the initial thread.

Figure 11.2  Printing thread IDs