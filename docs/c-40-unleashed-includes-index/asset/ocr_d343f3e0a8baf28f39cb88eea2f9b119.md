![](bbox=[0.06, 0.1, 0.78, 0.35])

FIGURE 10.15 An extension method showing up in IntelliSense.

Notice that another Reverse extension method seems to exist on System.String. In fact, this is an extension method on the generic IEnumerable<T> interface type, which is defined as part of the Standard Query Operators of LINQ. Every string is a sequence of characters, and hence System.String implements the IEnumerable<char> interface. The Reverse operator in LINQ can operate on every sequence (of any type T) and return the sequence in reverse.

# STATIC CLASSES

Notice that extension methods are defined in static classes, which is a requirement enforced by the compiler. Static classes were introduced in C# 2.0 to guard against creation of unusable classes that result from forgetting to mark a method as static. Before C# 2.0, to declare a class with only static utility methods, the following pattern was used:

```
class Helpers
{
    private Helpers() {}
    public static void Bar() { ... }
    ...
}
```

By defining a private instance constructor (see Chapter 12), no one can ever create an instance of the helper class, which is clearly the right thing to do because all methods on the class are static and hence don't need an instance to operate on. However, mistakes in definitions of such types weren't caught, in particular when someone added a method and forgot to mark it as static:

```
class Helpers
{
    private Helpers() {}
    public static void Bar() { ... }
    public void Foo() { ... }    // Oops, forgot to mark as static
    ...
}
```