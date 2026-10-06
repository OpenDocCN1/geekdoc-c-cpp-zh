# ISO/IEC 14882:2017(E)

expiration of the absolute timeout (33.2.4) specified by abs_time, or spuriously.

+   If the function exits via an exception, lock.lock() shall be called prior to exiting the function.

Remarks: If the function fails to meet the postcondition, terminate() shall be called (18.5.1). [Note: This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock is locked by the calling thread.

Returns: cv_status::timeout if the absolute timeout (33.2.4) specified by abs_time expired, otherwise cv_status::no_timeout.

Timed-out exceptions (33.2.4).

```
template<Class Lock, Class Rep, Class Period>
cv_status wait_for(Lock& lock, const chrono::duration<Rep, Period>& rel_time);
    cv_status::no_timeout;
```

Equivalent to:

```
return wait_until(lock, chrono::steady_clock::now() + rel_time);
```

Returns: cv_status::timeout if the relative timeout (33.2.4) specified by rel_time expired, otherwise cv_status::no_timeout.

Remarks: If the function fails to meet the postcondition, terminate() shall be called (18.5.1). [Note: This can happen if the re-locking of the mutex throws an exception. — end note]

Postconditions: lock is locked by the calling thread.

Timed-out exceptions (33.2.4).

```
template<Class Lock, Class Clock, Class Duration, Predicate Pred>
bool wait_for(Lock& lock, const chrono::time_point<Clock, Duration>& abs_time, Predicate pred);
```

Equivalent to:

```
while (pred()) {
    if (wait_until(lock, abs_time) == cv_status::timeout)
        return pred();
}
return true;
```

> [Note: There is no blocking if pred() is initially true, or if the timeout has already expired. — end note]

> [Note: The return value indicates whether the predicate evaluates to true regardless of whether the timeout was triggered. — end note]

```
template<Class Lock, Class Rep, Class Period, Predicate Pred>
bool wait_for(Lock& lock, const chrono::duration<Rep, Period>& rel_time, Predicate pred);
```

Equivalent to:

```
return wait_until(lock, chrono::steady_clock::now() + rel_time, std::move(pred));
```

# 33.6 Futures

# 33.6.1 Overview

[futures.overview]

future describes how a C++ program can use future to retrieve a result (value or exception) from a function that has run in the same thread or another thread. [Note: These components are not restricted to multi-threaded programs but can be useful in single-threaded programs as well. — end note]

# 33.6.2 Header <future> synopsis

[future.syn]

```
namespace std {
    enum class future_errc
```

33.6.2

©ISO/IEC 2017 - All rights reserved

1391