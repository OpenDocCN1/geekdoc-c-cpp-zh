The two subclass Output() methods differ in a trivial way: Both accept input strings, which they regurgitate to users. However, one converts the string to all caps before output and the other converts it to all-lowercase characters.

The following output from this program demonstrates the polymorphic nature of AbstractBaseClass:

```
Creating a SubClass1 object
Call to SubClass1.Output() from within TEST
Creating a SubClass2 object
Call to SubClass2.Output() from within test
Press Enter to terminate...
```

![](bbox=[0.15, 0.45, 0.25, 0.6])

An abstract method is automatically virtual, so you don't add the virtual keyword to an abstract method.

# Creating an abstract object — not!

Notice something about the AbstractInheritance program: It isn't legal to create an AbstractBaseClass object, but the argument to Test() is declared to be an object of the class AbstractBaseClass or one of its subclasses. It's the "subclasses" clause that's critical here. The SubClass1 and SubClass2 objects can be passed because each one is a concrete subclass of AbstractBaseClass. The IS_A relationship applies. This powerful technique lets you write highly general methods.

# Sealing a Class

You may decide that you don't want future generations of programmers to be able to extend a particular class. You can lock the class by using the keyword sealed.

![](bbox=[0.12, 0.85, 0.22, 0.97])

A sealed class cannot be used as the base class for any other class.

Consider this code snippet:

```
using System;
public class BankAccount
{
    // withdrawal -- You can withdraw any amount up to the
    //   balance; return the amount withdrawn
    virtual public void Withdraw(decimal withdrawal)
    {
        Console.WriteLine("invokes BankAccount.Withdraw()");
    }
}
public sealed class SavingsAccount : BankAccount
{
```