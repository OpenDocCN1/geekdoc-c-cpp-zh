# C# During Its Abstract Period 329

```
// SubClass1 -- Concrete implementation of AbstractBaseClass
public class SubClass1 : AbstractBaseClass
{
    override public void Output(string source) // Or "public override"
    string s = source.ToUpper();
    Console.WriteLine("Call to SubClass1.Output(from (0*)", s);
}

// SubClass2 -- Another concrete implementation of AbstractBaseClass
public class SubClass2 : AbstractBaseClass
{
    override void Output(string source) // Or 'override public'
    string s = source.ToLower();
    Console.WriteLine("Call to SubClass2.Output(from (0*)", s);
}

class Program
{
    public static void Test(AbstractBaseClass ba)
    {
        ba.Output("Test");
    }

    public static void Main(string[] strings)
    {
        // You cannot create an AbstractClass object because it's
        // abstract. C# generates a compile-time error if you
        // uncomment the following line:
        // AbstractClass ba = new AbstractClass();
        // Repeat the experiment with SubClass1;
        SubClass1 sc1 = new SubClass1();
        Test(sc1);

        // And finally, a SubClass2 object
        Console.WriteLine("increating a SubClass2 object");
        SubClass2 sc2 = new SubClass2();
        Test(sc2);

        // Wait for user to acknowledge.
        Console.WriteLine("Press Enter to terminate...");
        Console.Read();
    }
}
```

The first class defines the AbstractBaseClass with a single abstract Output() method. Because it's declared abstract, Output() has no implementation — that is, no method body.

Two classes inherit from AbstractBaseClass: SubClass1 and SubClass2. Both are concrete classes because they override the Output() method with "real" methods and contain no abstract methods.

A class can be declared abstract whether it has abstract members or; however, a class can be concrete only when all abstract methods in any base class above it have been overridden with full methods.

![](bbox=[0.135, 0.835, 0.195, 0.915])

Poly-what-ism?