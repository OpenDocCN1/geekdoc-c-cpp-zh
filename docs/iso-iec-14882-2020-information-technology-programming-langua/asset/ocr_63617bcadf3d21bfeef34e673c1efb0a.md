# ISO/IEC 14882:2020(E)

```
template<class Rep, class Period>
    cv_status wait_for(unique_lock<mutex>& lock,
                    const chrono::duration<Rep, Period>& rel_time);
```

Preconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread, and either

+   - no other thread is waiting on this condition_variable object or
+   - lock.mutex() returns the same value for each of the lock arguments supplied by all concurrently waiting (via wait, wait_for, or wait_until) threads.

Effects: Equivalent to:

```
return wait_until(lock, chrono::steady_clock::now() + rel_time);
```

Returns: cv_status::timeout if the relative timeout (32.2.4) specified by rel_time expired, otherwise cv_status::no_timeout.

Remarks: If the function fails to meet the postcondition, terminate() is called (14.6.2).

> [Note 5: This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread.

Throws: Timeout-related exceptions (32.2.4).

```
template<class Clock, class Duration, class Predicate>
    bool wait_until(unique_lock<mutex>& lock,
                    const chrono::time_point<Clock, Duration>& abs_time,
                    Predicate pred);
```

Preconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread, and either

+   - no other thread is waiting on this condition_variable object or
+   - lock.mutex() returns the same value for each of the lock arguments supplied by all concurrently waiting (via wait, wait_for, or wait_until) threads.

Effects: Equivalent to:

```
while (!pred())
    if (wait_until(lock, abs_time) == cv_status::timeout)
        return pred();
return true;
```

Remarks: If the function fails to meet the postcondition, terminate() is called (14.6.2).

> [Note 6: This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread.

> [Note 7: The returned value indicates whether the predicate evaluated to true regardless of whether the timeout was triggered. — end note]

Throws: Timeout-related exceptions (32.2.4) or any exception thrown by pred.

```
template<class Rep, class Period, class Predicate>
    bool wait_for(unique_lock<mutex>& lock,
                 const chrono::duration<Rep, Period>& rel_time,
                 Predicate pred);
```

Preconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread, and either

+   - no other thread is waiting on this condition_variable object or
+   - lock.mutex() returns the same value for each of the lock arguments supplied by all concurrently waiting (via wait, wait_for, or wait_until) threads.

Effects: Equivalent to:

```
return wait_until(lock, chrono::steady_clock::now() + rel_time, std::move(pred));
```

> [Note 8: There is no blocking if pred() is initially true, even if the timeout has already expired. — end note]

Remarks: If the function fails to meet the postcondition, terminate() is called (14.6.2).

> [Note 9: This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread.