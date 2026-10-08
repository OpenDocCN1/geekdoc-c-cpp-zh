# 268 Why You Should Worry about Access Control

![](bbox=[0.15, 0.125, 0.215, 0.195])

```
// DecimalBankAccount -- Create a bank account using a decimal
// Variable to store the account balance.
using System;
namespace DecimalBankAccount
{
    public class Program
    {
        public static void Main(string[] args)
        {
            // Open a bank account.
            Console.WriteLine("Create a bank account object");
            BankAccount ba = new BankAccount();
            ba.InitAccount();
            // Make a deposit.
            double deposit = 123.454;
            Console.WriteLine("Depositing {0:C}", deposit);
            ba.Deposit(deposit);
            // Account balance
            Console.WriteLine("Account: {0}", ba.GetBalance());
            // Now add a very small amount.
            double fractionalAddition = 0.002;
            Console.WriteLine("Adding {0:C}", fractionalAddition);
            ba.Deposit(fractionalAddition);
            // Resulting balance.
            Console.WriteLine("Resulting account {0}", ba.GetBalance());
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
}

// BankAccount -- Define a class that represents a simple account.
ublic class BankAccount
{
    private static int _nextAccountNumber = 1000;
    private int _accountNumber;
    // Maintain the balance as a single decimal variable.
    private decimal _balance;
    // Init -- Initialize a bank account with the next
    // account id and a balance of 0.
    public void InitBankAccount()
    {
        _accountNumber = ++_nextAccountNumber;
        _balance = 0;
    }

    // GetBalance -- Return the current balance.
    public double GetBalance()
    {
        return (double)_balance;
    }
    // AccountNumber
    public int GetAccountNumber()
    {
        return _accountNumber;
    }
    public void SetAccountNumber(int accountNumber)
    {
        this._accountNumber = accountNumber;
    }
    // Deposit -- Any positive deposit is allowed.
    public void Deposit(double amount)
    {
}
```