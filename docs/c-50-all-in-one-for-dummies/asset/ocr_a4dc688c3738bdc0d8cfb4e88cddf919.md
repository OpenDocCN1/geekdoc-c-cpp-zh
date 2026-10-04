the TakeANote method. The method that implements TakeANote doesn’t use the override keyword. Using an interface isn’t like overriding a virtual method in classes.

Class Pen might look like this:

```
class Pen : IRecordable
{
    public void TakeANote(string note)    // Interface method implementations
    {                                     // MUST be declared public.
        // ... scribble a note with a pen ...
    }
}
```

This example fulfills two requirements: Note that the class implements IRecordable and provides a method implementation for TakeANote().

The syntax indicating that a class inherits a base class, such as ThingsThatRecord, is essentially no different from the syntax indicating that the class implements a C# interface such as IRecordable:

```
public class PDA : ThingsThatRecord ...
public class PDA : IRecordable ...
```

![](bbox=[0.12, 0.5, 0.2, 0.62])

Visual Studio can help you implement an interface. Hover the mouse pointer over the interface name in the class heading. A little underline appears underneath the first character of the interface name — it’s a Smart Tag. Move the mouse until a menu opens and choose Implement Interface <name>. Presto! A skeleton framework appears — you fill in the details.

# How to name your interface

The .NET naming convention for interfaces precedes the name with the letter I. Interface names are typically adjectives, such as IRecordable.

# Why C# includes interfaces

![](bbox=[0.12, 0.73, 0.2, 0.82])

The bottom line of interfaces is that an interface describes a capability, such as Swim Safety Training or Class A Driver’s License. As a class, I earn my IRecordable badge when I implement the TakeANote ability.

More than that, an interface is a contract. If you agree to implement every method defined in the interface, you get to claim its capability. Not only that, but a client using your class in her program is guaranteed to be able to call those methods. Implementing an interface is a promise — enforced by the compiler. (Enforcing promises through the compiler reduces errors.)