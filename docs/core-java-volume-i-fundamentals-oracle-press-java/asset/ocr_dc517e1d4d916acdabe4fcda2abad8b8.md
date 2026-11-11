```
```java
/**
 * Constructs the bank.
 * @param n the number of accounts
 * @param initialBalance the initial balance for each
account
 */
public Bank(int n, double initialBalance)
{
    accounts = new double[n];
    Arrays.fill(accounts, initialBalance);
    bankLock = new ReentrantLock();
    sufficientFunds = bankLock.newCondition();
}

/**
 * Transfers money from one account to another.
 * @param from the account to transfer from
 * @param to the account to transfer to
 * @param amount the amount to transfer
 */
public void transfer(int from, int to, double amount)
throws InterruptedException
{
    bankLock.lock();
    try
    {
        while (accounts[from] < amount)
            sufficientFunds.await();
        System.out.print(Thread.currentThread());
        accounts[from] -= amount;
        System.out.printf(" %10.2f from %d to %d", amount,
        from, to);
        accounts[to] += amount;
        System.out.printf(" Total Balance: %10.2f%n",
        getTotalBalance());
        sufficientFunds.signalAll();
    }
    finally
    {
```
```