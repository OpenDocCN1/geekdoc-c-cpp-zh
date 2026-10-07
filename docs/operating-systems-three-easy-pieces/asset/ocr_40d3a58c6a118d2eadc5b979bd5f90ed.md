# SEMAPHORES

```
#include <semaphore.h>
sem_t s;
sem_init(&s, 0, 1);
```

Figure 31.1: Initializing A Semaphore

In the figure, we declare a semaphore and initialize it to the value 1 by passing 1 to 0 as the third argument. The second argument to sem_init() will be set to 0 in all of the examples we will see; this indicates that the semaphore is shared between threads in the same process. See the man page for other usages of semaphores (namely, how they can be used for synchronization across different processes), which require a different value for that second argument.

After a semaphore is initialized, we can call one of two functions to interact with it, or sem_post(). The behavior of these two functions is seen in Figure 31.2.

For now, we are not concerned with the implementation of these routines, with multiple threads calling into sem_wait() and sem_post(), there is the obvious need for managing these critical sections. We will now focus on how to use these primitives; later, we may discuss how they are built.

We should discuss a few aspects of the interfaces here. First, we can see that sem_wait() either return away (because the value of the semaphore was 0 or higher when we called sem_wait()), or it will cause the caller to suspend waiting for a subsequent post. Of course, multiple threads may call into sem_wait(), and all will be queued to be woken.

Second, we can see that sem_post() does not wait for some particular condition to hold sem_wait(). Rather, it simply increments the value of the semaphore, and if there is a thread waiting to be woken, wakes one of them.

Third, the value of the semaphore, when negative, is equal to the number of threads [D68b]. Though the value generally isn't seen by users of the semaphores, this invariant is worth knowing and perhaps can help you remember how semaphore functions.

```
int sem_wait(sem_t *s) {
    decrement the value of semaphore s by one
    wait if value of semaphore s is negative
}
```

```
int sem_post(sem_t *s) {
    increment the value of semaphore s by one
    if there are one or more threads waiting, wake one
}
```

Figure 31.2: Definitions Of Wait And Post

OPERATING SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG