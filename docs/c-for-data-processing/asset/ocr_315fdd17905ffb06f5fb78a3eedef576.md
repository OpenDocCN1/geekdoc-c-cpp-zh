means that it has a set of behaviours because it has inherited them from its parent. In short:

Interface: "I can do these things because I have told you I can"
Inheritance: "I can do these things because my parent can"

# 4.9.1 Extending a parent class

We can see an example of a use for inheritance in our bank account project. We have already noted that a BabyAccount must behave just like a CustomerAccount except in respect of the cash withdrawal method. Customer accounts can draw out as much as they want. Baby accounts are only allowed to draw up to 10 pounds out at a time.

We have solved this problem from a design point of view by using interfaces. By separating the thing that does the job from the description of the job (which is what an interface lets you do) we can get the whole banking system thinking in terms of IAccount and then plug in accounts with different behaviours as required. We can even create brand new accounts at any time after the system has been deployed. These can be introduced and work alongside the others because they behave correctly (i.e. they implement the interface).

But this does make things a bit tiresome when we write the program. We need to create a BabyAccount class which contains a lot of code which is duplicated in the CustomerAccount class. "This is not a problem" you probably think. "I can use the editor block copy to move the program text across". But:

# Programmer's Point: Block Copy is Evil

I still make mistakes when I write programs. You might think that after such a huge number of years in the job I get everything right every time. Wrong. And a lot of the mistakes that I make are caused by improper use of block copy. I write some code and find that I need something similar, but not exactly the same, in another part of the program. So I use block copy. Then I change most, but not all, of the new code and find that my program doesn't work properly.

Try not to do this. A great programmer writes every piece of code once, and only once. If you need to use it in more than one place, make it a method.

What we really want to do is pick up all the behaviours in the CustomerAccount and then just change the one method that needs to behave differently. It turns out that we can do this in C# using inheritance. When I create the BabyAccount class I can tell the compiler that it is based on the CustomerAccount one:

```
public class BabyAccount : CustomerAccount, IAccount
{
}
```

The key thing here is the highlighted part after the class name. I have put the name of the class that BabyAccount is extending. This means that everything that CustomerAccount can do, BabyAccount can do.

I can now write code like:

```
BabyAccount b = new BabyAccount();
b.PayInFunds(50);
```

This works because, although BabyAccount does not have a PayInFunds method, the parent class does. This means that the PayInFunds method from the CustomerAccount class is used at this point.

So, instances of the BabyAccount class have abilities which they pick up from their parent class. In fact, at the moment, the BabyAccount class has no behaviours of its own; it gets everything from its parent.