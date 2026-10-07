# Chapter 14 Reusing Code in C++

```
class Singer : virtual public Worker { ... };
class Waiter : virtual public Worker { ... };
class SingingWaiter : public Singer, public Waiter { ... };
```

![](bbox=[0.223, 0.185, 0.833, 0.463])

Let's look at some questions you might have:

+   - Why the term virtual?
- Why we don't dispense with declaring base classes virtual and make virtual behavior the norm for MI?
- Are there any catches?

First, why the term virtual? After all, there doesn't seem to be an obvious connection between the concepts of virtual functions and virtual base classes. There is pressure from the C++ community to resist the introduction of new keywords. It would be awkward, if a new keyword corresponded to the name of some important function or variable in a major program. So C++ merely recycled the keyword virtual for the new facility—a bit of keyword overloading.

Next, why we dispense with declaring base classes virtual and make virtual behavior the norm for MI? First, there are cases in which you might make multiple copies of a base. Second, making a base class virtual requires that a program do some additional accounting, and you shouldn't have to pay for that facility if you don't need it. Third, there are the disadvantages presented in the next paragraph.

Finally, are there catches? Yes. Making virtual base classes work requires adjustments to C++ rules, and you have to code some things differently. Also using virtual base classes may involve changing existing code. For example, adding the singingWaiter class to the