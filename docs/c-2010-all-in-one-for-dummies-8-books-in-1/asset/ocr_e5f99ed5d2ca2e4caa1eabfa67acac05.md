# 312 Overloading an Inherited Method

# Making the hiding approach better than adding a simple test

On the surface, adding a flag to the BankAccount.Withdraw() method may seem simpler than all this method-hiding stuff. After all, it's just four little lines of code, which are nothing more than braces.

The problems are manifold. (I had to write several chapters just to be able to use that word.) One problem is the BankAccount class has no business worrying about the details of SavingsAccount. More formally, it's "breaking the encapsulation of SavingsAccount." Base classes don't normally know about their subclasses, which leads to the real problem: Suppose your bank subclasses decide to add a CheckAccount or a CDAccount. All those likely have different withdrawal policies, each requiring its own flag. After adding three or four different types of accounts, the old Withdraw() method looks complicated. Each of those classes should worry about its own withdrawal policies and leave the old BankAccount.Withdraw() alone. Classes are responsible for themselves.

# Accidentally hiding a base class method

Oddly enough, you can hide a base class method accidentally. For example, you have a Vehicle.TakeOff() method that starts the vehicle rolling. Later, someone else extends your Vehicle class with an Airplane class. TakeOff() method is entirely different. In airplane logic, "take off" means more than "start moving." Clearly, this is a case of mistaken identity — the methods have no similarity other than their identical name.

Fortunately, C detects this problem.

C generates an ominous warning when it compiles the compiler HidingWithdrawal program example. The text of the warning message is, here's the important part:

```
...BankAccount.Withdraw(decimal) hides inherited member
'...BankAccount.Withdraw(decimal)'
Use the new keyword if hiding was intended.
```

C is trying to tell you that you've written a method in a subclass that has the same name as one in the base class. Is that what you meant to do?

This is just a warning — you don't notice it until you switch over to the Error List to take a look. But you must sort out and fix all warnings. In almost every case, a warning is telling you something about what you can bite if you don't fix it.

Tell the C compiler to treat warnings as errors, at least part of the time. To do so, choose Project::Properties. In the build pane of your project's properties, scroll down to Errors and Warnings. Setting the Level to 4, the highest level, which turns the compiler into more of a chatterbox. Also,