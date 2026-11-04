# ### Making the hiding approach better than adding a simple test

On the surface, adding a flag to the BankAccount.Withdraw() method may seem simpler than all this method-hiding stuff. After all, it's just four little lines of code, two of which are nothing more than braces.

The problems are manifold. (I had to write several chapters just to be able to use that word.) One problem is that the BankAccount class has no business worrying about the details of SavingsAccount. More formally, it's known as “breaking the encapsulation of SavingsAccount.” Base classes don't normally know about their subclasses, which leads to the real problem: Suppose that your bank subsequently decides to add a CheckingAccount or a CDAccount or a TBillAccount. All those likely additions have different withdrawal policies, each requiring its own flag. After adding three or four different types of accounts, the old Withdraw() method starts looking complicated. Each of those types of classes should worry about its own withdrawal policies and leave the poor old BankAccount.Withdraw() alone. Classes are responsible for themselves.

# ### Accidentally hiding a base class method

Oddly enough, you can hide a base class method accidentally. For example, you may have a Vehicle.TakeOff() method that starts the vehicle rolling. Later, someone else extends your Vehicle class with an Airplane class. Its TakeOff() method is entirely different. In airplane lingo, “take off” means more than just “start moving.” Clearly, this is a case of mistaken identity — the two methods have no similarity other than their identical name.

Fortunately, C# detects this problem.

C# generates an ominous-looking warning when it compiles the earlier HidingWithdrawal program example. The text of the warning message is long, but here's the important part:

```
    '...SavingsAccount.Withdraw(decimal)' hides inherited member
    '...BankAccount.Withdraw(decimal)'.
    Use the new keyword if hiding was intended.
```

C# is trying to tell you that you've written a method in a subclass that has the same name as a method in the base class. Is that what you meant to do?

![](bbox=[0.119, 0.718, 0.209, 0.773])

This message is just a warning — you don't even notice it unless you switch over to the Error List window to take a look. But you must sort out and fix all warnings. In almost every case, a warning is telling you about something that can bite you if you don't fix it.

![](bbox=[0.119, 0.808, 0.209, 0.862])

Tell the C# compiler to treat warnings as errors, at least part of the time. To do so, choose Project > Properties. In the Build pane of your project's properties page, scroll down to Errors and Warnings. Set the Warning Level to 4, the highest level, which turns the compiler into more of a chatterbox. Also,