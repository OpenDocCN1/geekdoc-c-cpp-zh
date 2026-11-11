| `java.util.concurrent.locks.Lock` |
|---|
| • `void lock()`<br>acquires this lock; blocks if the lock is currently owned by another thread.<br><br>• `void unlock()`<br>releases this lock. |

| `java.util.concurrent.locks.ReentrantLock` |
|---|
| • `ReentrantLock()`<br>constructs a reentrant lock that can be used to protect a critical section.<br><br>• `ReentrantLock(boolean fair)`<br>constructs a lock with the given fairness policy. A fair lock favors the thread that has been waiting for the longest time. However, this fairness guarantee can be a significant drag on performance. Therefore, by default, locks are not required to be fair. |

> **CAUTION:** It sounds nice to be fair, but fair locks are *a lot slower* than regular locks. You should only enable fair locking if you truly know what you are doing and have a specific reason to consider fairness essential for your program. Even if you use a fair lock, you have no guarantee that the thread scheduler is fair. If the thread scheduler chooses to neglect a thread that has been waiting a long time for the lock, it doesn’t get the chance to be treated fairly by the lock.

# 12.2.4 Condition Objects

Often, a thread enters a critical section only to discover that it can’t proceed until a condition is fulfilled. Use a *condition object* to manage threads that have acquired a lock but cannot do useful work. In this section, we introduce the implementation of condition objects in the Java library. (For historical reasons, condition objects are often called *condition variables*.)

Let us refine our simulation of the bank. We do not want to transfer money out of an account that does not have the funds to cover the transfer. Note that we cannot use the like

```
if (bank.getBalance(from) >= amount)
    bank.transfer(from, to, amount);
```

It is entirely possible that the current thread will be deactivated between the successful outcome of the test and the call to transfer.