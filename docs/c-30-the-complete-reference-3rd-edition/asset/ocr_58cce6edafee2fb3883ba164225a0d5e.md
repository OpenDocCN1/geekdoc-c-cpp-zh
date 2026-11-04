```
```
}
}

class Derived1 : Base {
    // Override Who() in a derived class.
    public override void Who() {
        Console.WriteLine("Who() in Derived1");
    }
}

class Derived2 : Derived1 {
    // This class also does not override Who().
}

class Derived3 : Derived2 {
    // This class does not override Who().
}

class NoOverrideDemo2 {
    static void Main() {
        Derived3 dOb = new Derived3();
        Base baseRef; // a base class reference

        baseRef = dOb;
        baseRef.Who(); // calls Derived1's Who()
    }
}
```
```

The output is shown here:

```
```text
Who() in Derived1
```
```

Here, **Derived3** inherits **Derived2**, which inherits **Derived1**, which inherits **Base**. As the output verifies, since `Who()` is not overridden by either `Derived3` or `Derived2`, it is the override of `Who()` in `Derived1` that is executed, since it is the first version of `Who()` that is found.

One other point: Properties can also be modified by the virtual keyword and overridden using override. The same is true for indexers.

# Why Overridden Methods?

Overridden methods allow C# to support runtime polymorphism. Polymorphism is essential to object-oriented programming for one reason: It allows a general class to specify methods that will be common to all of its derivatives, while allowing derived classes to define the specific implementation of some or all of those methods. Overridden methods are another way that C# implements the “one interface, multiple methods” aspect of polymorphism.

Part of the key to applying polymorphism successfully is understanding that the base classes and derived classes form a hierarchy that moves from lesser to greater specialization. Used correctly, the base class provides all elements that a derived class can use directly. Through virtual methods, it also defines those methods that the derived class can implement on its own. This allows the derived class flexibility, yet still enforces a consistent interface. Thus, by combining inheritance with overridden methods, a base class can define the general form of the methods that will be used by all of its derived classes.