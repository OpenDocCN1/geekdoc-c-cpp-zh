
```csharp
}

public void Change(Int32 x, Int32 y) {
    m_x = x; m_y = y;
}

public override String ToString() {
    return String.Format("({0}, {1})", m_x.ToString(), m_y.ToString());
}

public sealed class Program {
    public static void Main() {
        Point p = new Point(1, 1);

        Console.WriteLine(p);

        p.Change(2, 2);
        Console.WriteLine(p);

        Object o = p;
        Console.WriteLine(o);

        ((Point) o).Change(3, 3);
        Console.WriteLine(o);
    }
}
```

Very simply, Main creates an instance (p) of a Point value type on the stack and sets its m_x and m_y fields to 1. Then, p is boxed before the first call to WriteLine, which calls ToString on the boxed Point and (1, 1) is displayed as expected. Then, p is used to call the Change method, which changes the values of p's m_x and m_y fields on the stack to 2. The second call to WriteLine requires p to be boxed again and displays (2, 2), as expected.

Now, p is boxed a third time, and o refers to the boxed Point object. The third call to WriteLine again shows (2, 2), which is also expected. Finally, I want to call the Change method to update the fields in the boxed Point object. However, Object (the type of the variable o) doesn't know anything about the Change method, so I must first cast o to a Point. Casting o to a Point unboxes o and copies the fields in the boxed Point to a temporary Point on the thread's stack! The m_x and m_y fields of this temporary point are changed to 3 and 3, but the boxed Point isn't affected by this call to Change. When WriteLine is called the fourth time, (2, 2) is displayed again. Many developers do not expect this.

Some languages, such as C++/CLI, let you change the fields in a boxed value type, but C# does not. However, you can fool C# into allowing this by using an interface. The following code is a modified version of the previous code:

```csharp
using System;

// Interface defining a Change method
internal interface IChangeBoxedPoint {
```

```csharp
// If both references point to the same object,
// they must have the same value.
if (this == obj) return true;

// Assume that the objects do not have the same value.
return false;
}
}
```

At first, this seems like a reasonable default implementation of `Equals`: it returns true if the `this` and `obj` arguments refer to the same exact object. This seems reasonable because `Equals` knows that an object must have the same value as itself. However, if the arguments refer to different objects, `Equals` can’t be certain if the objects contain the same values, and therefore, `false` is returned. In other words, the default implementation of `Object`’s `Equals` method really implements identity, not value equality.

Unfortunately, as it turns out, `Object`’s `Equals` method is not a reasonable default, and it should have never been implemented this way. You immediately see the problem when you start thinking about class inheritance hierarchies and how to properly override `Equals`. Here is how to properly implement an `Equals` method internally:

- 1. If the `obj` argument is null, return `false` because the current object identified by `this` is obviously not null when the nonstatic `Equals` method is called.
- 2. If the `this` and `obj` arguments refer to the same object, return `true`. This step can improve performance when comparing objects with many fields.
- 3. If the `this` and `obj` arguments refer to objects of different types, return `false`. Obviously, checking if a `String` object is equal to a `FileStream` object should result in a false result.
- 4. For each instance field defined by the type, compare the value in the `this` object with the value in the `obj` object. If any fields are not equal, return `false`.
- 5. Call the base class’s `Equals` method so it can compare any fields defined by it. If the base class’s `Equals` method returns `false`, return `false`; otherwise, return `true`.

So Microsoft should have implemented `Object`’s `Equals` like this:

```csharp
public class Object {
    public virtual Boolean Equals(Object obj) {
        // The given object to compare to can't be null
        if (obj == null) return false;

        // If objects are different types, they can't be equal.
        if (this.GetType() != obj.GetType()) return false;

        // If objects are same type, return true if all of their fields match
        // Since System.Object defines no fields, the fields match
        return true;
    }
}
```

