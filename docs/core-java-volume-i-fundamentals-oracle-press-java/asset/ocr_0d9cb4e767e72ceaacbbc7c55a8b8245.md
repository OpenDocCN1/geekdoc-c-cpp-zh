```
```java
accounts[to] += amount;
System.out.printf(" Total Balance: %10.2f%n",
getTotalBalance());
}
```
```

Here is the code for the `Runnable` instances. The run method keeps moving money out of a given bank account. In each iteration, the run method picks a random target account and a random amount, calls transfer on the bank object, and then sleeps.

```
```java
Runnable r = () ->
{
    try
    {
        while (true)
        {
            int toAccount = (int) (bank.size() *
Math.random());
            double amount = MAX_AMOUNT * Math.random();
            bank.transfer(fromAccount, toAccount,
amount);        Thread.sleep((int) (DELAY *
Math.random()));
        }
    }
    catch (InterruptedException e)
    {
    }
};
```
```

When this simulation runs, we do not know how much money is in any one bank account at any time. But we do know that the total amount of money in all the accounts should remain unchanged because all we do is move money from one account to another.

At the end of each transaction, the `transfer` method recomputes the total and prints it.

This program never finishes. Just press Ctrl+C to kill the program.