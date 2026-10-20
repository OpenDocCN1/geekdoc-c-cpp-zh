a process to have its own copy of a data item, such as a variable. You may store a copy of a variable in a thread-specific data area. A change made to this variable is invisible to other threads.

You can create as many thread-specific data items as you want, each of type void*. Each such item is referenced by a key that you create using pthread_key_create(). The first parameter of this function is a pointer to an object of type pthread_key_t and the second is the thread cleanup function. The cleanup function is called automatically to deallocate a thread-specific data item when each thread terminates. This function is called even if the thread is canceled during its execution. Cleanup functions are used to prevent memory leaks. If you don't need a cleanup function, you set the second parameter to null.

```
...
 pthread_key_t thread_key;
 ...
 void * thread_fn (void *args)
 {
 ...
 int thread_item;
 ...
 pthread_setspecific(thread_key, thread_item);
 ...
 }
```

You can access a thread-specific data item using the pthread_getspecific() function that takes the key as its only argument and returns the data item associated with the key. Since thread-specific values are stored as void type, you must typecast them into the desired type, as in the following code snippet.

```
...
 int fd;
 ...
 fd = (int) pthread_getspecific(thread_key);
 ...

```



The pthread library provides support for a wide range of synchronization constructs (also known as primitives), including mutexes, reader-write-locks, semaphores, and condition variables. You can use these primitives to solve a range of problems in concurrent programming related to race conditions and the critical section problem. Table 16.12 shows a set of pthread library functions related to the abovementioned synchronization construct.

Further discussion on the synchronization topics is beyond the scope of this book. The interested reader may read more about them in a book on operating system concepts and principles, concurrent programming, or multithreaded programming.

# Summary

We described the Linux system calls and their use in small programs for process creation, process termination, and process management. Before discussing the system calls, we explained in detail the concept of processes and threads. We then discussed how they differ from each other and the concept of user- and kernel-level threads. We also discussed the following concepts and kernel data structures in Linux: the PCB, memory and disk images of processes, zombie processes, signals, and signal handling.