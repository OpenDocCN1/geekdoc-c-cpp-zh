# ISO/IEC 14882:2017(E)

1 An object of type scoped_lock controls the ownership of lockable objects within a scope. A scoped_lock obtains ownership of lockable objects throughout the scoped_lock object's lifetime (6.8). The behavior of a program is undefined if the lockable objects referenced by pm do not exist for the entire lifetime of the scoped_lock object. When sizeofof...(MutexTypes) is 1, the supplied Mutex type must have the BasicLockable requirements (33.2.5.2). Otherwise, the mutex types must satisfy the Lockable requirements (33.2.5.3).

2 explicit scoped_lock(MutexTypes... m);

3 Requires: If a Mutex type is not a recursive mutex, the thread does not own the corresponding mutex element of m. Effects: Initializes with pm(...). If sizeof...(MutexTypes) is 0, then lock(m). Otherwise, lock(m...).

explicit scoped_lock(MutexTypes... m, adopt_lock_t);

4 Requires: The calling thread owns the mutexes in m.

5 Effects: Initializes with pm(m...).

6 Throws: Nothing.

-scoped_lock();

7 Effects: For all i in [0, sizeof...(MutexTypes)], get<i>(pm).unlock().

# 33.4.4.3 Class unique_lock

```
namespace std {
    template <class Mutex>
    class unique_lock {
    public:
        using mutextype = Mutex;
        // 33.4.4.1. construct/destroy
        unique_lock() noexcept;
        explicit unique_lock(mutex& m, defer_lock_t) noexcept;
        unique_lock(mutex& m, adopt_lock_t) noexcept;
        unique_lock(mutextype& m, try_to_lock_t);
        template <class Clock, class Duration>
        unique_lock(Clock& m, const chrono::time_point<Clock, Duration>& abs_time);
        template <class Rep, class Period>
        unique_lock(mutextype& m, const chrono::duration<Rep, Period>& rel_time);
        -unique_lock();

        unique_lock(const unique_lock&) = delete;
        unique_lock& operator=(const unique_lock&) = delete;

        unique_lock(unique_lock&&) noexcept;
        unique_lock& operator=(unique_lock&&) noexcept;

        // 33.4.4.3. locking
        void lock();
        bool try_lock();

        template <class Rep, class Period>
        bool try_lock_for(const chrono::duration<Rep, Period>& rel_time);

```

> [thread.lock.unique]

©ISO/IEC 2017 - All rights reserved

1374