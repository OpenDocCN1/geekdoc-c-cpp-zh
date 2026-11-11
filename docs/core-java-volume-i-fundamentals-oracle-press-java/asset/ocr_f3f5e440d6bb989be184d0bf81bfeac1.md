Even if you use a fair lock, you have no guarantee that the thread scheduler is fair. If the thread scheduler chooses to neglect a thread that has been waiting a long time for the lock, it doesn’t get the chance to be treated fairly by the lock.

# 12.4.4 Condition Objects

Often, a thread enters a critical section only to discover that it can’t proceed until a condition is fulfilled. Use a *condition object* to manage threads that have acquired a lock but cannot do useful work. In this section, I introduce the implementation of condition objects in the Java library. (For historical reasons, condition objects are often called *condition variables*.)

Let us refine our simulation of the bank. We do not want to transfer money out of an account that does not have the funds to cover the transfer. Note that we cannot use code like

```
```java
if (bank.getBalance(from) >= amount)
    bank.transfer(from, to, amount);
```
```

It is entirely possible that the current thread will be deactivated between the successful outcome of the test and the call to `transfer`.

```
```java
if (bank.getBalance(from) >= amount)
    // thread might be deactivated at this point
    bank.transfer(from, to, amount);
```
```

By the time the thread is running again, the account balance may have fallen below the withdrawal amount. You must make sure that no other thread can modify the balance between the test and the transfer action. You do so by protecting both the test and the transfer action with a lock:

```
```java
public void transfer(int from, int to, int amount)
{
    bankLock.lock();
```
```