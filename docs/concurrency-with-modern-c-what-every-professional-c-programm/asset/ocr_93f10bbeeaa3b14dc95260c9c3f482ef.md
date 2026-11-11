# 2.3.4 All Atomic Operations

First, here is the list of all operations on atomics.

All operations on atomic

| Member functions | Description |
|---|---|
| test_and_set | Atomically set the flag to true and returns the previous value. |
| clear | Atomically sets the flag to false. |
| is_lock_free<br>atomic_ref<T>::is_always_lock_free | Checks if the atomic object is lock-free.<br>Checks at compile time if the atomic type is always lock-free. |
| load<br>operator T | Atomically returns the value of the atomic.<br>Atomically returns the value of the atomic. Equivalent to atomic.load(). |
| store | Atomically replaces the value of the atomic with a non-atomic. |
| exchange | Atomically replaces the value with the new value. Returns the old value. |
| compare_exchange_strong<br>compare_exchange_weak | Atomically compares and eventually exchanges the value. Details are here. |
| fetch_add, +=<br>fetch_sub, -= | Atomically adds (subtracts) the value.<br>Returns the old value. |
| fetch_or, |=<br>fetch_and, &=<br>fetch_xor, ^= | Atomically performs bitwise (AND, OR, and XOR) operation with the value.<br>Returns the old value. |
| ++, -- | Increments or decrements (pre- and post-increment) the atomic. |
| notify_one (C++20)<br>notify_all (C++20) | Notifies one atomic wait operation.<br>Notifies all atomic wait operations. |
| wait (C++20) | Blocks until it is notified.<br>Compares itself with the old value to protect against spurious wakeups and lost wakeups.<br>If the old value compares to unequal, returns. |

The atomic types have no copy constructor or copy assignment operator, but they support an assignment from an implicit conversion to the underlying built-in type. The composite assignment operators return the new value; the fetch variations return the old value. The composite assignment operators return values and not references to the assigned object.