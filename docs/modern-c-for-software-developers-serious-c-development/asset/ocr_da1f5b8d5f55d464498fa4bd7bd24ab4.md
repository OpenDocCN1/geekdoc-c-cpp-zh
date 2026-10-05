# std::unique_lock<std::mutex>

The class template std::unique_lock<std::mutex> is a wrapper that allows locking, time-constrained locking and recursive locking. The mutex template type must support one of the following functions: lock(), try_lock_for or try_lock_until. The template type must also support the unlock() function.

The following mutex types are supported:

+   1. lock(some_mutex)
2. try_lock(some_mutex)
3. try_lock_for(some_mutex)
4. try_lock_until(some_mutex)
6. owns_lock(some_mutex) - does the object own the mutex

The function owns_lock() determines whether a std::unique object has acquired a lock.

A lock acquired by a unique_lock object will be automatically released if an exception is thrown or if the lock object goes out of scope.

A std::unique_lock object can be used with condition variables. Furthermore the objects are movable but not copyable.

Here is an example of usage:

```
#include <iostream>
#include <thread>
#include <mutex>
std::mutex m1; // mutex for critical section
void print_block(int n, char c) {
    // we can use any of the following mutexes:
    // std::unique_lock<std::mutex> lock (m1);
    // std::unique_lock<std::mutex> try_lock (m1);

```