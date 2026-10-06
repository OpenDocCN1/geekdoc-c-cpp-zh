# ISO/IEC 14882:2017(Class Period)

```
template <class Rep, class Period>
c_status wait_for(unique_lock<mutex> &lock,
const chrono::duration duration, Period&rel_time);
```

+   Requires: lock.owns_lock() is true and lock.mutex() is locked by the calling thread, and either
- no other thread is waiting on this condition_variable object
- lock.mutex() returns the same value for each of the lock arguments supplied by all concurrently
  waiting (via wait, wait_for, or wait_until) threads

Equivalent to:
return wait_until(lock, chrono::steady_clock::now() + rel_time);

Returns: cv_status=timeout if the value trux (32.2.4) specified by rel_time expired, otherwise
c_status=no_timeout.

> Remarks: If the function fails to meet the postcondition, terminate() shall be called (18.5.1). [Note:
This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread.
Throws: Timeout-related exceptions (32.2.4).

```
template <class Lock, class Duration, class Predicate>
bool wait_until(unique_lock<mutex> &lock,
const chrono::time_point time, Duration&abs_time,
Predicate pred);
```

+   Requires: lock.owns_lock() is true and lock.mutex() is locked by the calling thread, and either
- no other thread is waiting on this condition_variable object
- lock.mutex() returns the same value for each of the lock arguments supplied by all concurrently
  waiting (via wait, wait_for, or wait_until) threads

Equivalent to:

```
while (!pred())
  if (wait_until(lock, abs_time) == cv_status::timeout)
    return false;
return true;
```

> Remarks: If the function fails to meet the postcondition, terminate() shall be called (18.5.1). [Note:
This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock.owns_lock() is true and lock.mutex() is locked by the calling thread.
[Note: The return value indicates whether the predicate evaluated to true regardless of whether the
time was triggered. — end note]

Throws: Timeout-related exceptions (32.2.4) or any exception thrown by pred.

```
template <class Rep, class Period, class Predicate>
bool wait_for(unique_lock<mutex> &lock,
const chrono::duration duration, Period&rel_time,
Predicate pred);
```

+   Requires: lock.owns_lock() is true and lock.mutex() is locked by the calling thread, and either
- no other thread is waiting on this condition_variable object
- lock.mutex() returns the same value for each of the lock arguments supplied by all concurrently
  waiting (via wait, wait_for, or wait_until) threads

33.5.3

©ISO/IEC 2017 - All rights reserved