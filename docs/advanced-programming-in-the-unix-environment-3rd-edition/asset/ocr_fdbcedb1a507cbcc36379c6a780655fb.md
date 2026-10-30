| Name of limit | Description | name argument |
|---|---|---|
| PTHREAD_DESTRUCTOR_ITERATIONS | maximum number of times an implementation will try to destroy the thread-specific data when a thread exits (Section 12.6) | _SC_THREAD_DESTRUCTOR_ITERATIONS |
| PTHREAD_KEYS_MAX | maximum number of keys that can be created by a process (Section 12.6) | _SC_THREAD_KEYS_MAX |
| PTHREAD_STACK_MIN | minimum number of bytes that can be used for a thread's stack (Section 12.3) | _SC_THREAD_STACK_MIN |
| PTHREAD_THREADS_MAX | maximum number of threads that can be created in a process (Section 12.3) | _SC_THREAD_THREADS_MAX |

Figure 12.1 Thread limits and name arguments to sysconf

Figure 12.2 shows the values of the thread limits for the four implementations described in this book. If the implementation's limit is indeterminate, "no limit" is listed. This doesn't mean that the value is unlimited, however.

> Note that although an implementation may not provide access to these limits, that doesn't mean that the limits don't exist. It just means that the implementation doesn't provide us with a way to get at them using sysconf.

| Limit | FreeBSD 8.0 | Linux 3.2.0 | Mac OS X 10.6.8 | Solaris 10 |
|---|---|---|---|---|
| PTHREAD_DESTRUCTOR_ITERATIONS | 4 | 4 | 4 | no limit |
| PTHREAD_KEYS_MAX | 256 | 1,024 | 512 | no limit |
| PTHREAD_STACK_MIN | 2,048 | 16,384 | 8,192 | 8,192 |
| PTHREAD_THREADS_MAX | no limit | no limit | no limit | no limit |

Figure 12.2 Examples of thread configuration limits

# 12.3 Thread Attributes

The pthread interface allows us to fine-tune the behavior of threads and synchronization objects by setting various attributes associated with each object. Generally, the functions for managing these attributes follow the same pattern:

+   1. Each object is associated with its own type of attribute object (threads with thread attributes, mutexes with mutex attributes, and so on). An attribute object can represent multiple attributes. The attribute object is opaque to applications. This means that applications aren't supposed to know anything about its internal structure, which promotes application portability. Instead, functions are provided to manage the attributes objects.