# Exploring Optional Parameters 397

make a divideit method and default the parameters to 0. Someone could call it and get an undebuggable division by zero error. Setting the optional values in addall to 1 inside the method would be bad.

```
public static int add(int z, int y, int x = 0, int w = 0, int v = 1)
    //You CLEARLY don't want this
    return z + y + x + w + v;
}
```

And sometimes problems can be very subtle, use optional parameters carefully. For instance, say you have a base class and a derived class that implements the base, like this:

```
public abstract class Base
    public virtual void someFunction(int x = 0)
    {...}

public sealed class Derived : Base
    public override void someFunction(int x = 1)
    {...}
```

![](bbox=[0.875, 0.315, 0.968, 0.483])

What happens if you declare a new instance?

```
Base ex1 = new Base();
    someFunction(); //someFunction(0)

Base ex2 = new Derived();
    someFunction(); //someFunction(0)

Derived ex3 = new Derived();
    someFunction(); //someFunction(1)
```

What happened here? Depending on how you implement the classes, the default value for the optional parameter is set differently. The first example, ex1 is an implementation of Base, and the default value is 0. In the second case, ex2 is cast to a type of Derived (which is legal, since Derived is a subclass of Base), and the default value is also 0. However, in the third example, Derived is instantiated directly, and the default value is 1. This is not particularly expected behavior, though I have to admit that I am not sure what expected behavior is in a case like this. No matter how you slice, it's a gotcha and something to watch out for.

# Reference types

A reference type, as Book I discusses, variables that store a reference to actual data, instead of the data itself. Reference types are usually referred to as objects, though this is a little inaccurate since everything in the .NET Framework is an object.