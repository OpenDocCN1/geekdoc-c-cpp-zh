class contains only static members and isn't intended to be instantiated, adding an empty private instance constructor will prevent instantiation. For example:

```
public class Trig
{
    private Trig() {}    // Prevent instantiation
    public const double PI = 3.14159265358979323846;
    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Tan(double x) {...}
}
```

The Trig class groups related methods and constants, but is not intended to be instantiated. Therefore it declares a single empty private instance constructor. At least one instance constructor must be declared to suppress the automatic generation of a default constructor.

> BILL WAGNER If a class is not meant to be instantiated, it would be better to make it a static class. However, if you are implementing the singleton pattern, a private constructor ensures that only your factory method can create the singleton object.

> JOSEPH ALBAHARI If the goal is simply to prevent instantiation, an easier option is to declare the class as static.

Private constructors also have a subtler purpose, which relies on the fact that a private constructor can still be invoked from static members of the same class. Sometimes exposing static methods as the only public means of instantiating a class offers certain advantages. For example, with immutable objects, this approach can be used to implement a transparent object caching system.

# 10.11.6 Optional Instance Constructor Parameters

The this(...) form of constructor initializer is commonly used in conjunction with overloading to implement optional instance constructor parameters. In the example

```
class Text
{
    public Text(): this(0, 0, null) {}
    public Text(int x, int y): this(x, y, null) {}
    public Text(int x, int y, string s) {
        // Actual constructor implementation
    }
}
```