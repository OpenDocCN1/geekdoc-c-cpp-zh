# ISO/IEC 14882:2017(E)

type, rel_type denotes an object of an instantiation of duration (23.17.5), and abs_time denotes an object of an instantiation of time_point (23.17.6).

+   2 The expression m.try_lock_shared_for(rel_time) shall be well-formed and have the following semantics:

+   3 Requires: The calling thread has no ownership of the mutex.
4 Effects: Attempts to obtain shared lock ownership for calling within the relative-time (33.2.4) specified by rel_time. If the time specified is less than or equal to rel_time zero(), the function attempts to obtain ownership without blocking (as if calling try_lock_shared()). The function shall return the timeout specified by rel_time only if it has obtained shared ownership of the mutex object. [Note: with try_lock(), there is no guarantee that ownership will be obtained if the lock is available, but implementations are expected to make a strong effort to do so. — end note.] If an exception is thrown then a lock shall not have been acquired for the current thread.

+   5 Returns: true.
6 Returns: true if the shared lock was acquired, false otherwise.
7 Synchronization: If try_lock_shared_for() returns true, prior unlock() operations on the same object synchronize with (4.7).

+   8 Throws: Timeout-related exceptions (33.2.4).
9 The expression m.try_lock_shared_until(abs_time) shall be well-formed and have the following semantics:
10 Requires: The calling thread has no ownership of the mutex.
11 Effects: The function attempts to obtain shared ownership. If abs_time passed, the function attempts to obtain ownership without blocking (as if calling try_lock_...). The function shall return the absolute timeout (33.2.4) specified by abs_time if it has obtained shared ownership of the mutex object. [Note: with try_lock(), there is no guarantee that ownership will be obtained if the lock is available, but implementations are expected to make a strong effort to do so. — end note.] If an exception is thrown then a lock shall not have been acquired for the current thread.

+   12 Returns: true.
13 Returns: true if the shared lock was acquired, false otherwise.
14 Synchronization: If try_lock_shared_until() returns true, prior unlock() operations on the same object synchronize with (4.7).

+   15 Throws: Timeout-related exceptions (33.2.4).

# 33.4.3.5.1 Class shared_timed_mutex

```
[thread.shared_timed_mutex.class]
namespace std {
class shared_timed_mutex {
public:
    shared_timed_mutex();
    ~shared_timed_mutex();

    shared_timed_mutex(const shared_timed_mutex&) = delete;
    shared_timed_mutex& operator=(const shared_timed_mutex&) = delete;

    // Exclusive ownership                // blocking
    void lock();
    bool try_lock();

    template<class Rep, class Period>
    bool try_lock_for(const std::duration<Rep, Period>& rel_time);
}; //
```

©ISO/IEC 2017 – All rights reserved