- Equals must be transitive; that is, if x.Equals(y) returns true and y.Equals(z) returns true, then x.Equals(z) must also return true.
- Equals must be consistent. Provided that there are no changes in the two values being compared, Equals should consistently return true or false.

If your implementation of Equals fails to adhere to all of these rules, your application will behave in strange and unpredictable ways.

When overriding the Equals method, there are a few more things that you'll probably want to do:

- Have the type implement the System.IEquatable<T> interface's Equals method. This generic interface allows you to define a type-safe Equals method. Usually, you'll implement the Equals method that takes an Object parameter to internally call the type-safe Equals method.
- Overload the == and != operator methods. Usually, you'll implement these operator methods to internally call the type-safe Equals method.

Furthermore, if you think that instances of your type will be compared for the purposes of sorting, you'll want your type to also implement System.IComparable's CompareTo method and System.IComparable<T>'s type-safe CompareTo method. If you implement these methods, you'll also want to overload the various comparison operator methods (<, <=, >, >=) and implement these methods internally to call the type-safe CompareTo method.

## Object Hash Codes

The designers of the FCL decided that it would be incredibly useful if any instance of any object could be placed into a hash table collection. To this end, System.Object provides a virtual GetHashCode method so that an Int32 hash code can be obtained for any and all objects.

If you define a type and override the Equals method, you should also override the GetHashCode method. In fact, Microsoft's C# compiler emits a warning if you define a type that overrides Equals without also overriding GetHashCode. For example, compiling the following type yields this warning: "warning CS0659: 'Program' overrides Object.Equals(object o) but does not override Object.GetHashCode()".

```csharp
public sealed class Program {
    public override Boolean Equals(Object obj) { ... }
}
```

The reason why a type that defines Equals must also define GetHashCode is that the implementation of the System.Collections.Hashtable type, the System.Collections.Generic.Dictionary type, and some other collections require that any two objects that are equal must have the same hash code value. So if you override Equals, you should override GetHashCode to ensure that the algorithm you use for calculating equality corresponds to the algorithm you use for calculating the object’s hash code.

Basically, when you add a key/value pair to a collection, a hash code for the key object is obtained first. This hash code indicates which “bucket” the key/value pair should be stored in. When the collection needs to look up a key, it gets the hash code for the specified key object. This code identifies the “bucket” that is now searched sequentially, looking for a stored key object that is equal to the specified key object. Using this algorithm of storing and looking up keys means that if you change a key object that is in a collection, the collection will no longer be able to find the object. If you intend to change a key object in a hash table, you should remove the original key/value pair, modify the key object, and then add the new key/value pair back into the hash table.

Defining a GetHashCode method can be easy and straightforward. But depending on your data types and the distribution of data, it can be tricky to come up with a hash algorithm that returns a well-distributed range of values. Here’s a simple example that will probably work just fine for Point objects:

```csharp
internal sealed class Point {
    private readonly Int32 m_x, m_y;
    public override Int32 GetHashCode() {
        return m_x ^ m_y;  // m_x XOR'd with m_y
    }
    ...
}
```

When selecting an algorithm for calculating hash codes for instances of your type, try to follow these guidelines:

- Use an algorithm that gives a good random distribution for the best performance of the hash table.
- Your algorithm can also call the base type’s GetHashCode method, including its return value. However, you don’t generally want to call Object’s or ValueType’s GetHashCode method, because the implementation in either method doesn’t lend itself to high-performance hashing algorithms.
- Your algorithm should use at least one instance field.
- Ideally, the fields you use in your algorithm should be immutable; that is, the fields should be initialized when the object is constructed, and they should never again change during the object’s lifetime.
- Your algorithm should execute as quickly as possible.
- Objects with the same value should return the same code. For example, two String objects with the same text should return the same hash code value.

System.Object’s implementation of the GetHashCode method doesn’t know anything about its derived type and any fields that are in the type. For this reason, Object’s GetHashCode method
