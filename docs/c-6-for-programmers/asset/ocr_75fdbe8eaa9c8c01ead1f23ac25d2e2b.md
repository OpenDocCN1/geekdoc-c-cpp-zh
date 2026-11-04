depositAmount, forming a *temporary* sum which is then assigned to the `Balance` property. The property’s setter then *replaces* instance variable balance’s prior value (recall that addition has a *higher* precedence than the assignment operator). So line 39 uses the `Balance` property’s `get` accessor on the right side of the assignment and the `set` accessor on the left side. It’s important to understand that the calculation on the right side of the assignment operator in line 39 does *not* modify the instance variable balance—that’s why the assignment is necessary.

![](bbox=[0.16, 0.247, 0.214, 0.288])

> **Software Engineering Observation 4.5**
> 
> When implementing a method of a class, although it’s possible for the method to access the class’s instance variables directly, always use the class’s properties for that purpose. In Chapter 10, we’ll take a deeper look at this issue.

# 4.9.2 AccountTest Class That Uses Account Objects with Balances

Class AccountTest (Fig. 4.12) creates two Account objects (lines 9–10) and initializes them with a valid balance of 50.00m and an invalid balance of -7.53m, respectively—for the purpose of our examples, we assume that balances must be greater than or equal to zero. The calls to method Console.WriteLine in lines 13–16 output the account names and initial balances, which are obtained from each account’s Name and Balance properties.

```
```csharp
// Fig. 4.12: AccountTest.cs
// Reading and writing monetary amounts with Account objects.
using System;

class AccountTest
{
    static void Main()
    {
        Account account1 = new Account("Jane Green", 50.00m);
        Account account2 = new Account("John Blue", -7.53m);

        // display initial balance of each object
        Console.WriteLine(
            $"{account1.Name}'s balance: {account1.Balance:C}");
        Console.WriteLine(
            $"{account2.Name}'s balance: {account2.Balance:C}");

        // prompt for them to enter input
        Console.Write("\nEnter deposit amount for account1: ");
        decimal depositAmount = decimal.Parse(Console.ReadLine());
        Console.WriteLine(
            $"adding {depositAmount:C} to account1 balance\n");
        account1.Deposit(depositAmount); // add to account1's balance

        // display balances
        Console.WriteLine(
            $"{account1.Name}'s balance: {account1.Balance:C}");
        Console.WriteLine(
            $"{account2.Name}'s balance: {account2.Balance:C}");
}
```
```

**Fig. 4.12** | Reading and writing monetary amounts with Account objects. (Part 1 of 2.)