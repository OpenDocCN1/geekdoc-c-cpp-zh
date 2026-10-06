# ISO/IEC 14882:2017(E)

17 The expression m.try_lock_shared() shall be well-formed and have the following semantics:

18 Requires: The calling thread has no ownership of the mutex.

19 Effects: Attempts to obtain shared ownership of the mutex for the calling thread without blocking. If shared ownership is not obtained, there is no effect and try_lock_shared() immediately returns. An implementation may fail to obtain the lock if it is not held by any other thread.

20 Return type: bool.

21 Returns: true if the shared ownership was acquired, otherwise false.

22 Synchronization: If try_lock_shared() returns true, prior unlock() operations on the same object synchronize with (4.7) this operation.

23 Throws:

# 33.4.3.4 Class shared_mutex

```
namespace std {
    class shared_mutex {
    public:
        shared_mutex();
        ~shared_mutex() = delete;

        shared_mutex(const shared_mutex&) = delete;
        shared_mutex& operator=(const shared_mutex&) = delete;

        // Exclusive ownership
        void lock();
        bool try_lock();
        void unlock();

        // Shared ownership
        void lock_shared();
        bool try_lock_shared();
        void unlock_shared();

        using native_handle_type = implementation_defined;
        native_handle_type native_handle();
    };
};
```

[thread.shared_mutex.class]

+   1 The class shared_mutex shall provide a recursive mutex with shared ownership semantics. It shall be a standard-layout class (Clause 12).

+   2 The behavior of a shared_mutex is undefined if:
- it destroys a shared_mutex object owned by any thread,
- a thread attempts to recursively gain any ownership of a shared_mutex,
- a thread terminates while possessing any ownership of a shared_mutex.

4 shared_mutex may be a synonym for shared_timed_mutex.

# 33.4.3.5 Shared timed mutex types

+   1 The standard library type shared_timed_mutex is a shared timed mutex type. Shared timed mutex types shall meet the requirements of timed mutex types (33.4.3.3), shared mutex types (33.4.3.4), and additionally shall meet the requirements set out below. In this description, m denotes an object of a shared timed mutex

[thread.sharedtimedmutex.requirements]