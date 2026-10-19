
```
~mutex();

mutex(const mutex&) = delete;
mutex& operator=(const mutex&) = delete;

void lock();
bool try_lock();
void unlock();

using native_handle_type = implementation-defined;    // see 32.2.3
native_handle_type native_handle();                  // see 32.2.3
};
}
```

1 The class mutex provides a non-recursive mutex with exclusive ownership semantics. If one thread owns a mutex object, attempts by another thread to acquire ownership of that object will fail (for try_lock()) or block (for lock()) until the owning thread has released ownership with a call to unlock().

2 [Note 1: After a thread A has called unlock(), releasing a mutex, it is possible for another thread B to lock the same mutex, observe that it is no longer in use, unlock it, and destroy it, before thread A appears to have returned from its unlock call. Implementations are required to handle such scenarios correctly, as long as thread A doesn't access the mutex after the unlock call returns. These cases typically occur when a reference-counted object contains a mutex that is used to protect the reference count. — end note]

3 The class mutex meets all of the mutex requirements (32.5.4). It is a standard-layout class (11.2).

4 [Note 2: A program can deadlock if the thread that owns a mutex object calls lock() on that object. If the implementation can detect the deadlock, a resource_deadlock_would_occur error condition can be observed. — end note]

5 The behavior of a program is undefined if it destroys a mutex object owned by any thread or a thread terminates while owning a mutex object.

## 32.5.4.2.3 Class recursive_mutex [thread.mutex.recursive]

```
namespace std {
class recursive_mutex {
public:
recursive_mutex();
~recursive_mutex();

recursive_mutex(const recursive_mutex&) = delete;
recursive_mutex& operator=(const recursive_mutex&) = delete;

void lock();
bool try_lock() noexcept;
void unlock();

using native_handle_type = implementation-defined;    // see 32.2.3
native_handle_type native_handle();                  // see 32.2.3
};
}
```

1 The class recursive_mutex provides a recursive mutex with exclusive ownership semantics. If one thread owns a recursive_mutex object, attempts by another thread to acquire ownership of that object will fail (for try_lock()) or block (for lock()) until the first thread has completely released ownership.

2 The class recursive_mutex meets all of the mutex requirements (32.5.4). It is a standard-layout class (11.2).

3 A thread that owns a recursive_mutex object may acquire additional levels of ownership by calling lock() or try_lock() on that object. It is unspecified how many levels of ownership may be acquired by a single thread. If a thread has already acquired the maximum level of ownership for a recursive_mutex object, additional calls to try_lock() fail, and additional calls to lock() throw an exception of type system_error. A thread shall call unlock() once for each level of ownership acquired by calls to lock() and try_lock(). Only when all levels of ownership have been released may ownership be acquired by another thread.

4 The behavior of a program is undefined if:
(4.1) — it destroys a recursive_mutex object owned by any thread or

# ISO/IEC 14882:2020(E)

Throws: Timeout-related exceptions (32.2.4).

The expression m.try_lock_shared_until(abs_time) is well-formed and has the following semantics:

Preconditions: The calling thread has no ownership of the mutex.

Effects: The function attempts to obtain shared ownership of the mutex. If abs_time has already passed, the function attempts to obtain shared ownership without blocking (as if by calling try_lock_shared()). The function returns before the absolute timeout (32.2.4) specified by abs_time only if it has obtained shared ownership of the mutex object.

> [Note 2: As with try_lock(), there is no guarantee that ownership will be obtained if the lock is available, but implementations are expected to make a strong effort to do so. — end note]

If an exception is thrown then a shared lock has not been acquired for the current thread.

Return type: bool.

Returns: true if the shared lock was acquired, false otherwise.

Synchronization: If try_lock_shared_until() returns true, prior unlock() operations on the same object synchronize with (6.9.2) this operation.

Throws: Timeout-related exceptions (32.2.4).

## 32.5.4.5.2 Class shared_timed_mutex [thread.sharedtimedmutex.class]

```
namespace std {
  class shared_timed_mutex {
  public:
    shared_timed_mutex();
    ~shared_timed_mutex();

    shared_timed_mutex(const shared_timed_mutex&) = delete;
    shared_timed_mutex& operator=(const shared_timed_mutex&) = delete;

    // exclusive ownership
    void lock();                // blocking
    bool try_lock();
    template<class Rep, class Period>
      bool try_lock_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
      bool try_lock_until(const chrono::time_point<Clock, Duration>& abs_time);
    void unlock();

    // shared ownership
    void lock_shared();         // blocking
    bool try_lock_shared();
    template<class Rep, class Period>
      bool try_lock_shared_for(const chrono::duration<Rep, Period>& rel_time);
    template<class Clock, class Duration>
      bool try_lock_shared_until(const chrono::time_point<Clock, Duration>& abs_time);
    void unlock_shared();
  };
}
```

The class shared_timed_mutex provides a non-recursive mutex with shared ownership semantics.

The class shared_timed_mutex meets all of the shared timed mutex requirements (32.5.4.5). It is a standard-layout class (11.2).

The behavior of a program is undefined if:

- — it destroys a shared_timed_mutex object owned by any thread,
- — a thread attempts to recursively gain any ownership of a shared_timed_mutex, or
- — a thread terminates while possessing any ownership of a shared_timed_mutex.

## 32.5.5 Locks [thread.lock]

### 32.5.5.1 General [thread.lock.general]

1 A lock is an object that holds a reference to a lockable object and may unlock the lockable object during the lock’s destruction (such as when leaving block scope). An execution agent may use a lock to aid in managing ownership of a lockable object in an exception safe manner. A lock is said to own a lockable object if it is currently managing the ownership of that lockable object for an execution agent. A lock does not manage the lifetime of the lockable object it references.

> [Note 1: Locks are intended to ease the burden of unlocking the lockable object under both normal and exceptional circumstances. — end note]

2 Some lock constructors take tag types which describe what should be done with the lockable object during the lock’s construction.

```
namespace std {
  struct defer_lock_t { };      // do not acquire ownership of the mutex
  struct try_to_lock_t { };    // try to acquire ownership of the mutex
                              // without blocking
  struct adopt_lock_t  { };    // assume the calling thread has already
                              // obtained mutex ownership and manage it

  inline constexpr defer_lock_t  defer_lock { };
  inline constexpr try_to_lock_t try_to_lock { };
  inline constexpr adopt_lock_t  adopt_lock { };
}
```

## 32.5.5.2 Class template lock_guard [thread.lock.guard]

```
namespace std {
template<class Mutex>
class lock_guard {
public:
  using mutex_type = Mutex;

  explicit lock_guard(mutex_type& m);
  lock_guard(mutex_type& m, adopt_lock_t);
  ~lock_guard();

  lock_guard(const lock_guard&) = delete;
  lock_guard& operator=(const lock_guard&) = delete;

private:
  mutex_type& pm;            // exposition only
};
}
```

1 An object of type lock_guard controls the ownership of a lockable object within a scope. A lock_guard object maintains ownership of a lockable object throughout the lock_guard object’s lifetime (6.7.3). The behavior of a program is undefined if the lockable object referenced by pm does not exist for the entire lifetime of the lock_guard object. The supplied Mutex type shall meet the Cpp17BasicLockable requirements (32.2.5.2).

```
explicit lock_guard(mutex_type& m);
```

2 Preconditions: If mutex_type is not a recursive mutex, the calling thread does not own the mutex m.

3 Effects: Initializes pm with m. Calls m.lock().

```
lock_guard(mutex_type& m, adopt_lock_t);
```

4 Preconditions: The calling thread owns the mutex m.

5 Effects: Initializes pm with m.

6 Throws: Nothing.

```
~lock_guard();
```

7 Effects: As if by pm.unlock().
