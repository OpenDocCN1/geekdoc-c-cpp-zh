# 262 Restricting Access to Class Members

does. People start out with good intentions (like my intentions to work every day), but those good intentions get crushed by the weight of schedule pressures to get out the door. Speaking of weight....

# A public example of public BankAccount

The following BankAccount class example declares all its methods public declares its data members, _accountNumber and _balance. Note that I've left it in an incorrect state to make a point. The following code chunk fails to compile correctly:

![](bbox=[0.165, 0.313, 0.238, 0.385])

```
// Create a bank account using a double variable
// to store the account balance (keep the balance in a private
// variable to hide its implementation from the outside world)
// Note: Until you correct it, this program fails to compile
// because Main() refers to a private member of class BankAccount.
namespace BankAccount {
    public class Program {
        public static void Main(string[] args {
            Console.WriteLine("This program doesn't compile in its state.");
            Console.WriteLine("Create a bank account object");
            BankAccount ba = new BankAccount();
            ba.InitBankAccount();
            // Accessing the balance via the Deposit() method is okay
            ba.Deposit() has access to all the data members.
            ba.Deposit(10);
            // Accessing the data member directly is a compile-time error.
            Console.WriteLine("Just in case you get this far the following is " + supposed to generate a compile error");
            ba._balance = it;
            // Wait for user to acknowledge the results.
            Console.WriteLine("Press Enter to terminate...");
            Console.Read();
        }
    }
classBankAccount {
    // Define a class that represents a simple account.
    private int _nextAccountNumber = 1000;
    private int _accountNumber;
    // Maintain the balance as a double variable.
    private double _balance;
    // Init - Initialize a bank account with the next
    // account id and a balance of 0.
    public void InitBankAccount() {
        _accountNumber = ++nextAccountNumber;
        _balance = 0.0;
    }
    // GetBalance - Return the current balance.
    public double GetBalance() {
        return _balance;
    }
}
```

*