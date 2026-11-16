# HOW'D YOU DO?

Here's one way to fix the class declaration to make it safe. You might have done things a little differently, and that's fine, as long as you gave the class itself, and not the calling program, control over how and when the AccountBalance gets changed.

```
class FinancialDetails
{
    public String BankName {get; set;}
    public String AccountNumber {get; set;}
    public Decimal AccountBalance {get; set;}
}
```

> Would you REALLY let just anybody change the balance in your bank account? I certainly wouldn't.

In the next section, we'll learn some better options for making these public, too.

By requiring that changes to the account balance be made through functions, you can control what 'happens.'

```
class FinancialDetails
{
    public String BankName {get; set;}
    public String AccountNumber {get; set;}
    public Decimal AccountBalance {get;}

    public MakeDeposit(Decimal amount)
    {
        ...
    }

    public WithdrawCash(Decimal amount)
    {
        ...
    }
}
```

> At the very least, you'll need to make AccountBalance read-only.