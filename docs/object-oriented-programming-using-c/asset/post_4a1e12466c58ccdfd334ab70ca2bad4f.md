
When each individual account is created we will add it to the list of accounts and we will also allow an individual account to be retrieved so that the account holder can deposit money into their account.

We will demonstrate this with a Main method that runs through a fixed routine a) adding a few accounts, b) displaying these accounts and c) retrieving an account, adding money to this account and displaying the list of accounts again.

We will need an accessor method in Bank that the Main method can access the list of accounts to display them. In C# we will implement this using a public property.

The code for the Account class is shown below and should need no explanation.

```csharp
class Account
{
    private String name;
    public String Name
    {
        get { return name; }
    }

    private String dateOfBirth;
    public String DateOfBirth
    {
        get { return dateOfBirth; }
    }

    private int balance;

    public Account(String name, String dob)
    {
        this.name = name;
        this.dateOfBirth = dob;
        balance = 0;
    }

    public void DepositMoney(int increase)
    {
        balance = balance + increase;
    }

    public override String ToString()
    {
        return "Name: " + name + "\nBalance: " + balance;
    }
}
```

## Object Oriented Programming C# Generic Collections and how to Serialize them

The code for the Bank class is given below and this demonstrates how easy it is to use the collection class 'List'.

```csharp
class Bank
{
    private List<Account> accounts;
    public List<Account> Accounts
    {
        get { return accounts; }
    }

    public Bank()
    {
        accounts = new List<Account>();
    }

    public void AddAccount(Account account)
    {
        accounts.Add(account);
    }

    public Account GetAccount(String name, String dob)
    {
        Account FoundAccount = null;
        foreach (Account a in accounts)
        {
            if (a.Name == name && (a.DateOfBirth == dob))
            {
                FoundAccount = a;
            }
        }
        return FoundAccount;
    }
}
```

Firstly the constructor creates a list of accounts. With any list this automatically resizes itself, so unlike an array we do not need to worry about running out of space.

Also when elements are removed the remaining elements are moved so that the blank spaces are deleted. While this is not hard to do with arrays it is a time consuming process that is handled automatically for when we use Lists.

Adding an account becomes a trivial task of invoking the Add() method.

Finally retrieving an individual account is fairly simple to do by iterating through the list until the account we are looking for found.

Note this list manages a collection of complex objects and when any object is retrieved from the list the methods associated with that object can be invoked on that object.

This can be demonstrated via the following 'Main' method.

## Object Oriented Programming using C#

### Generic Collections and how to Serialize them

```csharp
static void Main(string[] args)
{
    Bank b = new Bank();
    Account a;

    a = new Account("Alice", "06/12/1963");
    b.AddAccount(a);
    a = new Account("Bert", "14/08/1990");
    b.AddAccount(a);
    a = new Account("Claire", "1/1/2000");
    b.AddAccount(a);

    // Display the accounts
    foreach (Account acc in b.Accounts)
    {
        Console.WriteLine(acc.ToString());
    }

    Account al = b.GetAccount("Bert", "14/08/1990");
    al.DepositMoney(100);

    // Display the accounts again
    foreach (Account acc in b.Accounts)
    {
        Console.WriteLine(acc.ToString());
    }

    Console.ReadLine();
}
```

![](img/e143b38d00f95425fa4f3efca0527189_143_0.png)

YOUR CHANCE TO CHANGE THE WORLD

Here at Ericsson we have a deep rooted belief that the innovations we make on daily basis can have a profound effect on making the world a better place for people, business and society. Join us.

- In Germany we are especially looking for graduates as Integration Engineers for
- Radio Access and IP Networks
- IMS and IPT

We are looking forward to getting your application! To apply and for all current job openings please visit our web page: www.ericsson.com/careers

Object Oriented Programming using C#

The code above performs the following actions :-

- Firstly invokes the constructor for the Bank class which in turn creates an empty list of Accounts.
- It creates three accounts and adds these to the list in the Bank object.
- The list of accounts is then displayed.
- An individual bank account is then retrieved from the list and money is deposited into this account.
- Finally the list of accounts is displayed again.

The output from running this program is shown below....

![](img/e143b38d00f95425fa4f3efca0527189_144_0.png)

## 7.9 An Example Using Sets

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

Generic Collections and how to Serialize them

| Bank | Account |
| :--- | :--- |
| | 1 accounts * | - name: String<br>-dateOfBirth:String<br>- balance int |
| +AddAccount(account : Account)<br>+GetAccount(name: String, DOB: String) | + Account(name: String)<br>+DepositMoney(increase :int)<br>+ToString():String |

However a much better choice for this collection would be to store the collection of accounts as a set, because sets do not allow duplicates to be created.

Consider a set of bank accounts :-

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Furthermore the list stores objects in a particular order – in this case order the account were created. But this order is irrelevant as it will not help find a particular account belonging to an individual.

The essential problem remains the same – to store a collection of bank accounts.

Object Oriented Programming using C#

### Generic Collections and how to Serialize them

In the example above we used a list to store a collection of bank accounts. This is not the most sensible choice as it allows duplicates to be created and the bank would get very confused if two identical accounts were created (when money was deposited into an account which should be added to?).

Consider a set of bank accounts :-

