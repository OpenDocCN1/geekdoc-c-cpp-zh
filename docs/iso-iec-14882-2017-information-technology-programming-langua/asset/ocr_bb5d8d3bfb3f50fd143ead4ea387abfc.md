# ISO/IEC 14882:2017(E)

(4.1) — resource_unavailable_try_again — if some non-memory resource limitation prevents initialization-

(4.2) — operation_not_permitted — if the thread does not have the privilege to perform the operation.

-condition_variable_anyOf();

5 Requires: There shall be no block on *this. [Note: That is, all threads shall have been notified; they may subsequently block on the lock specified in the wait. This relaxes the usual rule, which would require all calls to wait before destruction. Only the notification to unlock the wait needs to happen before destruction. The user should take care to ensure that no wait functions once the destructor has been started, especially when the waiting threads are calling the wait functions in a loop or overloads of wait, wait_for, or wait_until that take a predicate, — end note]

6 Effects: Destroys the object.

```
void notify_one(noexcept);
```

7 Effects: If any threads are blocked waiting for *this, unblocks one of those threads.

```
void notify_all(noexcept);
```

8 Effects: Unblocks all threads that are blocked waiting for *this.

```
template <class Lock>
void wait(Lock& lock);
```

9 [Note: If the wait function exits via an exception, it is unspecified whether the Lock is held. One can use a Lock type to query that, such as the unique_lock wrapper. — end note]

10:

+   — Atomically calls lock.unlock() and on *this.

+   — When unblocked, calls lock.lock() (possibly blocking on the lock) and returns.

+   — The function will unblock when signaled by a call to notify_one(), a call to notify_all(), or spuriously.

11 Remarks: If the function fails to meet the postcondition, terminate() shall be called (18.5.1). [Note: This can happen if the re-locking of the mutex throws an exception. — end note]

12

Postconditions: lock is locked by the calling thread.

13

```
template <class Lock, class Predicate>
void wait(Lock& lock, Predicate pred);
```

14 Equivalent to:

```
while (!pred())
wait(lock);
```

```
template <class Lock, class Clock, class Duration>
cv_status wait_until(Lock& lock, const chrono::time_point<Clock, Duration>& abs_time);
```

15 Effects:

+   — Atomically calls lock.unlock() and on *this.

+   — When unblocked, calls lock.lock() (possibly blocking on the lock) and returns.

+   — The function will unblock when signaled by a call to notify_one(), or a call to notify_all().