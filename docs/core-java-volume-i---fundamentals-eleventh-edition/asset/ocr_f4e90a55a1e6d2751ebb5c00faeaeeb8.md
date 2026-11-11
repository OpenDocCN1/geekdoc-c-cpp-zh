your loop calls sleep, don’t check the interrupted status. Instead, catch the InterruptedException, like this:

```
```java
Runnable r = () -> {
    try
    {
        ...
        while (more work to do)
        {
            do more work
            Thread.sleep(delay);
        }
    }
    catch (InterruptedException e)
    {
        // thread was interrupted during sleep
    }
    finally
    {
        cleanup, if required
    }
    // exiting the run method terminates the thread
};
```
```

> > **NOTE:** There are two very similar methods, `interrupted` and `isInterrupted`. The `interrupted` method is a static method that checks whether the *current* thread has been interrupted. Furthermore, calling the `interrupted` method *clears* the interrupted status of the thread. On the other hand, the `isInterrupted` method is an instance method that you can use to check whether any thread has been interrupted. Calling it does not change the interrupted status.

You’ll find lots of published code in which the InterruptedException is squelched at a low level, like this:

```
```java
void mySubTask()
{
    ...
    try { sleep(delay); }
    catch (InterruptedException e) { } // don't ignore!
    ...
}
```
```

Don’t do that! If you can’t think of anything good to do in the catch clause, you still have two reasonable choices:

+   - In the `catch` clause, call `Thread.currentThread().interrupt()` to set the interrupted status. Then the caller can test it.