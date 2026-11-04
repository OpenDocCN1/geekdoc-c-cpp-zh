```
lock (obj)
{
    balance -= 100;
    Console.WriteLine("After debiting, balance is {0}", balance);
}
```

Is equivalent to this Monitor class usage:

```
Monitor.Enter(obj);
try
{
    balance -= 100;
    Console.WriteLine("After debiting, balance is {0}", balance);
}
finally
{
    Monitor.Exit(obj);
}
```

Now the code looks promising, but the debiting could still result in a negative balance. To resolve this, you need to so some checking to ensure that the debiting does not proceed until there is a positive balance. Here's how:

```
static void Debit()
{
    //==debit 1000==
    for (int i = 0; i < 10; i++)
    {
        Monitor.Enter(obj);
        if (balance == 0)
            Monitor.Wait(obj);
        balance -= 100;
        Console.WriteLine("After debiting, balance is {0}", balance);
        Monitor.Exit(obj);
    }
}
```

When you use the Wait() method of the Monitor class, you release the lock on the object and enter the object's waiting queue. The next thread that is waiting for the object acquires the lock. If the balance is 0, the debit thread would give up control and let the credit thread have the lock.

However, this code modification may result in the scenario shown in Figure 10-7, in which after debiting the balance five times, balance becomes 0. On the sixth time, the lock held by the debit thread is released to the credit thread. The credit thread credits the balance 15 times. At that point, the program freezes. Turns out that the credit thread has finished execution, but the debit thread is still waiting for the lock to be explicitly returned to it.