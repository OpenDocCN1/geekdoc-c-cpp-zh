Here is a first attempt:

```
```cpp
void withdraw(double balance, double amount) // Does not work
{
    const double PENALTY = 10;
    if (balance >= amount)
    {
        balance = balance - amount;
    }
    else
    {
        balance = balance - PENALTY;
    }
}
```
```

But this doesn't work.

Let's walk through the function call withdraw(harrys_account, 100)—see Figure 6. As the function starts, the parameter variable balance is created ❶ and set to the same value as harrys_account, and amount is set to 100 ❷. Then balance is modified ❸. Of course, that modification has no effect on harrys_account, because balance is a separate variable. When the function returns, balance is forgotten, and no money was withdrawn from harrys_account ❹.

![](bbox=[0.346, 0.43, 0.852, 0.847])

**Figure 6** When balance and account are Value Parameters