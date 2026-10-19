Returns: The value returned by the call to try_lock().

Postconditions: owns == res, where res is the value returned by the call to try_lock().

Throws: Any exception thrown by pm->try_lock(). system_error when an exception is required (32.2.2).

Error conditions:

+   — operation_not_permitted — if pm is nullptr.

+   — resource_deadlock_would_occur — if on entry owns is true.

```
template<class Clock, class Duration>
bool try_lock_until(const chrono::time_point<Clock, Duration>& abs_time);
```

Preconditions: The supplied Mutex type meets the Cpp17TimedLockable requirements (32.2.5.4).

Effects: As if by pm->try_lock_until(abs_time).

Returns: The value returned by the call to try_lock_until(abs_time).

Postconditions: owns == res, where res is the value returned by the call to try_lock_until(abs_time).

Throws: Any exception thrown by pm->try_lock_until(). system_error when an exception is required (32.2.2).

Error conditions:

+   — operation_not_permitted — if pm is nullptr.

+   — resource_deadlock_would_occur — if on entry owns is true.

```
template<class Rep, class Period>
bool try_lock_for(const chrono::duration<Rep, Period>& rel_time);
```

Preconditions: The supplied Mutex type meets the Cpp17TimedLockable requirements (32.2.5.4).

Effects: As if by pm->try_lock_for(rel_time).

Returns: The value returned by the call to try_lock_for(rel_time).

Postconditions: owns == res, where res is the value returned by the call to try_lock_for(rel_time).

Throws: Any exception thrown by pm->try_lock_for(). system_error when an exception is required (32.2.2).

Error conditions:

+   — operation_not_permitted — if pm is nullptr.

+   — resource_deadlock_would_occur — if on entry owns is true.

```
void unlock();
```

Effects: As if by pm->unlock().

Postconditions: owns == false.

Throws: system_error when an exception is required (32.2.2).

Error conditions:

+   — operation_not_permitted — if on entry owns is false.

# 32.5.5.4.4 Modifiers [thread.lock.unique.mod]

```
void swap(unique_lock& u) noexcept;
```

Effects: Swaps the data members of *this and u.

```
mutex_type* release() noexcept;
```

Returns: The previous value of pm.

Postconditions: pm == 0 and owns == false.