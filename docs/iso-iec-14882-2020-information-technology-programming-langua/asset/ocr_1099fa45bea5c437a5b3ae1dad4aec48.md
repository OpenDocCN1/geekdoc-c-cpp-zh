(4.3) — invalid_argument — if any native handle type manipulated as part of mutex construction is incorrect.

5 The implementation provides lock and unlock operations, as described below. For purposes of determining the existence of a data race, these behave as atomic operations (6.9.2). The lock and unlock operations on a single mutex appears to occur in a single total order.

> [Note 1: This can be viewed as the modification order (6.9.2) of the mutex. — end note]

> [Note 2: Construction and destruction of an object of a mutex type need not be thread-safe; other synchronization can be used to ensure that mutex objects are initialized and visible to other threads. — end note]

6 The expression m.lock() is well-formed and has the following semantics:

Preconditions: If m is of type mutex, timed_mutex, shared_mutex, or shared_timed_mutex, the calling thread does not own the mutex.

Effects: Blocks the calling thread until ownership of the mutex can be obtained for the calling thread.

Postconditions: The calling thread owns the mutex.

Return type: void.

Synchronization: Prior unlock() operations on the same object synchronize with (6.9.2) this operation.

Throws: system_error when an exception is required (32.2.2).

Error conditions:

+   — operation_not_permitted — if the thread does not have the privilege to perform the operation.

+   — resource_deadlock_would_occur — if the implementation detects that a deadlock would occur.

14 The expression m.try_lock() is well-formed and has the following semantics:

Preconditions: If m is of type mutex, timed_mutex, shared_mutex, or shared_timed_mutex, the calling thread does not own the mutex.

Effects: Attempts to obtain ownership of the mutex for the calling thread without blocking. If ownership is not obtained, there is no effect and try_lock() immediately returns. An implementation may fail to obtain the lock even if it is not held by any other thread.

> [Note 3: This spurious failure is normally uncommon, but allows interesting implementations based on a simple compare and exchange (Clause 31). — end note]

An implementation should ensure that try_lock() does not consistently return false in the absence of contending mutex acquisitions.

Return type: bool.

Returns: true if ownership of the mutex was obtained for the calling thread, otherwise false.

Synchronization: If try_lock() returns true, prior unlock() operations on the same object synchronize with (6.9.2) this operation.

> [Note 4: Since lock() does not synchronize with a failed subsequent try_lock(), the visibility rules are weak enough that little would be known about the state after a failure, even in the absence of spurious failures. — end note]

Throws: Nothing.

21 The expression m.unlock() is well-formed and has the following semantics:

Preconditions: The calling thread owns the mutex.

Effects: Releases the calling thread's ownership of the mutex.

Return type: void.

Synchronization: This operation synchronizes with (6.9.2) subsequent lock operations that obtain ownership on the same object.

Throws: Nothing.

# 32.5.4.2.2 Class mutex [thread.mutex.class]

```
namespace std {
  class mutex {
  public:
    constexpr mutex() noexcept;
```