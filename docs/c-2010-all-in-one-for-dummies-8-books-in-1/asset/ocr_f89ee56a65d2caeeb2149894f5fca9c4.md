# #304 The Updated BankAccount Class

```
public static void void DirectDeposit(BankAccount ba, decimal pay)
{
    ba.Deposit(pay);
}
public static void Main(string[] args)
{
    // Create a bank account and display it.
    BankAccount ba = new BankAccount(100M);
    DirectDeposit(ba, 100M);
    Console.WriteLine("Account 0", ba.ToBankAccountString());
    // Now a savings account
    SavingsAccount sa = new SavingsAccount(12.5M);
    DirectDeposit(sa, 100M);
    sa.AccumulateInterest();
    Console.WriteLine("Account 0", sa.ToSavingsString());
    // Wait for user to acknowledge the results.
    Console.WriteLine("Press Enter to terminate...");
    Console.Read();
}
```

BankAccount defines two constructors: one that accepts an initial balance and the default constructor, which does not. To avoid duplicating code within the constructor, the default constructor invokes the BankAccount(initial balance) constructor using the this keyword.

The SavingsAccount class also provides two constructors. The SavingsAccount(interest rate) constructor invokes the SavingsAccount(interest rate, initial balance) constructor, passing an initial balance of 0. This most general constructor passes the initial balance to the BankAccount(initial balance) constructor using the base keyword, as shown in Figure 6-1.

| Figure 6-1: Bank Account (0) | |
| The path for constructing an object using the default constructor. | passes balance to base class |
| Savings Account (12.5%), 0) | defaults to 0 |
| Savings Account (12.5%) | |