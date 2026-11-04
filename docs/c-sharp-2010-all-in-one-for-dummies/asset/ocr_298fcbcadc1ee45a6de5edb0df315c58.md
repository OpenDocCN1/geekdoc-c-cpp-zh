```
```csharp
// Withdraw -- This version accesses the hidden method in the base
//    class by explicitly recasting the this object.
new public decimal Withdraw(decimal withdrawal)
{
    // Cast the this reference into an object of class BankAccount.
    BankAccount ba = (BankAccount)this;
    // Invoking Withdraw() using this BankAccount object
    // calls the method BankAccount.Withdraw().
    decimal amountWithdrawn = ba.Withdraw(withdrawal);
    amountWithdrawn += ba.Withdraw(1.5);
    return amountWithdrawn;
}
```
```

This solution works: The call ba.Withdraw() now invokes the BankAccount method, just as intended. The problem with this approach is the explicit reference to BankAccount. A future change to the program may rearrange the inheritance hierarchy so that SavingsAccount no longer inherits directly from BankAccount. This type of rearrangement breaks this method in a way that future programmers may not easily find. (Heck, I would never be able to find a bug like that one.)

You need a way to tell C# to call the Withdraw() method from “the class immediately above” in the hierarchy without naming it explicitly. That would be the class that SavingsAccount extends. C# provides the keyword base for this purpose.

![](bbox=[0.07, 0.42, 0.16, 0.51])

This keyword base is the same one that a constructor uses to pass arguments to its base class constructor.

The C# keyword base, shown in the following chunk of code, is the same sort of beast as this but is automatically recast to the base class no matter what that class may be:

```
```csharp
// Withdraw -- You can withdraw any amount up to the
//    balance; return the amount withdrawn.
new public decimal Withdraw(decimal withdrawal)
{
    // Take the $1.50 off the top.
    base.Withdraw(1.5M);
    // Now you can withdraw from what's left.
    return base.Withdraw(withdrawal);
}
```
```

The call base.Withdraw() now invokes the BankAccount.Withdraw() method, thereby avoiding the recursive “invoking itself” problem. In addition, this solution doesn't break if the inheritance hierarchy is changed.

# # Polymorphism

You can overload a method in a base class with a method in the subclass. As simple as this process sounds, it introduces considerable capability, and with capability comes danger.