
two threads are simultaneously trying to update an account. Suppose two threads simultaneously carry out the instruction

```c
accounts[to] += amount;
```

The problem is that these are not atomic operations. The instruction might be processed as follows:

- 1. Load `accounts[to]` into a register.
- 2. Add amount.
- 3. Move the result back to `accounts[to]`.

Now, suppose the first thread executes Steps 1 and 2, and then it is preempted. Suppose the second thread awakens and updates the same entry in the account array. Then, the first thread awakens and completes its Step 3.

That action wipes out the modification of the other thread. As a result, the total is no longer correct (see Figure 12.2).

![](img/127bccebb2cfadea3f02579edaad63c3_779_0.png)

**Figure 12.2**  Simultaneous access by two threads

Our test program detects this corruption. (Of course, there is a slight chance of false alarms if the thread is interrupted as it is performing the tests!)

> **NOTE:** You can actually peek at the virtual machine bytecodes that execute each statement in your class. Run the command
>
> ```
> javap -c -v Bank
> ```
>
> to decompile the Bank.class file. For example, the line
>
> ```
> accounts[to] += amount;
> ```
>
> is translated into the following bytecodes:
>
> ```
> aload_0
> getfield        #2; //Field accounts:[D
> iload_2
> dup2
> daload
> dload_3
> dadd
> dastore
> ```
>
> What these codes mean does not matter. The point is that the increment command is made up of several instructions, and the thread executing them can be interrupted at any instruction.

What is the chance of this corruption occurring? On a modern processor with multiple cores, the risk of corruption is quite high. We boosted the chance of observing the problem on a single-core processor by interleaving the print statements with the statements that update the balance.

If you omit the print statements, the risk of corruption is lower because each thread does so little work before going to sleep again, and it is unlikely that the scheduler will preempt it in the middle of the computation. However, the risk of corruption does not go away completely. If you run lots of threads on a heavily loaded machine, the program will still fail even after you have eliminated the print statements. The failure may take a few minutes or hours or days to occur. Frankly, there are few things worse in the life of a programmer than an error that only manifests itself irregularly.

The real problem is that the work of the transfer method can be interrupted in the middle. If we could ensure that the method runs to completion before the thread loses control, the state of the bank account object would never be corrupted.

## 12.4.3 Lock Objects

There are two mechanisms for protecting a code block from concurrent access. The Java language provides a synchronized keyword for this purpose, and Java 5 introduced the ReentrantLock class. The synchronized keyword automatically provides a lock as well as an associated “condition,” which makes it powerful and convenient for most cases that require explicit locking. However, we believe that it is easier to understand the synchronized keyword after you have seen locks and conditions in isolation. The java.util.concurrent framework provides separate classes for these fundamental mechanisms, which we explain here and in Section 12.4.4, “Condition Objects,” on p. 758. Once you have understood those building blocks, we present the synchronized keyword in Section 12.4.5, “The synchronized Keyword,” on p. 764.

The basic outline for protecting a code block with a ReentrantLock is:

```java
myLock.lock(); // a ReentrantLock object
try
{
    critical section
}
finally
{
    myLock.unlock(); // make sure the lock is unlocked even if an exception is thrown
}
```

This construct guarantees that only one thread at a time can enter the critical section. As soon as one thread locks the lock object, no other thread can get past the lock statement. When other threads call lock, they are deactivated until the first thread unlocks the lock object.

> **CAUTION:** It is critically important that the unlock operation is enclosed in a finally clause. If the code in the critical section throws an exception, the lock must be unlocked. Otherwise, the other threads will be blocked forever.

> **NOTE:** When you use locks, you cannot use the try-with-resources statement. First off, the unlock method isn’t called close. But even if it was renamed, the try-with-resources statement wouldn’t work. Its header expects the declaration of a new variable. But when you use a lock, you want to keep using the same variable that is shared among threads.

Let us use a lock to protect the `transfer` method of the `Bank` class.

