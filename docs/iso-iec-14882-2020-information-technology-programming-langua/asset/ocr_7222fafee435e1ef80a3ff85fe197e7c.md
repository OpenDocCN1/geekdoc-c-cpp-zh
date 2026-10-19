# 32.5.5.5.4 Modifiers [thread.lock.shared.mod]

```
void unlock();
```

Effects: As if by pm->unlock_shared().

Postconditions: owns == false.

Throws: system_error when an exception is required (32.2.2).

Error conditions:

+   - operation_not_permitted — if on entry owns is false.

```
void swap(shared_lock& sl) noexcept;
```

Effects: Swaps the data members of *this and sl.

```
mutex_type* release() noexcept;
```

Returns: The previous value of pm.

Postconditions: pm == nullptr and owns == false.

```
template<class Mutex>
    void swap(shared_lock<Mutex>& x, shared_lock<Mutex>& y) noexcept;
```

Effects: As if by x.swap(y).

# 32.5.5.5.5 Observers [thread.lock.shared.obs]

```
bool owns_lock() const noexcept;
```

Returns: owns.

```
explicit operator bool() const noexcept;
```

Returns: owns.

```
mutex_type* mutex() const noexcept;
```

Returns: pm.

# 32.5.6 Generic locking algorithms [thread.lock.algorithm]

```
template<class L1, class L2, class... L3> int try_lock(L1&, L2&, L3&...);
```

Preconditions: Each template parameter type meets the Cpp17Lockable requirements.

[Note 1: The unique_lock class template meets these requirements when suitably instantiated. — end note]

Effects: Calls try_lock() for each argument in order beginning with the first until all arguments have been processed or a call to try_lock() fails, either by returning false or by throwing an exception. If a call to try_lock() fails, unlock() is called for all prior arguments with no further calls to try_lock().

Returns: -1 if all calls to try_lock() returned true, otherwise a zero-based index value that indicates the argument for which try_lock() returned false.

```
template<class L1, class L2, class... L3> void lock(L1&, L2&, L3&...);
```

Preconditions: Each template parameter type meets the Cpp17Lockable requirements.

[Note 2: The unique_lock class template meets these requirements when suitably instantiated. — end note]

Effects: All arguments are locked via a sequence of calls to lock(), try_lock(), or unlock() on each argument. The sequence of calls does not result in deadlock, but is otherwise unspecified.

[Note 3: A deadlock avoidance algorithm such as try-and-back-off can be used, but the specific algorithm is not specified to avoid over-constraining implementations. — end note]

If a call to lock() or try_lock() throws an exception, unlock() is called for any argument that had been locked by a call to lock() or try_lock().