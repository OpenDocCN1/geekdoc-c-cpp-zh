# Why You Should Worry about Access Control

# 265

Keeping a member hidden by declaring it private offers the maximum amount of security. However, in many cases, you don't need level of security. After all, the members of a subclass already depend on the members of the base class, so protected offers a comfortable level of security.

# Why You Should Worry about Access Control

Declaring the internal members of a class public is a bad idea for at least these reasons:

+   * With all data members public, you can't easily determine when and how data members are being modified. Why better safety checks into the Deposit() and Withdraw() methods? In fact, even better with these methods? Any method of class can modify these elements at any time. If other methods can access these elements, they almost certainly win.

Your BankAccount program may execute for an hour or before you notice that one of the accounts has a negative balance. The Withdraw() method would have ensured that this situation didn't happen, so obviously another method accessed the balance without going through Withdraw(). Figuring out which method is responsible and under conditions is a problem.

+   * Exposing all members of the class makes the interface too complicated. As a programmer using the BankAccount class, you don't want to know the internal workings of the class. You just need to know that you can deposit and withdraw funds. It's like a candy machine that has 50 buttons versus just—the ones you need.

+   * Exposing internal elements can lead to corruption of the class rules. For example, my BankAccount class doesn't allow the balance to be negative under any circumstances. That business rule should be isolated within the Withdraw() method. Otherwise, you have to add this check everywhere that the balance is updated.

Sometimes, a bank decides to change the rules so that "custom customers" are allowed to carry slightly negative balances for a short period, to avoid unintended overdrafts. Then you have to search through the program to update every section of code that accesses the balance, to ensure that the safety checks are changed.

Make your classes and methods no more accessible than necessary. I give you this advice not so much to cause paranoia about snoopy hackers as to suggest a prudent step that helps reduce errors as you code. Use private, if possible, and escalate to protected, internal, internal protected or public as necessary.

![](bbox=[0.134, 0.823, 0.213, 0.903])