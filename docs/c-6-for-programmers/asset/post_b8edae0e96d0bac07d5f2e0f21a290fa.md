
```csharp
6 class AccountTest
7 {
8     static void Main()
9     {
10     // create two Account objects
11     Account account1 = new Account("Jane Green");
12     Account account2 = new Account("John Blue");
13
14     // display initial value of name for each Account
15     Console.WriteLine($"account1 name is: {account1.Name}");
16     Console.WriteLine($"account2 name is: {account2.Name}");
17     }
18 }
```

account1 name is: Jane Green
account2 name is: John Blue

**Fig. 4.9** | Using the Account constructor to set an Account's name when an Account object is created. (Part 2 of 2.)

## Default Constructor

Recall that line 10 of Fig. 4.5

```csharp
Account myAccount = new Account();
```

used new to create an Account object. The empty parentheses in the expression

```csharp
new Account()
```

indicate a call to the class's default constructor—in any class that does not explicitly declare a constructor, the compiler provides a public default constructor (which always has no parameters). When a class has only the default constructor, the class's instance variables are initialized to their default values:

- 0 for numeric simple types,
- false for simple type bool and
- null for all other types.

In Section 10.5, you'll learn that classes can have multiple constructors through a process called overloading.

## There's No Default Constructor in a Class That Declares a Constructor

If you declare one or more constructors for a class, the compiler will not create a default constructor for that class. In that case, you will not be able to create an Account object with the expression new Account() as we did in Fig. 4.5—unless one of the custom constructors you declare takes no parameters.

### Software Engineering Observation 4.4

Unless default initialization of your class's instance variables is acceptable, provide a custom constructor to ensure that your instance variables are properly initialized with meaningful values when each new object of your class is created.

## Adding the Constructor to Class Account’s UML Class Diagram

The UML class diagram of Fig. 4.10 models class Account of Fig. 4.8, which has a constructor with a string accountName parameter. The UML models constructors as operations in the third compartment of a class diagram. To distinguish a constructor from the class’s other operations, the UML requires that the word “constructor” be enclosed in guillemets (« and ») and placed before the constructor’s name. It’s customary to list constructors before other operations in the third compartment. In Fig. 4.14, you’ll see a class diagram with both a constructor and an operation in the third compartment.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_122_0.png)

**Fig. 4.10** | UML class diagram for Account class of Fig. 4.8.

## 4.9 Account Class with a Balance; Processing Monetary Amounts

In this section, we’ll declare an Account class that maintains an Account’s *balance* in addition to its name. Most account balances are not whole numbers (such as 0, −22 and 1024), rather they’re numbers that include a decimal point, such as 99.99 or −20.15. For this reason, class Account represents the account balance using type `decimal`, which is designed to precisely represent numbers with decimal points, especially *monetary amounts*.

### 4.9.1 Account Class with a decimal balance Instance Variable

A typical bank services *many* accounts, each with its *own* balance, so our next Account class (Fig. 4.11) maintains a bank account’s

- `name`—as the auto-implemented Name property (line 6)—and
- `balance`—as the private decimal instance variable balance (line 7) and a corresponding public Balance property (lines 17–32). We use a fully implemented Balance property here so we can ensure that the set accessor’s argument is valid before assigning it to the balance instance variable.

A decimal instance variable is initialized to zero by default. Every instance (i.e., object) of class Account contains its *own* name and balance.

```csharp
// Fig. 4.11: Account.cs
// Account class with a balance and a Deposit method.

class Account
{
6    public string Name { get; set; } // auto-implemented property
7    private decimal balance; // instance variable
8
9    // Account constructor that receives two parameters
10   public Account(string accountName, decimal initialBalance)
11   {
12       Name = accountName;
13       Balance = initialBalance; // Balance's set accessor validates
14   }
15
16   // Balance property with validation
17   public decimal Balance
18   {
19       get
20       {
21           return balance;
22       }
23       private set // can be used only within the class
24       {
25           // validate that the balance is greater than 0.0; if it's not,
26           // instance variable balance keeps its prior value
27           if (value > 0.0m) // m indicates that 0.0 is a decimal literal
28           {
29               balance = value;
30           }
31       }
32   }
33
34   // method that deposits (adds) only a valid amount to the balance
35   public void Deposit(decimal depositAmount)
36   {
37       if (depositAmount > 0.0m) // if the depositAmount is valid
38       {
39           Balance = Balance + depositAmount; // add it to the balance
40       }
41   }
42 }
```

