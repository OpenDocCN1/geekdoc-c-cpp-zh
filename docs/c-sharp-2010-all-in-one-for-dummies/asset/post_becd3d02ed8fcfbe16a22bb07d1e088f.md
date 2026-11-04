
in the Treat Warnings As Errors section, select All. (If a particular warning becomes annoying, you can list it in the Suppress Warnings box to keep it out of your face.) When you treat warnings as errors, you're forced to fix the warnings — just as you would be forced to fix real compiler errors. This practice makes for better code. Even if you don't enable the Treat Warnings As Errors option, leave the Warning Level at 4 and select the Error List window after each build.

The descriptor new, shown in the following sample code, tells C# that the hiding of methods is intentional and not the result of an oversight (and it makes the warning disappear):

```csharp
// No withdraw() pains now.
new public decimal Withdraw(decimal withdrawal)
{
    // . . . no change internally . . .
}
```

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_338_0.png)

This use of the keyword new has nothing to do with the same word new that's used to create an object. (C# even overloads itself!)

## Calling back to base

Check out the SavingsAccount.Withdraw() method in the HidingWithdrawal example, shown earlier in this chapter. The call to BankAccount.Withdraw() from within this new method includes the keyword base.

The following version of the method without the base keyword doesn't work:

```csharp
new public decimal Withdraw(decimal withdrawal)
{
    decimal amountWithdrawn = Withdraw(withdrawal);
    amountWithdrawn += Withdraw(1.5);
    return amountWithdrawn;
}
```

This call has the same problem as this one:

```csharp
void fn()
{
    fn(); // Call yourself.
}
```

The call to fn() from within fn() ends up calling itself (recursing) repeatedly. Similarly, a call to Withdraw() from within the method calls itself in a loop, chasing its tail until the program eventually crashes.

Somehow, you need to indicate to C# that the call from within SavingsAccount.Withdraw() is meant to invoke the base class BankAccount.Withdraw() method. One approach is to cast the this reference into an object of class BankAccount before making the call:

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

This solution works: The call ba.Withdraw() now invokes the BankAccount method, just as intended. The problem with this approach is the explicit reference to BankAccount. A future change to the program may rearrange the inheritance hierarchy so that SavingsAccount no longer inherits directly from BankAccount. This type of rearrangement breaks this method in a way that future programmers may not easily find. (Heck, I would never be able to find a bug like that one.)

You need a way to tell C# to call the Withdraw() method from “the class immediately above” in the hierarchy without naming it explicitly. That would be the class that SavingsAccount extends. C# provides the keyword base for this purpose.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_339_0.png)

This keyword base is the same one that a constructor uses to pass arguments to its base class constructor.

The C# keyword base, shown in the following chunk of code, is the same sort of beast as this but is automatically recast to the base class no matter what that class may be:

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

The call base.Withdraw() now invokes the BankAccount.Withdraw() method, thereby avoiding the recursive “invoking itself” problem. In addition, this solution doesn't break if the inheritance hierarchy is changed.

## Polymorphism

You can overload a method in a base class with a method in the subclass. As simple as this process sounds, it introduces considerable capability, and with capability comes danger.

Here's a thought experiment: Should you make the decision to call BankAccount.Withdraw() or SavingsAccount.Withdraw() at compile-time or at runtime?

To illustrate the difference, I change the previous HidingWithdrawal program in a seemingly innocuous way. I call this new version HidingWithdrawalPolymorphically. (I've streamlined the listing by leaving out the stuff that doesn't change.) The new version is shown here:

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_340_0.png)

// HidingWithdrawalPolymorphically -- Hide the Withdraw() method in the base class with a method in the subclass of the same name.
// class Program
public class Program
{
    public static void MakeAWithdrawal(BankAccount ba, decimal amount)
    {
        ba.Withdraw(amount);
    }
    public static void Main(string[] args)
    {
        BankAccount ba;
        SavingsAccount sa;

        // Create a bank account, withdraw $100, and
        // display the results.
        ba = new BankAccount(300M);
        MakeAWithdrawal(ba, 100M);

        // Try the same trick with a savings account.
        sa = new SavingsAccount(200M, 12);
        MakeAWithdrawal(sa, 100M);

        // Display the resulting balance.
        Console.WriteLine("When invoked through intermediary:");
        Console.WriteLine("BankAccount balance is {0:C}", ba.Balance);
        Console.WriteLine("SavingsAccount balance is {0:C}", sa.Balance);

        // Wait for user to acknowledge the results.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}

The following output from this program may or may not be confusing, depending on what you expected:

When invoked through intermediary
BankAccount balance is $100.00
SavingsAccount balance is $100.00
Press Enter to terminate...

This time, rather than perform a withdrawal in Main(), the program passes the bank account object to the method MakeAWithdrawal().

The first question is fairly straightforward: Why does the MakeAWithdrawal() method even accept a SavingsAccount object when it clearly states that it's looking for a BankAccount? The answer is obvious: 'Because a SavingsAccount IS_A BankAccount.' (See Chapter 6 of this minibook.)

The second question is subtle. When passed a `BankAccount` object, `MakeAWithdrawal()` invokes `BankAccount.Withdraw()` — that's clear enough. But when passed a `SavingsAccount` object, `MakeAWithdrawal()` calls the same method. Shouldn't it invoke the `Withdraw()` method in the subclass?

The prosecution intends to show that the call `ba.Withdraw()` should invoke the method `BankAccount.Withdraw()`. Clearly, the `ba` object is a `BankAccount`. To do anything else would merely confuse the state. The defense has witnesses back in `Main()` to prove that although the `ba` object is declared `BankAccount`, it is in fact a `SavingsAccount`. The jury is dead-locked. Both arguments are equally valid.

In this case, C# comes down on the side of the prosecution: The safer of the two possibilities is to go with the declared type because it avoids any miscommunication. The object is declared to be a `BankAccount` and that's that. However, that may not be what you want.

### Using the declared type every time (Is that so wrong?)

In some cases, you don't want to choose the declared type. What you want (or, "what you really, really want," to quote the popular Spice Girls song) is to make the call based on the *real type* — the runtime type — as opposed to the declared type. For example, you want to use the `SavingsAccount` stored in a `BankAccount` variable. This capability to *decide at runtime* is known as *polymorphism*, or *late binding*. Using the declared type every time is called *early binding* because it sounds like the opposite of *late binding*.

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_341_0.png)

The ridiculous term *polymorphism* comes from the Greek language: *Poly* means "more than one," *morph* means "transform," and *ism* is a fairly useless Greek term. But we're stuck with it.

Polymorphism and late binding aren't exactly the same concept — but the difference is subtle:

- *Polymorphism* refers to the general ability to decide which method to invoke at runtime.
- *Late binding* refers to the specific way a language implements polymorphism.

Polymorphism is the key to the power of object-oriented (OO) programming. It's so important that languages that don't support it can't advertise themselves as OO languages. (I think it's an FDA regulation: You can't label a
