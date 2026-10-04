
```cs
}
}
public class SubClass : BaseClass
{
    public SubClass()
    {
        Console.WriteLine("Constructing SubClass (default)");
    }
    public SubClass(int i1, int i2) : base(i1)
    {
        Console.WriteLine("Constructing SubClass({0}, {1})", i1, i2);
    }
}
public class Program
{
    public static void Main(string[] args)
    {
        Console.WriteLine("Invoking SubClass()");
        SubClass sc1 = new SubClass();

        Console.WriteLine("\nInvoking SubClass(1, 2)");
        SubClass sc2 = new SubClass(1, 2);

        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

The output from this program is

```
Invoking SubClass()
Constructing BaseClass (default)
Constructing SubClass (default)

Invoking SubClass(1, 2)
Constructing BaseClass(1)
Constructing SubClass(1, 2)
Press Enter to terminate...
```

This version begins the same as the previous examples, by creating a default SubClass object using the default constructor of both BaseClass and SubClass.

The second object is created with the expression new SubClass(1, 2). C# invokes the SubClass(int, int) constructor, which uses the base keyword to pass one of the values to the BaseClass(int) constructor. SubClass passes the first argument to the base class for processing and then uses the second value itself.

# The Updated BankAccount Class

The program ConstructorSavingsAccount, found on the website, is an updated version of the SimpleBankAccount program. In this version, however, the SavingsAccount constructor can pass information back to the BankAccount constructors. Only Main() and the constructors themselves are shown here:

![](img/6df7bb88e9302e98442acc219cfbd7fc_324_0.png)

```cs
// ConstructorSavingsAccount -- Implement a SavingsAccount as
//   a form of BankAccount; use no virtual methods, but
//   implement the constructors properly.
using System;
namespace ConstructorSavingsAccount
{
    // BankAccount -- Simulate a bank account, each of which carries an
    //   account ID (which is assigned upon creation) and a balance.
    public class BankAccount
    {
        // Bank accounts start at 1000 and increase sequentially.
        public static int _nextAccountNumber = 1000;
        // Maintain the account number and balance for each object.
        public int _accountNumber;
        public decimal _balance;
        // Constructors
        public BankAccount() : this(0)
        {
        }
        public BankAccount(decimal initialBalance)
        {
            _accountNumber = ++_nextAccountNumber;
            _balance = initialBalance;
        }
        public decimal Balance
        {
            get { return _balance; }
            // Protected setter lets subclass use Balance property to set.
            protected set { _balance = value; }
        }
        // Deposit -- Any positive deposit is allowed.
        public void Deposit(decimal amount)
        {
            if (amount > 0)
            {
                Balance += amount;
            }
        }
        // Withdraw -- You can withdraw any amount up to the
        //   balance; return the amount withdrawn.
        public decimal Withdraw(decimal withdrawal)
        {
            if (Balance <= withdrawal)
            {
                withdrawal = Balance;
            }
            Balance -= withdrawal;
            return withdrawal;
        }
        // ToString -- Stringify the account.
        public string ToBankAccountString()
        {
            return String.Format("{0} - {1:C}",
                _accountNumber, Balance);
        }
    }
    // SavingsAccount -- A bank account that draws interest
public class SavingsAccount : BankAccount
{
    public decimal _interestRate;
    // InitSavingsAccount -- Input the rate expressed as a
    //   rate between 0 and 100.
    public SavingsAccount(decimal interestRate) : this(interestRate, 0) { }
    public SavingsAccount(decimal interestRate, decimal initial) : base(initial)
    {
        this._interestRate = interestRate / 100;
    }
    // AccumulateInterest -- Invoke once per period.
    public void AccumulateInterest()
    {
        // Use protected setter and public getter via Balance property.
        Balance = Balance + (decimal)(Balance * _interestRate);
    }
    // ToString -- Stringify the account.
    public string ToSavingsAccountString()
    {
        return String.Format("{0} ({1}%)",
            ToBankAccountString(), _interestRate * 100);
    }
}
public class Program
{
    // DirectDeposit -- Deposit my paycheck automatically.
    public static void DirectDeposit(BankAccount ba, decimal pay)
    {
        ba.Deposit(pay);
    }
    public static void Main(string[] args)
    {
        // Create a bank account and display it.
        BankAccount ba = new BankAccount(100M);
        DirectDeposit(ba, 100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // Now a savings account
        SavingsAccount sa = new SavingsAccount(100M);
        DirectDeposit(ba, 100M);
        Console.WriteLine("Account {0}", ba.ToBankAccountString());
        // Now a savings account
        sa.AccumulateInterest();
        Console.WriteLine("Account {0}", sa.ToSavingsAccountString());
        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

C# provides a method that’s inverse to the constructor: the destructor. It carries the name of the class with a tilde (~) in front. For example, ~BaseClass() is the destructor for BaseClass.

# Garbage collection and the destructor

The C# destructor is much less useful than it is in other object-oriented languages, such as C++, because C# has nondeterministic destruction. Understanding what that term means — and why it’s important — requires some explanation.
