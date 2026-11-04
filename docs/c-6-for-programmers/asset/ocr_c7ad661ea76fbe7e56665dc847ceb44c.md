```
```csharp
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
```

**Fig. 4.11** | Account class with a decimal instance variable balance and a Balance property and Deposit method that each perform validation. (Part 2 of 2.)

# *Account Class Two-Parameter Constructor*

It’s common for someone opening an account to deposit money immediately, so the constructor (lines 10–14) now receives a second parameter—initialBalance of type decimal that represents the starting balance. Line 13 assigns initialBalance to the property Balance, invoking Balance’s set accessor to ensure that the initialBalance argument is valid before assigning a value to the instance variable balance.

# *Account Property Balance*

Property Balance (lines 17–32) of type decimal provides a get accessor, which allows clients of the class to obtain a particular Account object’s balance. The property also provides a set accessor.