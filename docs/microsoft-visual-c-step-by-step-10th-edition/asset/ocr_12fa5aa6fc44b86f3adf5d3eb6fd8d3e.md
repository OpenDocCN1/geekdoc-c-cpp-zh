specialized types of Objects. After all, a String should be able to do anything that an Object can do—that's the purpose of inheritance.

This sounds a little presumptive, however. How does the C# compiler know that you're not going to perform any type-specific operations in the code for the Compare method that might fail if you invoke the method through an interface based on a different type? If you revisit the definition of the IComparable interface, you can see the qualifier before the type parameter.

Click here to view code image

```
public interface IComparable<T>
{
    int Compare(T x, T y);
}
```

The keyword tells the C# compiler that you can either pass the T as the parameter type to methods or pass any type that derives from T. You cannot use T as the return type of any methods. This makes it possible for you to reference an object either through a generic interface based on the object type or through a generic interface based on a type that derives from the object type. Basically, if A exposes some operations, properties, or fields, and if B derives from A, then B must also expose the same operations (which might behave differently if they have been overridden), properties, and fields. Consequently, it should be safe to substitute an object of B for an object of A.

Covariance and contravariance might seem like fringe topics in the world of generics, but they are useful. For example, the List<T> generic collection (in the System.Collections.Generic namespace) uses IComparable<T> objects to implement the Sort and BinarySearch methods. A List<Object> object can contain a collection of objects of any type, so the Sort and BinarySearch methods work. Without using contravariance, these methods would need to include logic that determines the real types of the items being sorted or searched and implement a type-specific sort or search mechanism. However, unless you're a mathematician, it can be quite difficult to recall what covariance and contravariance actually do. I remember, based on the examples in this section, is as follows:

+   Covariance example If the methods in a generic interface can return strings, they can also return objects. (All strings are objects.)