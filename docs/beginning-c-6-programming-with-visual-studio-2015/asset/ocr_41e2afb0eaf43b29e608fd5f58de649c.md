You saw behavior like this earlier in this book for simple variable types such as int. The upshot is that the two struct type variables contain different structs. The entire technique of using pointers is hidden from you in managed C# code, making your code much simpler. It is possible to access lower-level operations such as pointer manipulation in C# using unsafe code, but that is an advanced topic not covered here.

# SHALLOW COPYING VERSUS DEEP COPYING

Copying objects from one variable to another by value instead of by reference (that is, copying them in the same way as structs) can be quite complex. Because a single object can contain references to many other objects, such as field members and so on, a lot of processing can be involved. Simply copying each member from one object to another might not work because some of these members might be reference types in their own right.

The .NET Framework takes this into account. You can create a simple copy of an object where each member is copied to the new object by using the method MemberwiseClone(), inherited from System.Object. This is a protected method, but it would be easy to define a public method on an object that called this method. This copying method is known as a shallow copy, in that it doesn't take reference type members into account. This means that reference members in the new object refer to the same objects as equivalent members in the source object, which isn't ideal in many cases. If you want to create new instances of the members in question by copying the values across (rather than the references), you need to perform a deep copy.

There is an interface you can implement that enables you to deep copy in a standard way: ICloneable. If you use this interface, then you must implement the single method it contains, Clone(). This method returns a value of type System.Object. You can use whatever processing you want to obtain this object, by implementing the method body however you choose. That means you can implement a deep copy if you want to, although the exact behavior isn't mandatory, so you could perform a shallow copy if you desired. There are no rules or restrictions on what you actually return from this method, so many people recommend avoiding it. Instead, they recommend implementing your own deep-copy method. You take a closer look at this interface in Chapter 11.

# EXERCISES

# 9.1 What is wrong with the following code?

```
public sealed class MyClass
{
    // Class members.
}
public class myDerivedClass : MyClass
{
    // Class members.
}
```