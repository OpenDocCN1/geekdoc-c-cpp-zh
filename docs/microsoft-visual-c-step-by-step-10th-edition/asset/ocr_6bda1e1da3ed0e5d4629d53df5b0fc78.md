C# includes pattern-matching capabilities that can take advantage of property values in a type. For example, suppose you're modeling bank accounts in an application. You define the following interface:

Click here to view code image

```
interface IBankAccount
{
    decimal Balance { get; }
    decimal OverdraftLimit { get; }
    void Deposit(decimal amount);
    decimal Withdraw(decimal amount);
}
```

You implement several types of bank accounts, each with varying limitations and interest rates:

Click here to view code image

```
class CurrentAccount : IBankAccount
{
    // Implementation details not shown
    ...
}
class DepositAccount : IBankAccount
{
    // Implementation details not shown
}
class HighInterestSavingsAccount : IBankAccount
{
    // Implementation details not shown
    ...
}
```

You want to write a method that calculates the interest receivable for any of these types of account. The amount of interest paid depends on the balance and the type of account. The switch statement enables you to perfrom a complex set of rules quickly and easily, based on pattern-matching capabilities that enable you to determine the type of an object and the values of its properties. The following code shows the `CalculateInterest` method:

Click here to view code image