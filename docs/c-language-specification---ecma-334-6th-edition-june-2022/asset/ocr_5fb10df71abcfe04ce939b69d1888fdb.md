```
```
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```
```

The type of the member a in the generic class declaration Gen is “two-dimensional array of T”, so the type of the member a in the constructed type above is “two-dimensional array of single-dimensional array of int”, or int[,][].

*end example*

Within instance function members, the type of this is the instance type (§14.3.2) of the containing declaration.

All members of a generic class can use type parameters from any enclosing class, either directly or as part of a constructed type. When a particular closed constructed type (§8.4.3) is used at run-time, each use of a type parameter is replaced with the type argument supplied to the constructed type.

Example:

```
```
class <V>
{
    public V f1;
    public C<V> f2 = null;

    public C(V x)
    {
        this.f1 = x;
        this.f2 = this;
    }
}

class Application
{
    static void Main()
    {
        <int> x1 = new <int>(1);          // Prints 1
        Console.WriteLine(x1.f1);

        <double> x2 = new C<double>(3.1415);  // Prints 3.1415
        Console.WriteLine(x2.f1);
    }
}
```
```

*end example*

# 14.3.4 Inheritance

A class inherits the members of its direct base class. Inheritance means that a class implicitly contains all members of its direct base class, except for the instance constructors, finalizers, and static constructors of the base class. Some important aspects of inheritance are:

+   - Inheritance is transitive. If C is derived from B, and B is derived from A, then C inherits the members declared in B as well as the members declared in A.
+   - A derived class extends its direct base class. A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.