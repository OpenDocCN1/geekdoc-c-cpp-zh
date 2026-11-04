Here's the initializer business. Both _accountNumber and _balance are assigned a value as part of their declaration, which has the same effect as a constructor but without having to do the work in it.

Be clear about exactly what's happening. You may think that this statement sets _balance to 0.0 right now. However, _balance exists only as a part of an object. Thus the assignment isn't executed until a BankAccount object is created. In fact, this assignment is executed every time an object is created.

Note that the static data member _nextAccountNumber is initialized the first time the BankAccount class is accessed — as your tour in the debugger showed, that's the first time you access any method or property of the object owning the static data member, including the constructor.

After the static member is initialized, it isn't reinitialized every time you construct a BankAccount instance. That's different from the nonstatic members.

Initializers are executed in the order of their appearance in the class declaration. If C# encounters both initializers and a constructor, the initializers are executed before the body of the constructor.

![](bbox=[0.1, 0.47, 0.22, 0.66])

# Seeing that construction stuff with initializers

In the DemonstrateCustomConstructor program, move the call new MyOtherObject() from the MyObject constructor to the declaration itself, as follows (see the bold text), modify the second WriteLine() statement as shown, and then rerun the program:

```
public class MyObject
{
    // This member is a property of the class (it's static).
    private static MyOtherObject _staticObj = new MyOtherObject();
    // This member is a property of each instance.
    private MyOtherObject _dynamicObj = new MyOtherObject(); // <-- Here.
    public MyObject()
    {
        Console.WriteLine("MyObject constructor starting");
        Console.WriteLine("Both data members initialized before this constructor");
        // _dynamicObj construction was here, now moved up.
        Console.WriteLine("MyObject constructor ending");
    }
}
```

Compare the following output from this modified program with the output from its predecessor, DemonstrateCustomConstructor:

```
Main() starting
Creating a local MyObject in Main():
MyOtherObject constructing
MyOtherObject constructing
```