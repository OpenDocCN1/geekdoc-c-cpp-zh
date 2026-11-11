# 12.4 Synchronization

In most practical multithreaded applications, two or more threads need to share access to the same data. What happens if two threads have access to the same object and each calls a method that modifies the state of the object? As you might imagine, the threads can step on each other’s toes. Depending on the order in which the data are accessed, corrupted objects can result. Such a situation is often called a *race condition*.

# 12.4.1 An Example of a Race Condition

To avoid corruption of shared data by multiple threads, you must learn how to *synchronize the access*. In this section, you’ll see what happens if you do not use synchronization. In the next section, you’ll see how to synchronize data access.

In the next test program, we continue working with our simulated bank. Unlike the example in Section 12.1, “What Are Threads?,” on p. 734, we randomly select the source and destination of the transfer. Since this will cause problems, let us look more carefully at the code for the transfer method of the Bank class.

```
```java
public void transfer(int from, int to, double amount)
    // CAUTION: unsafe when called from multiple threads
{
    System.out.print(Thread.currentThread());
    accounts[from] -= amount;
    System.out.printf(" %10.2f from %d to %d", amount, from, to);
    accounts[to] += amount;
    System.out.printf(" Total Balance: %10.2f%n", getTotalBalance());
}
```
```

Here is the code for the Runnable instances. The run method keeps moving money out of a given bank account. In each iteration, the run method picks a random target account and a random amount, calls transfer on the bank object, and then sleeps.

```
```java
Runnable r = () -> {
    try
    {
        while (true)
        {
            int toAccount = (int) (bank.size() * Math.random());
            double amount = MAX_AMOUNT * Math.random();
            bank.transfer(fromAccount, toAccount, amount);
            Thread.sleep((int) (DELAY * Math.random()));
        }
    }
}
```
```