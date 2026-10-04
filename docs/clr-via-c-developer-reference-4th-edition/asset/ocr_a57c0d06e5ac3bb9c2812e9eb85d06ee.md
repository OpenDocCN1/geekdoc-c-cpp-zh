Now the previous CompareTo method will call the CompareTo method in Base. But sometimes you cannot remove the interface from the type because you want the derived type to implement an interface method. The best way to fix this is for the Base class to provide a virtual method in addition to the interface method it has chosen to implement explicitly. The Derived class can override the virtual method. Here is the correct way to define the Base and Derived classes.

```
internal class Base : IComparable {
```

```
// Explicit Interface Method Implementation
Int32 CompareTo(object o) {
Console.WriteLine("Base's IComparable CompareTo");
return CompareTo(o); // This now calls the virtual method
}
```

```
// Virtual method for derived classes (this method could have any name)
public virtual Int32 CompareTo(object o) {
Console.WriteLine("Base's virtual CompareTo");
return 0;
}
```

```
internal sealed class Derived : Base, IComparable {
```

```
// A public method that is also the interface implementation
public override Int32 CompareTo(object o) {
Console.WriteLine("Derived's CompareTo");
```

```
// Now, we can call Base's virtual method
return base.CompareTo(o);
```

Note that I have defined the virtual method above as a public method, but in some cases, you will prefer to make the method protected instead of public, but that will necessitate other changes. This discussion clearly shows that EIMIs should be used with great care. When many developers learn about EIMIs, they'll think they're cool and start using them whenever possible. Don't do this! EIMIs are useful in some circumstances, but you should avoid them whenever possible because they make using a type much more difficult.

# Design: Base Class or Interface?

I often hear the question, "Should I design a base type or an interface?" The answer isn't always clear-cut. Here are some guidelines that might help you:

+   - IS-A vs. CAN-DO relationship A type can inherit only one implementation. The derived type can't claim an IS-A relationship with the base type; don't use a base type; use an interface. Interfaces imply a CAN-DO relationship. If the CAN-DO functionality appears to belong to various object types, use an interface. For example, a type can convert instances of itself