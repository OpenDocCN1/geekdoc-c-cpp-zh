resources for the reader-writer lock, pthread_rwlock_destroy frees those resources. If we free the memory backing a reader-writer lock without first calling pthread_rwlock_destroy, any resources assigned to the lock will be lost.

To lock a reader-writer lock in read mode, we call pthread_rwlock_rdlock. To write lock a reader-writer lock, we call pthread_rwlock_wrlock. Regardless of how we lock a reader-writer lock, we can unlock it by calling pthread_rwlock_unlock.

```
#include <pthread.h>
int pthread_rwlock_rdlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_wrlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_unlock(pthread_rwlock_t *rwlock);
All return: 0 if OK, error number on failure
```

Implementations might place a limit on the number of times a reader-writer lock can be locked in shared mode, so we need to check the return value of pthread_rwlock_rdlock. Even though pthread_rwlock_wrlock and pthread_rwlock_unlock have error returns, and technically we should always check for errors when we call functions that can potentially fail, we don’t need to check them if we design our locking properly. The only error returns defined are when we use them improperly, such as with an uninitialized lock, or when we might deadlock by attempting to acquire a lock we already own. However, be aware that specific implementations might define additional error returns.

The Single UNIX Specification also defines conditional versions of the reader-writer locking primitives.

```
#include <pthread.h>
int pthread_rwlock_tryrdlock(pthread_rwlock_t *rwlock);
int pthread_rwlock_trywrlock(pthread_rwlock_t *rwlock);
Both return: 0 if OK, error number on failure
```

When the lock can be acquired, these functions return 0. Otherwise, they return the error EBUSY. These functions can be used to avoid deadlocks in situations where conforming to a lock hierarchy is difficult, as we discussed previously.

# Example

The program in Figure 11.14 illustrates the use of reader-writer locks. A queue of job requests is protected by a single reader-writer lock. This example shows a possible implementation of Figure 11.1, whereby multiple worker threads obtain jobs assigned to them by a single master thread.

```
#include <stdlib.h>
#include <pthread.h>

struct job {
    struct job *j_next;
    struct job *j_prev;
```