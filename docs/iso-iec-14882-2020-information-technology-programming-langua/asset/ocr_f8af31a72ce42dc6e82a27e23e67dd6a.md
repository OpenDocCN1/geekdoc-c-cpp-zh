```
template<class Mutex>
    void swap(shared_lock<Mutex>& x, shared_lock<Mutex>& y) noexcept;
}
```

1 An object of type shared_lock controls the shared ownership of a lockable object within a scope. Shared ownership of the lockable object may be acquired at construction or after construction, and may be transferred, after acquisition, to another shared_lock object. Objects of type shared_lock are not copyable but are movable. The behavior of a program is undefined if the contained pointer pm is not null and the lockable object pointed to by pm does not exist for the entire remaining lifetime (6.7.3) of the shared_lock object. The supplied Mutex type shall meet the shared mutex requirements (32.5.4.5).

2 [Note 1: shared_lock<Mutex> meets the Cpp17TimedLockable requirements (32.2.5.4). — end note]

# 32.5.5.5.2 Constructors, destructor, and assignment [thread.lock.shared.cons]

```
shared_lock() noexcept;
```

1 Postconditions: pm == nullptr and owns == false.

```
explicit shared_lock(mutex_type& m);
```

2 Preconditions: The calling thread does not own the mutex for any ownership mode.

3 Effects: Calls m.lock_shared().

4 Postconditions: pm == addressof(m) and owns == true.

```
shared_lock(mutex_type& m, defer_lock_t) noexcept;
```

5 Postconditions: pm == addressof(m) and owns == false.

```
shared_lock(mutex_type& m, try_to_lock_t);
```

6 Preconditions: The calling thread does not own the mutex for any ownership mode.

7 Effects: Calls m.try_lock_shared().

8 Postconditions: pm == addressof(m) and owns == res where res is the value returned by the call to m.try_lock_shared().

```
shared_lock(mutex_type& m, adopt_lock_t);
```

9 Preconditions: The calling thread has shared ownership of the mutex.

10 Postconditions: pm == addressof(m) and owns == true.

```
template<class Clock, class Duration>
    shared_lock(mutex_type& m,
                const chrono::time_point<Clock, Duration>& abs_time);
```

11 Preconditions: The calling thread does not own the mutex for any ownership mode.

12 Effects: Calls m.try_lock_shared_until(abs_time).

13 Postconditions: pm == addressof(m) and owns == res where res is the value returned by the call to m.try_lock_shared_until(abs_time).

```
template<class Rep, class Period>
    shared_lock(mutex_type& m,
                const chrono::duration<Rep, Period>& rel_time);
```

14 Preconditions: The calling thread does not own the mutex for any ownership mode.

15 Effects: Calls m.try_lock_shared_for(rel_time).

16 Postconditions: pm == addressof(m) and owns == res where res is the value returned by the call to m.try_lock_shared_for(rel_time).

```
~shared_lock();
```

17 Effects: If owns calls pm->unlock_shared().

```
shared_lock(shared_lock&& sl) noexcept;
```

18 Postconditions: pm == sl_p.pm and owns == sl_p.owns (where sl_p is the state of sl just prior to this construction), sl.pm == nullptr and sl.owns == false.