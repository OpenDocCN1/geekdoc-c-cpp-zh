# Polymorphism

You can overload a method in a base class with a method in the subclass. As simple as this process sounds, it introduces considerable capability, and with capability comes danger.

Here’s a thought experiment: Should you make the decision to call BankAccount.Withdraw() or SavingsAccount.Withdraw() at compile-time or at runtime?

To illustrate the difference, I change the previous HidingWithdrawal program in a seemingly innocuous way. I call this new version HidingWithdrawalPolymorphically. (I’ve streamlined the listing by leaving out the stuff that doesn’t change.) The new version is shown here:

![](bbox=[0.11, 0.44, 0.2, 0.55])

```
// HidingWithdrawalPolymorphically -- Hide the Withdraw() method in the base
// class with a method in the subclass of the same name.
public class Program
{
    public static void MakeAWithdrawal(BankAccount ba, decimal amount)
    {
        ba.Withdraw(amount);
    }
    public static void Main(string[] args)
    {
        BankAccount ba;
        SavingsAccount sa;

        // Create a bank account, withdraw $100, and
        // display the results.
        ba = new BankAccount(200M);
        MakeAWithdrawal(ba, 100M);

        // Try the same trick with a savings account.
        sa = new SavingsAccount(200M, 12);
        MakeAWithdrawal(sa, 100M);

        // Display the resulting balance.
        Console.WriteLine("When invoked through intermediary:");
        Console.WriteLine("BankAccount balance is {0:C}", ba.Balance);
        Console.WriteLine("SavingsAccount balance is {0:C}", sa.Balance);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

The following output from this program may or may not be confusing, depending on what you expected:

```
When invoked through intermediary
BankAccount balance is $100.00
```