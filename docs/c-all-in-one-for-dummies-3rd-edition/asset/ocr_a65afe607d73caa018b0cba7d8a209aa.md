If you want to specify that a base class has abstract virtual functions, you specify those in the class by using italics. For example, Figure 3-4 shows a base class called Person. This is an abstract class because it contains an abstract virtual function: work(). The function is abstract virtual because it is in italics. (And thus the class itself is virtual. Remember that a class that has at least one abstract virtual function is therefore itself abstract.)

![](bbox=[0.12, 0.25, 0.45, 0.43])

The two classes derived from Person, BankRobber and MiddleManager (we just thought those made for an interesting combination) each override the work() function. Therefore, they are *not* abstract. And thus you can create instances of BankRobber and MiddleManager.

![](bbox=[0.12, 0.56, 0.18, 0.63])

You may have noticed that, so far, we have not mentioned a way to specify a virtual function in UML. You can specify a member function as abstract, but what about plain old virtual? You can't. The virtual keyword is unique to C++, and the word simply means that you can override a function. So how do you specify virtual? Many CASE tools include an option in the model that lets you specify a member function as virtual.

# Aggregating and composing classes

When you associate two classes but not by inheritance, you can do it in two common ways: composition and aggregation. Consider the LaserPrinter class and its association with the TonerCartridge class. A toner cartridge is a fundamental part of a laser printer, but a toner cartridge can't be inside more than one laser printer at a time. This is composition.

Aggregation, on the other hand, refers to two objects that are more loosely connected. In an office, you may find hundreds of computers and a dozen or so laser printers. The laser printers can function on their own, and they interact with many different computers. Meanwhile, the computers can each interact with many different laser printers. This is a much looser connection; this is aggregation.