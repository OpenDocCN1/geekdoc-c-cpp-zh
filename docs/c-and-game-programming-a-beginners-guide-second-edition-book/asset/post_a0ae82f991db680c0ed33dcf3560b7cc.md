
## Overloading Constructors

Constructors can be overloaded in numerous ways. Again, these functions will be automatically referenced when the appropriate instances are declared, and again, their arguments will determine the accessible function. One such class revision might include a secondary constructor that gives a special rate to some depositors and a third that determines an alternate rate for both their savings and loans (see Example 5.22).

### Example 5.22. Overloading constructors.

```csharp
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        public decimal InterestRate;
        public decimal LoanRate;

        // Default Constructor
        public BankAccount() {
            InterestRate = .03M; LoanRate = .13M;
        }

        // Overloaded Constructor
        public BankAccount(decimal IRate) {
            InterestRate = .03M;
            LoanRate = .13M;
        }

        // Overloaded Constructor
        public BankAccount(decimal IRate, decimal LoanRate) {
            InterestRate = .03M;
            LoanRate = .13M;
        }
    }

    class Class1 {
        static void Main() {
            BankAccount account = new BankAccount();
        }
    }
}
```

## Assigning Instances

Once two or more instances are declared by the same class, the values of those instances can be passed using the assignment statement; for example, account1 = account2; // where BankAccount account1, account2; In Example 5.23, the values from account2 are passed to account1 (this process is commonly referred to as a memberwise copy). It is worth noting that restrictions in systems implementations can potentially cause errors when dealing with dynamically allocated storage.

### Example 5.23. Memberwise copy—assigning instances.

```csharp
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        public decimal InterestRate;
        public decimal LoanRate;

        public BankAccount() {
            InterestRate = .03M;
            LoanRate = .13M;
        }

        public BankAccount(decimal IRate) {
            InterestRate = .03M;
            LoanRate = .13M;
        }

        public BankAccount(decimal IRate, decimal LoanRate) {
            InterestRate = .03M;
            LoanRate = .13M;
        }
    }

    class Class1 {
        static void Main() {
            BankAccount account = new BankAccount();
            BankAccount account1 = new BankAccount();
            BankAccount account2 = new BankAccount(23);

            account = account1;
            account = account2;
        }
    }
}
```

## Reading and Writing to Private Members

Encapsulation is a key point when working with private members, but for varying reasons we often find that we need to gain at least limited access in order to implement changes within our programs. These changes can be facilitated with the use of specialized member functions. Practically, these functions are usually broken up into two forms: the first to read (compare, get) those values, and the second to set (put, write) or alter those values. Typically, the setting functions are void, while the reading functions are meant to return the implied value. Both are usually only used to access one class member, but several equivalent member functions may be written to include as many members as required (see Example 5.24).

### Example 5.24. Reading and writing to private members.

```csharp
public decimal ReadInterestRate() {
    return(InterestRate);
}

public void SetInterestRate(decimal IRate) {
    InterestRate = IRate;
}
```

## The Keyword this

The keyword this is a specialized reference signature used to indicate the referencing object of a passing class, therefore, this is a longhand version for the otherwise abbreviated member. While the this reference is implied, its definitions can become ambiguous and should be included to prevent this error (see Examples 5.25 and 5.26).

Unlike C++, C#'s single dot reference can be used for both reference and nonreference. The proper notation for a this pointer depends upon the purpose of its referencing class, e.g., the this->variable versus the (*this).variable.

### Example 5.25. The this reference.

```csharp
/* Written with the this reference. */
using System;
using System.IO;

namespace Chapter5 {
    class BankAccount {
        protected string first_name;
        protected string last_name;
        protected long account_number;
        protected decimal checking;
        protected decimal savings;
        protected short pin_number;

        private void ReadFile() {
            StreamReader file = new StreamReader(@"C:\MyFile.txt");
            this.pin_number = short.Parse(file.ReadLine());
            this.account_number = long.Parse(file.ReadLine());
            this.savings = decimal.Parse(file.ReadLine());
            this.checking = decimal.Parse(file.ReadLine());
            this.first_name = file.ReadLine();
            this.last_name = file.ReadLine();
            file.Close();
        }

        public void CreateFile() {
            Console.WriteLine("Enter Your New Pin Number: ");
            this.pin_number = short.Parse(Console.ReadLine());

            Random rnd = new Random();
            this.account_number = rnd.Next(1, 100);
            Console.WriteLine("\nYour New Account Number is: {0}",
                this.account_number);
            Console.Write("\nEnter your first name: ");
            this.first_name = Console.ReadLine();
            Console.Write("\nEnter your last name: ");
            this.last_name = Console.ReadLine();
            Console.WriteLine("\nEnter Your Savings Balance: ");
            this.savings = decimal.Parse(Console.ReadLine());
            Console.WriteLine("\nEnter Your Checking Balance: ");
            this.checking = decimal.Parse(Console.ReadLine());
            this.SaveFile(0, 0);
        }

        private void SaveFile(short input1, short input2) {
            StreamWriter file = new StreamWriter(@"C:\MyFile.txt");
            file.WriteLine(this.pin_number);
            file.WriteLine(this.account_number);
            file.WriteLine(this.savings + input1);
            file.WriteLine(this.checking + input2);
            file.WriteLine(this.first_name);
            file.WriteLine(this.last_name);
            file.Close();
        }

        public void ViewFile() {
            this.ReadFile();
            Console.WriteLine("Pin Number: {0}",
                this.pin_number);
            Console.WriteLine("Account Number: {0}",
                this.account_number);
            Console.WriteLine("Name: {0} {1}",
                this.first_name, this.last_name);
            Console.WriteLine("Savings Balance: {0}",
                this.savings);
            Console.WriteLine("Checking Balance: {0}",
                this.checking);
        }
    }

    class Class1 {
        static void Main() {
            BankAccount account = new BankAccount();

            char input;
            while (true) {
                Console.WriteLine("Enter <C> to create new file or " +
                    "<V> to view account");
                input = char.Parse(Console.ReadLine());

                if (Char.ToUpper(input) == 'C') {
                    account.CreateFile();
```

```csharp
Console.WriteLine("\nYour New Account Number is: {0}",
    account_number);
Console.Write("\nEnter your first name: ");
first_name = Console.ReadLine();
Console.Write("\nEnter your last name: ");
last_name = Console.ReadLine();
Console.WriteLine("\nEnter Your Savings Balance: ");
savings = decimal.Parse(Console.ReadLine());
Console.WriteLine("\nEnter Your Checking Balance: ");
checking = decimal.Parse(Console.ReadLine());
SaveFile(0, 0);
}

private void SaveFile(short input1, short input2) {
    StreamWriter file = new StreamWriter(@"C:\MyFile.txt");
    file.WriteLine(pin_number);
    file.WriteLine(account_number);
    file.WriteLine((savings + input1));
    file.WriteLine((checking + input2));
    file.WriteLine(first_name);
    file.WriteLine(last_name);
    file.Close();
}

public void ViewFile() {
    ReadFile();
    Console.WriteLine("Pin Number: {0}",
        pin_number);
    Console.WriteLine("Account Number: {0}",
        account_number);
    Console.WriteLine("Name: {0} {1}",
        first_name, last_name);
    Console.WriteLine("Savings Balance: {0}",
        savings);
    Console.WriteLine("Checking Balance: {0}",
        checking);
}

class Class1 {
    static void Main() {
        BankAccount account = new BankAccount();
```
