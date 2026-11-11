```
```java
bankLock.unlock();
}
}

/**
 * Gets the sum of all account balances.
 * @return the total balance
 */
public double getTotalBalance()
{
    bankLock.lock();
    try
    {
        double sum = 0;

        for (double a : accounts)
            sum += a;

        return sum;
    }
    finally
    {
        bankLock.unlock();
    }
}

/**
 * Gets the number of accounts in the bank.
 * @return the number of accounts
 */
public int size()
{
    return accounts.length;
}
```
```