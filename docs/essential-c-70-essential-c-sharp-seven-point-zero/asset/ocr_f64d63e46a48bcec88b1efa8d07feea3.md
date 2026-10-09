# **BEGINNER TOPIC**

# **Threading Problems**

We’ve said several times that writing multithreaded programs is complex and difficult, but we have not said why. In a nutshell, the problem is that many of our reasonable assumptions that are true of single-threaded programs are violated in multithreaded programs. The issues include a lack of atomicity, race conditions, complex memory models, and deadlocks.

# **Most Operations Are Not Atomic**

An atomic operation is one that always is observed to be either not started or already completed. Its state is never externally visible as “in progress.” Consider, for example, this code fragment:

```
if (bankAccounts.Checking.Balance >= 1000.00m)
{
bankAccounts.Checking.Balance -= 1000.00m;
bankAccounts.Savings.Balance += 1000.00m;
}
```

This operation—checking for available funds and then conditionally debiting one account and crediting another—needs to be atomic. In other words, for it to execute correctly, we must ensure that there is never a moment when the operation can be observed to be partially completed. Imagine, for example, that two threads are running on this code concurrently. It is possible that both threads verify that there are sufficient funds in the account, and then both threads do a transfer of funds, even if there are only sufficient funds in the account to do the transfer once. And, in fact, the situation is considerably worse: There are *no* operations in this code fragment that are atomic! Even operations like compound addition/subtraction or reading and writing a property of decimal type are nonatomic operations in C#. As such, they can all be observed to be “partially complete” in multithreaded scenarios—only partially incremented or decremented. The observation of inconsistent state due to partially completed nonatomic operations is a special case of a more general problem, called a **race condition**.

# **Uncertainty Caused by Race Conditions**

As we discussed earlier, concurrency is often simulated by time slicing. In the absence of special thread synchronization (which we discuss in detail the next chapter), the operating system can switch contexts between any two threads at any time of its choosing. As a consequence, when two