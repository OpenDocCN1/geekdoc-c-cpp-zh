perhaps other kinds of clocks as well. We'll end up writing a separate class definition for each different type of clock. Even though all of these have similar or identical constructors and member functions, we'll still end up repeating the member function implementations for each different kind of clock.

The solution to the clock problem is a new concept, called derived classes, described here:

> # Derived Classes
> 
> Derived classes use a concept called inheritance. In particular, once we have a class, we can then declare new classes that contain all of the members of the original class—plus any extras that you want to throw in. This new class is called a **derived class** of the original class. The original class is called the **base class**. And the members that the derived class receives from its base class are called **inherited members**.

# How to Declare a Derived Class

In the definition of the derived class, the name of the derived class is followed by a single colon, the keyword `public`, and then the name of the base class. For example, suppose that we want to declare a derived class `cuckoo_clock` using the existing `Clock` class as the base class. The beginning of the `cuckoo_clock` class definition would then look like this:

```
class cuckoo_clock : public clock
{
    ...
}
```

This definition indicates that every `cuckoo_clock` is also an ordinary clock. The primary consequence is that all of the public members of an ordinary clock are immediately available as public members of a `cuckoo_clock`. These members are said to be **inherited** from the clock.

public base class versus private base class

In the clock example, we used the keyword `public`, which creates a **public base class**. An alternative is to use the keyword `private` instead of `public`, resulting in a **private base class**. With a private base class, all of the public members of an ordinary clock are immediately available as public members of a `cuckoo_clock`. In both cases—public base class or private base class—it is the public members of the clock that are accessible to the `cuckoo_clock`. In some sense, the private members of the clock are also present in a `cuckoo_clock`—they must be present because some of the public members make use of the private members. But these private members cannot be accessed directly in a `cuckoo_clock`, not even by the programmer who implements a `cuckoo_clock`.

This is why we did not even list the clock's private members in Figure 14.1.

protected members

For future reference, you should know that there is a third kind of member called a **protected member**. In most respects, a protected member is just like a private member, but the programmer of a derived class has direct access to protected members. We'll use protected members in Section 14.3.