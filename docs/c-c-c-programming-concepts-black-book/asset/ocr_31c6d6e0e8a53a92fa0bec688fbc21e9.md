```
```c
res = pthread_create(&thread2, NULL, thread_function, &arr);
if (res != 0) {
    fprintf(stderr, "\nThread creation failed\n");
    return 1;
}

fprintf(stdout, "\nWaiting for threads to finish...\n");
res = pthread_join(thread1, NULL);
if (res != 0) {
    fprintf(stderr, "\nThread join failed\n");
    return 0;
}
res = pthread_join(thread2, NULL);
if (res != 0) {
    fprintf(stderr, "\nThread join failed\n");
    return 0;
}

fprintf(stdout, "\nThread joined. \n");
for (i = 0; i < ARRRSIZE; i++)
    fprintf(stdout, "\narr[%d] = %d. Correct Result=[%d]", i, arr.arr[i], i*10);
    if (arr.arr[i] != (i*10))
        fprintf(stdout, " INCORRECT");
    }
}
return 0;
}
```
```

In the preceding program, we have created two threads using the pthread_create() API and let them execute the same thread function on their own. This would result in the synchronization problem between the two threads. To solve the problem of synchronization in a multithreading environment, we use the concept called mutex. Let’s learn about it in the next section.

# Mutex

Mutexes or mutual exclusion locks are enforced to avoid situations where one thread is operating on a shared variable. Similar to locks, the states of a mutex can also vary between locked and unlocked. Once a thread has locked a mutex, no other thread will be able to lock or acquire that mutex. Other threads should wait until the mutex is released; otherwise, an attempt to lock that mutex will lock the thread. After the mutex is unlocked, one of the threads waiting for it will be unlocked to acquire the lock on it.

Linux ensures an atomic lock operation on a mutex, that is, even if multiple threads are in the race to lock the same mutex, only one thread will be able to acquire the lock. When a mutex is unlocked, only one of the blocked threads waiting on that mutex will be unlocked to acquire the lock. Remaining threads will continue to be in the blocked state.

Following are the steps to use a mutex:

+   - Declare a mutex as pthread_mutex_t mutex;
+   - Initialize the mutex as pthread_mutex_init (&mutex, NULL) Or pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
+   - Lock the mutex as pthread_mutex_lock (&mutex);
+   - Unlock the mutex as pthread_mutex_unlock(&mutex);
+   - Destroy the mutex as pthread_mutex_destroy(&mutex);