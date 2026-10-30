```
#include <semaphore.h>
int sem_post(sem_t *sem);
Returns: 0 if OK, -1 on error
```

If a process is blocked in a call to sem_wait (or sem_timedwait) when we call sem_post, the process is awakened and the semaphore count that was just incremented by sem_post is decremented by sem_wait (or sem_timedwait).

When we want to use POSIX semaphores within a single process, it is easier to use unnamed semaphores. This only changes the way we create and destroy the semaphore. To create an unnamed semaphore, we call the sem_init function.

```
#include <semaphore.h>
int sem_init(sem_t *sem, int pshared, unsigned int value);
Returns: 0 if OK, -1 on error
```

The pshared argument indicates if we plan to use the semaphore with multiple processes. If so, we set it to a nonzero value. The value argument specifies the initial value of the semaphore.

Instead of returning a pointer to the semaphore like sem_open does, we need to declare a variable of type sem_t and pass its address to sem_init for initialization. If we plan to use the semaphore between two processes, we need to ensure that the sem argument points into the memory extent that is shared between the processes.

When we are done using the unnamed semaphore, we can discard it by calling the sem_destroy function.

```
#include <semaphore.h>
int sem_destroy(sem_t *sem);
Returns: 0 if OK, -1 on error
```

After calling sem_destroy, we can't use any of the semaphore functions with sem unless we reinitialize it by calling sem_init again.

One other function is available to allow us to retrieve the value of a semaphore. We call the sem_getvalue function for this purpose.

```
#include <semaphore.h>
int sem_getvalue(sem_t *restrict sem, int *restrict valp);
Returns: 0 if OK, -1 on error
```

On success, the integer pointed to by the valp argument will contain the value of the semaphore. Be aware, however, that the value of the semaphore can change by the time that we try to use the value we just read. Unless we use additional synchronization mechanisms to avoid this race, the sem_getvalue function is useful only for debugging.