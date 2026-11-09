way of manipulating the data in a more general, less type-safe fashion.

Some of the generic interfaces inherit the non-generic versions, so your class will have to implement both the generic and non-generic versions of the interfaces. For example, the generic IEnumerable<out T> interface inherits the non-generic IEnumerable interface. So if your class implements IEnumerable<out T>, your class must also implement IEnumerable.

Sometimes when integrating with other code, you may have to implement a non-generic interface because a generic version of the interface simply doesn't exist. In this case, if any of the interface's methods take or return Object, you will lose compile-time type safety, and you will get boxing with value types. You can alleviate this situation to some extent by using a technique I describe in the "Improving Compile-Time Type Safety with Explicit Interface Method Implementations" section near the end of this chapter.

The third benefit of generic interfaces is that a class can implement the same interface multiple times as long as different type parameters are used. The following code shows an example of how useful this could be:

```
```csharp
using System;

// This class implements the generic IComparable<T> interface twice
public sealed class Number: IComparable<Int32>, IComparable<String> {
    private Int32 m_val = 5;

    // This method implements IComparable<Int32>'s CompareTo
    public Int32 CompareTo(Int32 n) {
        return m_val.CompareTo(n);
    }

    // This method implements IComparable<String>'s CompareTo
    public Int32 CompareTo(String s) {
        return m_val.CompareTo(Int32.Parse(s));
    }
}

public static class Program {
    public static void Main() {
        Number n = new Number();

        // Here, I compare the value in n with an Int32 (5)
        IComparable<Int32> cInt32 = n;
        Int32 result = cInt32.CompareTo(5);

        // Here, I compare the value in n with a String ("5")
        IComparable<String> cString = n;
        result = cString.CompareTo("5");
    }
}
```
```

An interface's generic type parameters can also be marked as contravariant and covariant, which allows even more flexibility for using generic interfaces. For more about contravariance and covariance, see the "Delegate and Interface Contravariant and Covariant Generic Type Arguments" section in