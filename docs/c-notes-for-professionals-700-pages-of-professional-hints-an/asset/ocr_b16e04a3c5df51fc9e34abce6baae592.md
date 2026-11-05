View Demo

Calling a different constructor of the base class is done by placing : base(args) between the constructor's signature and its body:

```
```csharp
public class Mammal : Animal
{
    public Mammal(string name) : base(name)
    {
        Console.WriteLine(name + " is a mammal.");
    }
}
```
```

Calling new Mammal("George the Cat") will now print:

> George the Cat gets born.
> George the Cat is a mammal.

View Demo

# Section 39.7: Finalizers on derived classes

When an object graph is finalized, the order is the reverse of the construction. E.g. the super-type is finalized before the base-type as the following code demonstrates:

```
```csharp
class TheBaseClass
{
    ~TheBaseClass()
    {
        Console.WriteLine("Base class finalized!");
    }
}

class TheDerivedClass : TheBaseClass
{
    ~TheDerivedClass()
    {
        Console.WriteLine("Derived class finalized!");
    }
}

//Don't assign to a variable
//to make the object unreachable
new TheDerivedClass();

//Just to make the example work;
//this is otherwise NOT recommended!
GC.Collect();

//Derived class finalized!
//Base class finalized!
```
```

# Section 39.8: Exceptions in static constructors

If a static constructor throws an exception, it is never retried. The type is unusable for the lifetime of the AppDomain. Any further usages of the type will raise a TypeInitializationException wrapped around the original