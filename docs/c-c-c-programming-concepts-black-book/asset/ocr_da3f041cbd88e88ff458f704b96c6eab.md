```
```c
fprintf(stdout, "\nwaiting for threads to finish...\n");
res = pthread_join(thread1, NULL);
if (res != 0) {
    fprintf(stderr, "\nThread join failed\n");
    return 0;
}

fprintf(stdout, "\nThread joined. \n");
pthread_mutex_destroy(&mutex);

return 0;
}
```
```

Before moving on to the next section, let’s get an overview of a non-blocking mutex lock. The benefit of using a non-blocking mutex lock is that if a mutex is not already locked, then it will obtain the lock; else, if it is already locked, then the call would return with the status EBUSY. Following are the properties of a non-blocking mutex lock:

+   - It is possible to lock an object by mutex lock without actually blocking it using
+   - `int pthread_mutex_trylock(pthread_mutex_t *mutex);`
+   - If a mutex is unlocked, then the `pthread_mutex_trylock()` API would work similar to `pthread_mutex_lock()`
+   - If the mutex object referenced by a mutex is currently locked by any thread including the current thread, then the call to the mutex lock will return immediately.
+   - If the mutex type is `PTHREAD_MUTEX_RECURSIVE_NP` and the mutex is currently owned by the calling thread, then the mutex lock count will be incremented by one and `pthread_mutex_trylock()` will immediately return success.

In the next section, let’s discuss semaphore.

# Semaphore

Semaphore is a protected variable that is used to synchronize the parallel access to the shared accessible resources. Semaphore is a mechanism involving an abstract counter and two operations that can be used to synchronize multiple threads. The following two operations can be performed on semaphores:

+   - **The wait operation**—Decrements the value of the semaphore by one. If the value of the semaphore is zero, then the wait operation blocks a thread until some other thread increments the value of the semaphore. When the value becomes positive, the value of the semaphore is decremented by one and the wait operation returns.
+   - **The post operation**—Increments the value of the semaphore by one. If the value of the semaphore is zero, then the post operation unblocks one of the threads, which is blocked on a wait call to this semaphore. The unblocked thread will complete the wait call. The post operation is also called the signal operation.

Following are the steps to use a semaphore:

+   1. Include `<semaphore.h>`, as follows:
+      ```c
+      #include <semaphore.h>
+      ```
+   2. Declare a semaphore (type is `sem_t`), as follows:
+      ```c
+      sem_t sem;
+      ```
+   3. Initialize the semaphore, as follows:
+      ```c
+      sem_init(&sem, 0, 0);
+      ```