**Fig. 4.11** | Account class with a decimal instance variable balance and a Balance property and Deposit method that each perform validation. (Part 1 of 2)

**Fig. 4.11** | Account class with a decimal instance variable balance and a Balance property and Deposit method that each perform validation. (Part 2 of 2.)

### Account Class Two-Parameter Constructor

It’s common for someone opening an account to deposit money immediately, so the constructor (lines 10–14) now receives a second parameter—initialBalance of type decimal that represents the starting balance. Line 13 assigns initialBalance to the property Balance, invoking Balance’s set accessor to ensure that the initialBalance argument is valid before assigning a value to the instance variable balance.

### Account Property Balance

Property Balance (lines 17–32) of type decimal provides a get accessor, which allows clients of the class to obtain a particular Account object’s balance. The property also provides a set accessor.

In Fig. 4.6, class `Account` defined a `Name` property in which the `set` accessor simply assigned the value received in its implicit parameter `value` to class `Account`’s instance variable `name`. The `Name` property did *not* ensure that `name` contains only valid data.

The `Balance` property’s `set` accessor performs validation (also known as validity checking). Line 27 (Fig. 4.11) ensures that the `set` accessor’s implicit `value` parameter is greater than `0.0m`—the letter `m` (or `M`) indicates that `0.0` is a **decimal literal**. If `value` is greater than `0.0m`, the amount stored in `value` is assigned to instance variable `balance` (line 29). Otherwise, `balance` is left unchanged—we’ll say more about error processing throughout the book.

Though we validated the `balance` in this example, we did not validate the `name`. Names are normally quite “free form”—there’s a wide variety of acceptable name formats. Often when you fill out a form, you’re asked to limit a `name` to a certain number of characters. In Chapter 16, *Strings and Characters: A Deeper Look*, you’ll learn how to check a `string`’s length, so that you can validate strings by checking that they’re not too long.

### set and get Accessors with Different Access Modifiers

By default, a property’s `get` and `set` accessors have the *same* access as the property—e.g., `public` property `Name`’s accessors are `public`. It’s possible to declare the `get` and `set` accessors with different access modifiers. In this case, one of the accessors must *implicitly* have the *same* access as the property and the other must be *explicitly* declared with a *more restrictive* access modifier than the property. We declared the `Balance` property’s `set` accessor `private`—this indicates that it may be used only in class `Account`, not by the class’s clients. This enables us to ensure that once an `Account` object exists, its `balance` can be modified only by method `Deposit`.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_124_0.png)

### **Error-Prevention Tip 4.3**

*The benefits of data integrity are not automatic simply because instance variables are made private—you must provide appropriate validity checking and report the errors.*

![](img/3f5ef6be1748bb746e5f71a483bba4d0_124_1.png)

### **Error-Prevention Tip 4.4**

*set accessors that set the values of private data should verify that the intended new values are proper; if they’re not, the set accessors should leave the instance variables unchanged and indicate an error. We demonstrate how to indicate errors by throwing exceptions in Chapter 10.*

### Account Class Deposit Method

The `public` method `Deposit` (lines 35–41 of Fig. 4.11) enables the client code to deposit money into an `Account`, thus increasing its `balance`. Line 35 indicates that

- the method does not return any information to its caller (as indicated by the return type `void`) and
- receives one parameter named `depositAmount`—a decimal value.

The `depositAmount` is added to the `balance` only if the parameter’s value is *valid*—that is, it’s greater than `0.0m` as specified in line 37. Line 39 first adds the current `Balance` and

4. The `m` is required to indicate a decimal literal. C# treats numeric literals with decimal points as type `double` by default, and `double`s and `decimal`s cannot be intermixed. We introduce type `double` in Chapter 5.
