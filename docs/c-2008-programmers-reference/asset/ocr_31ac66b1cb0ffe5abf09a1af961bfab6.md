> In general, it is best to avoid using a public object for locking purposes. This prevents situations in which threads are all waiting for a public object, which may itself be locked by some other code.

To delineate a block of code to lock, enclose the statements with the lock statement:

```
lock (obj)
{
    //---place code here---
}
```

As long as one thread is executing the statements within the block, all other threads will have to wait for the statements to be completed before they can execute the statements.

Figure 10-6 shows one possible outcome of the execution.

![](bbox=[0.28, 0.55, 0.86, 0.74])

Figure 10-6

Notice that the value of balance is now consistent after each credit/debit operation.

# Monitor Class

The limitation of the lock statement is that you do not have the capability to release the lock halfway through the critical section. This is important because there are situations in which one thread needs to release the lock so that other threads have a chance to proceed before the first thread can resume its execution.

For instance, you saw in Figure 10-6 that on the fifth line the balance goes into a negative value. In real life this might not be acceptable. The bank might not allow your account to go into a negative balance, and thus you need to ensure that you have a positive balance before any more debiting can proceed. Hence, you need to check the value of balance. If it is 0, then you should release the lock and let the crediting thread have a chance to increment the balance before you do any more debiting.