```java
public class Bank
{
    private Lock bankLock = new ReentrantLock();

    public void transfer(int from, int to, int amount)
    {
        bankLock.lock();
        try
        {
            System.out.print(Thread.currentThread());
            accounts[from] -= amount;
            System.out.printf(" %10.2f from %d to %d", amount, from, to);
            accounts[to] += amount;
            System.out.printf(" Total Balance: %10.2f%n", getTotalBalance());
        }
        finally
        {
            bankLock.unlock();
        }
    }
}
```

Suppose one thread calls `transfer` and gets preempted before it is done. Suppose a second thread also calls `transfer`. The second thread cannot acquire the lock and is blocked in the call to the `lock` method. It is deactivated and must wait for the first thread to finish executing the `transfer` method. When the first thread unlocks the lock, then the second thread can proceed (see Figure 12.3).

Try it out. Add the locking code to the `transfer` method and run the program again. You can run it forever, and the bank balance will not become corrupted.

Note that each `Bank` object has its own `ReentrantLock` object. If two threads try to access the same `Bank` object, then the lock serves to serialize the access. However, if two threads access different `Bank` objects, each thread acquires a different lock and neither thread is blocked. This is as it should be, because the threads cannot interfere with one another when they manipulate different `Bank` instances.

The lock is called *reentrant* because a thread can repeatedly acquire a lock that it already owns. The lock has a *hold count* that keeps track of the nested calls to the `lock` method. The thread has to call `unlock` for every call to `lock` in order to relinquish the lock. Because of this feature, code protected by a lock can call another method that uses the same locks.

![](img/127bccebb2cfadea3f02579edaad63c3_783_0.png)

**Figure 12.3**  Comparison of unsynchronized and synchronized threads

For example, the `transfer` method calls the `getTotalBalance` method, which also locks the `bankLock` object, which now has a hold count of 2. When the `getTotalBalance` method exits, the hold count is back to 1. When the `transfer` method exits, the hold count is 0, and the thread relinquishes the lock.

In general, you will want to protect blocks of code that update or inspect a shared object, so you can be assured that these operations run to completion before another thread can use the same object.

> **CAUTION:** Be careful to ensure that the code in a critical section is not bypassed by throwing an exception. If an exception is thrown before the end of the section, the `finally` clause will relinquish the lock, but the object may be in a damaged state.

| `java.util.concurrent.locks.Lock` |
|---|
| • `void lock()`<br>acquires this lock; blocks if the lock is currently owned by another thread.<br><br>• `void unlock()`<br>releases this lock. |

| `java.util.concurrent.locks.ReentrantLock` |
|---|
| • `ReentrantLock()`<br>constructs a reentrant lock that can be used to protect a critical section.<br><br>• `ReentrantLock(boolean fair)`<br>constructs a lock with the given fairness policy. A fair lock favors the thread that has been waiting for the longest time. However, this fairness guarantee can be a significant drag on performance. Therefore, by default, locks are not required to be fair. |

> **CAUTION:** It sounds nice to be fair, but fair locks are *a lot slower* than regular locks. You should only enable fair locking if you truly know what you are doing and have a specific reason to consider fairness essential for your program. Even if you use a fair lock, you have no guarantee that the thread scheduler is fair. If the thread scheduler chooses to neglect a thread that has been waiting a long time for the lock, it doesn’t get the chance to be treated fairly by the lock.

## 12.4.4 Condition Objects

Often, a thread enters a critical section only to discover that it can’t proceed until a condition is fulfilled. Use a *condition object* to manage threads that have acquired a lock but cannot do useful work. In this section, we introduce the implementation of condition objects in the Java library. (For historical reasons, condition objects are often called *condition variables*.)

Let us refine our simulation of the bank. We do not want to transfer money out of an account that does not have the funds to cover the transfer. Note that we cannot use code like

```
if (bank.getBalance(from) >= amount)
    bank.transfer(from, to, amount);
```

It is entirely possible that the current thread will be deactivated between the successful outcome of the test and the call to transfer.
