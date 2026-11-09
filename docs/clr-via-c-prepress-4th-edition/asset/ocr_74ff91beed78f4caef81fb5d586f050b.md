# Generic Interfaces

C#’s and the CLR’s support of generic interfaces offers many great features for developers. In this section, I’d like to discuss the benefits offered when using generic interfaces.

First, generic interfaces offer great compile-time type safety. Some interfaces (such as the non-generic IComparable interface) define methods that have Object parameters or return types. When code calls these interface methods, a reference to an instance of any type can be passed. But this is usually not desired. The following code demonstrates:

```
```csharp
private void SomeMethod1() {
    Int32 x = 1, y = 2;
    IComparable c = x;

    // CompareTo expects an Object; passing y (an Int32) is OK
    c.CompareTo(y);     // y is boxed here

    // CompareTo expects an Object; passing "2" (a String) compiles
    // but an ArgumentException is thrown at runtime
    c.CompareTo("2");
}
```
```

Obviously, it is preferable to have the interface method strongly typed, and this is why the FCL includes a generic IComparable<T> interface. Here is the new version of the code revised by using the generic interface:

```
```csharp
private void SomeMethod2() {
    Int32 x = 1, y = 2;
    IComparable<Int32> c = x;

    // CompareTo expects an Int32; passing y (an Int32) is OK
    c.CompareTo(y);     // y is not boxed here

    // CompareTo expects an Int32; passing "2" (a String) results
    // in a compiler error indicating that String cannot be cast to an Int32
    c.CompareTo("2");   // Error
}
```
```

The second benefit of generic interfaces is that much less boxing will occur when working with value types. Notice in SomeMethod1 that the non-generic IComparable interface’s CompareTo method expects an Object; passing y (an Int32 value type) causes the value in y to be boxed. However, in SomeMethod2, the generic IComparable<int> interface’s CompareTo method expects an Int32; passing y causes it to be passed by value, and no boxing is necessary.

**Note** The FCL defines non-generic and generic versions of the IComparable, ICollection, IList, and IDictionary interfaces, as well as some others. If you are defining a type, and you want to implement any of these interfaces, you should typically implement the generic versions of these interfaces. The non-generic versions are in the FCL for backward compatibility to work with code written before the .NET Framework supported generics. The non-generic versions also provide users a