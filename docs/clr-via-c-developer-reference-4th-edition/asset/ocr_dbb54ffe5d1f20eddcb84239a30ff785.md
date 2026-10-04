Now, let me reprite the generic SimpleType so that you can see an observable difference.

```
internal sealed class SimpleType : IDisposable {
public void Dispose() { Console.WriteLine("Dispose"); }
void IDisposable.Dispose() { Console.WriteLine("IDisposable Dispose"); }
}
```

Without changing the Main method earlier, if we just recompile and rerun the program, the

```
public Dispose
IDisposable Dispose
```

In#, when you use the prefix of a method with the name of the interface that defines the method (IDisposable.Dispose as in this example), you are creating an explicit interface implementation (EIIM). Note that when you define an explicit interface method in C#, you are not allowed to specify any accessibility (such as public or private). However, when the compiler generates the metadata for the method, its accessibility is to private, preventing any code using an instance of the class from simply calling the interface method. The only way to call the interface method is through a variable of the interface's type.

Also note that an EIIM method cannot be marked as virtual and therefore cannot be overridden. This is because the EIIM method is not part of the type's object model; it is a way of attaching an interface (set of behaviors or methods) onto a type without making the behaviors/methods obvious. If all of this seems a bit kludgy to you, you are understanding correctly—this is all a bit kludgy. Later in this chapter, I'll show some valid reasons for using EIIMs.

# Generic Interfaces

C# and the CLR's support of generic interfaces offers many great features for developers. In this section, I'd like to discuss the benefits offered when using generic interfaces.

First, generic interfaces offer great compile-time safety. Some interfaces (such as the non-generic IComparable interface) define methods that have Object parameters or return types. When code calls these interface, a reference to an instance of any type can be passed. But this is usually not desired. The following code demonstrates.

```
private void SomeMethod() {
Int32 x = 1, y = 2;
IComparable c = x;
```

```
// Compare expects an Object, passing "2" (a String) compiles
// c.CompareTo(y);      // y is boxed here
```

```
// Compare expects an Object, passing "2" (a String) compiles
// but an ArgumentException is thrown at runtime
c.CompareTo("2");
```