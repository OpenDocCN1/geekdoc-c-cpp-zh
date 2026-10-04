# Chapter 5: Holding a Class Responsible

# In This Chapter

+   ✓ Letting the class protect itself through access control

+   ✓ Introducing the property, a specialized kind of method

+   ✓ Allowing an object to initialize itself via the constructor

+   ✓ Defining multiple constructors for the same class

+   ✓ Constructing static or class members

A class must be held responsible for its actions. Just as a microwave oven shouldn’t burst into flames if you press the wrong key, a class shouldn’t allow itself to roll over and die when presented with incorrect data.

To be held responsible for its actions, a class must ensure that its initial state is correct and then control its subsequent state so that it remains valid. C# provides both these capabilities.

# Restricting Access to Class Members

Simple classes define all their members as public. Consider a BankAccount program that maintains a balance data member to retain the balance in each account. Making that data member public puts everyone on the honor system.

I don’t know about your bank, but my bank isn’t nearly so forthcoming as to leave a pile of money and a register for me to mark down every time I add money to or take money away from the pile. After all, I may forget to mark my withdrawals in the register.

Controlling access avoids little mistakes, such as forgetting to mark a withdrawal here or there, and manages to avoid some truly big mistakes with withdrawals.

I know exactly what you procedural types out there are thinking: “Just make a rule that other classes can’t access the balance data member directly, and that’s that.” That approach may work in theory, but in practice it never does. People start out with good intentions (like my intentions to work

![](bbox=[0.12, 0.85, 0.2, 0.95])