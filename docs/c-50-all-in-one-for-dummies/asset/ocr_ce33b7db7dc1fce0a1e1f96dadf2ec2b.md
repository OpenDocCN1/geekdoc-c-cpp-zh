# 286 Inheriting from a BankAccount Class (A More Complex Example)

```
public decimal _interestRate;
// InitSavingsAccount -- Input the rate expressed as a
//   rate between 0 and 100.
public void InitSavingsAccount(decimal interestRate)
{
    InitSavingsAccount(0, interestRate);
}
public void InitSavingsAccount(decimal initialBalance, decimal interestRate)
{
    InitBankAccount(initialBalance);  // Note call to base class.
    this._interestRate = interestRate / 100;
}
// AccumulateInterest -- Invoke once per period.
public void AccumulateInterest()
{
    _balance = Balance + (decimal)(Balance * _interestRate);
}
// ToString -- Stringify the account.
public string ToSavingsAccountString()
{
    return String.Format("{0} ({1}%)",
        ToBankAccountString(), _interestRate * 100);
}
public class Program
{
    public static void Main(string[] args)
    {
        // Create a bank account and display it.
        BankAccount ba = new BankAccount();
        ba.InitBankAccount(100M);  // M suffix indicates decimal.
        ba.Deposit(100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // Now a savings account
        SavingsAccount sa = new SavingsAccount();
        sa.InitSavingsAccount(100M, 12.5M);
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

The BankAccount class is not unlike some that appear in other chapters of this book. It begins with an overloaded initialization method InitBankAccount(): one for accounts that start out with an initial balance and another for which an initial balance of zero will have to suffice. Notice that this version of BankAccount doesn’t take advantage of the latest and greatest constructor advances. If you read this entire chapter and see that I clean up this topic in the final version of BankAccount, you can then see why I chose to “drop back” a little here.

The Balance property allows other people to read the balance without letting them modify it. The Deposit() method accepts any positive deposit. Withdraw() lets you take out as much as you want, as long as you have