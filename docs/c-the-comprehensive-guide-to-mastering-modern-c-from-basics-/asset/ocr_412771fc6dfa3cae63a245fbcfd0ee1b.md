Some operations in a CPU register take less than one cycle. Reading from memory can be 30 times slower. A simple additional lock for synchronization takes between to ten times as much time. You have achieved a lot if you can get your read/write operations distributed across two threads as fast as memory access. Faster is an absolute exception.

# 29.7.3 Example

Using a short example, I would demonstrate both the general usage of atomic and the memory orders.

The SpinlockMutex class implements a mutex that you can use together with one of the lock classes. The advantage over a normal mutex is that the thread is not put to sleep when it tries to lock the SpinlockMutex. Instead, it waits in a tight loop for the lock to be released. This approach is a good idea if you expect to wait only a very short time for the lock to be released. Putting a thread to sleep and waking it up again takes time. If the mutex is unlocked just after one or two loops, it is better.

```
// https://godbolt.org/EnjPrSr76
#include <atomic>
class SpinlockMutex {
    std::atomic_flag flag;
public:
    SpinlockMutex()
        : flag_(ATOMIC_FLAG_INIT)
    {}
    void lock() { // e.g., called by
        lock_guard
        while(flag_.test_and_set(std::memory_order_acquire)) // mostly read
            /* nothing * */
    }
    void unlock() {
```