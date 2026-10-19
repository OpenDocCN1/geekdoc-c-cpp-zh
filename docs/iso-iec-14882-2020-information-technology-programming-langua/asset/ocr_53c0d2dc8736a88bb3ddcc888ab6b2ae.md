# 32.5.2 Header <mutex> synopsis [mutex.syn]

```
namespace std {
    class mutex;
    class recursive_mutex;
    class timed_mutex;
    class recursive_timed_mutex;

    struct defer_lock_t { explicit defer_lock_t() = default; };
    struct try_to_lock_t { explicit try_to_lock_t() = default; };
    struct adopt_lock_t { explicit adopt_lock_t() = default; };

    inline constexpr defer_lock_t defer_lock {};
    inline constexpr try_to_lock_t try_to_lock {};
    inline constexpr adopt_lock_t adopt_lock {};

    template<class Mutex> class lock_guard;
    template<class... MutexTypes> class scoped_lock;
    template<class Mutex> class unique_lock;

    template<class Mutex>
        void swap(unique_lock<Mutex>& x, unique_lock<Mutex>& y) noexcept;

    template<class L1, class L2, class... L3> int try_lock(L1&, L2&, L3&...);
    template<class L1, class L2, class... L3> void lock(L1&, L2&, L3&...);

    struct once_flag;

    template<class Callable, class... Args>
        void call_once(once_flag& flag, Callable&& func, Args&&... args);
}
```

# 32.5.3 Header <shared_mutex> synopsis [shared.mutex.syn]

```
namespace std {
    class shared_mutex;
    class shared_timed_mutex;
    template<class Mutex> class shared_lock;
    template<class Mutex>
        void swap(shared_lock<Mutex>& x, shared_lock<Mutex>& y) noexcept;
}
```

# 32.5.4 Mutex requirements [thread.mutex.requirements]

# 32.5.4.1 In general [thread.mutex.requirements.general]

1 A mutex object facilitates protection against data races and allows safe synchronization of data between execution agents (32.2.5). An execution agent owns a mutex from the time it successfully calls one of the lock functions until it calls unlock. Mutexes can be either recursive or non-recursive, and can grant simultaneous ownership to one or many execution agents. Both recursive and non-recursive mutexes are supplied.

# 32.5.4.2 Mutex types [thread.mutex.requirements.mutex]

# 32.5.4.2.1 General [thread.mutex.requirements.mutex.general]

1 The mutex types are the standard library types mutex, recursive_mutex, timed_mutex, recursive_timed_mutex, shared_mutex, and shared_timed_mutex. They meet the requirements set out in 32.5.4.2. In this description, m denotes an object of a mutex type.

2 The mutex types meet the Cpp17Lockable requirements (32.2.5.3).

3 The mutex types meet Cpp17DefaultConstructible and Cpp17Destructible. If initialization of an object of a mutex type fails, an exception of type system_error is thrown. The mutex types are neither copyable nor movable.

4 The error conditions for error codes, if any, reported by member functions of the mutex types are as follows:

+   (4.1) — resource_unavailable_try_again — if any native handle type manipulated is not available.
+   (4.2) — operation_not_permitted — if the thread does not have the privilege to perform the operation.