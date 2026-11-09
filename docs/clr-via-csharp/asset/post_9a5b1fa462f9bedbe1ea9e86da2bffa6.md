
operands to **Object** first) because one of the operands' types could overload the == operator, giving it semantics other than identity.

As you can see, the .NET Framework has a very confusing story when it comes to object equality and identity. By the way, **System.ValueType** (the base class of all value types) does override **Object's Equals** method and is correctly implemented to perform a value equality check (not an identity check). Internally, **ValueType's Equals** is implemented this way:

- 1. If the **obj** argument is **null**, return **false**.
- 2. If the **this** and **obj** arguments refer to objects of different types, return **false**.
- 3. For each instance field defined by the type, compare the value in the **this** object with the value in the **obj** object by calling the field's **Equals** method. If any fields are not equal, return **false**.
- 4. Return **true**. **Object's Equals** method is not called by **ValueType's Equals** method.

Internally, **ValueType's Equals** method uses reflection (covered in Chapter 23, "Assembly Loading and Reflection") to accomplish step #3 above. Since the CLR's reflection mechanism is slow, when defining your own value type, you should override **Equals** and provide your own implementation to improve the performance of value equality comparisons that use instances of your type. Of course, in your own implementation, do not call **base.Equals**.

When defining your own type, if you decide to override **Equals**, you must ensure that it adheres to the four properties of equality:

- **Equals** must be reflexive; that is, **x.Equals(x)** must return **true**.
- **Equals** must be symmetric; that is, **x.Equals(y)** must return the same value as **y.Equals(x)**.
- **Equals** must be transitive; that is, if **x.Equals(y)** returns **true** and **y.Equals(z)** returns **true**, then **x.Equals(z)** must also return **true**.
- **Equals** must be consistent. Provided that there are no changes in the two values being compared, **Equals** should consistently return **true** or **false**.

If your implementation of **Equals** fails to adhere to all of these rules, your application will behave in strange and unpredictable ways.

When overriding the **Equals** method, there are a few more things that you'll probably want to do:

- Have the type implement the **System.IEquatable&lt;T&gt;** interface's **Equals** method. This generic interface allows you to define a type-safe **Equals** method. Usually, you'll implement the **Equals** method that takes an **Object** parameter to internally call the type-safe **Equals** method.
- **Overload the == and != operator methods.** Usually, you'll implement these operator methods to internally call the type-safe **Equals** method.

Furthermore, if you think that instances of your type will be compared for the purposes of sorting, you'll want your type to also implement **System.IComparable**'s **CompareTo** method and **System.IComparable&lt;T&gt;**'s type-safe **CompareTo** method. If you implement these methods, you'll also want to overload the various comparison operator methods (&lt;, &lt;=, &gt;, &gt;=) and implement these methods internally to call the type-safe **CompareTo** method.

## Object Hash Codes

The designers of the FCL decided that it would be incredibly useful if any instance of any object could be placed into a hash table collection. To this end, **System.Object** provides a virtual **GetHashCode** method so that an **Int32** hash code can be obtained for any and all objects.

If you define a type and override the **Equals** method, you should also override the **GetHashCode** method. In fact, Microsoft's C# compiler emits a warning if you define a type that overrides **Equals** without also overriding **GetHashCode**. For example, compiling the following type yields this warning: "warning CS0659: 'Program' overrides Object.Equals(Object o) but does not override Object.GetHashCode()".

```csharp
public sealed class Program {
   public override Boolean Equals(Object obj) { ... }
}
```

The reason why a type that defines **Equals** must also define **GetHashCode** is that the implementation of the **System.Collections.Hashtable** type, the **System.Collections.Generic.Dictionary** type, and some other collections require that any two objects that are equal must have the same hash code value. So if you override **Equals**, you should override **GetHashCode** to ensure that the algorithm you use for calculating equality corresponds to the algorithm you use for calculating the object's hash code.

Basically, when you add a key/value pair to a collection, a hash code for the key object is obtained first. This hash code indicates which "bucket" the key/value pair should be stored in. When the collection needs to look up a key, it gets the hash code for the specified key object. This code identifies the "bucket" that is now searched sequentially, looking for a stored key object that is equal to the specified key object. Using this algorithm of storing and looking up keys means that if you change a key object that is in a collection, the collection will no longer be able to find the object. If you intend to change a key object in a hash table, you should remove the original object/value pair, modify the key object, and then add the new key object/value pair back into the hash table.

Defining a **GetHashCode** method can be easy and straightforward. But depending on your data types and the distribution of data, it can be tricky to come up with a hashing algorithm that returns a well-distributed range of values. Here's a simple example that will probably work just fine for **Point** objects:

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
- Your algorithm can also call the base type's **GetHashCode** method, including its return value. However, you don't generally want to call **Object**'s or **ValueType**'s **GetHashCode** method, because the implementation in either method doesn't lend itself to high-performance hashing algorithms.
- Your algorithm should use at least one instance field.
- Ideally, the fields you use in your algorithm should be immutable; that is, the fields should be initialized when the object is constructed, and they should never again change during the object's lifetime.
- Your algorithm should execute as quickly as possible.
- Objects with the same value should return the same code. For example, two **String** objects with the same text should return the same hash code value.

**System.Object**'s implementation of the **GetHashCode** method doesn't know anything about its derived type and any fields that are in the type. For this reason, **Object**'s **GetHashCode** method returns a number that is guaranteed to uniquely identify the object within the AppDomain; this number is guaranteed not to change for the lifetime of the object. After the object is garbage collected, however, its unique number can be reused as the hash code for a new object.

> **Note** If a type overrides **Object**'s **GetHashCode** method, you can no longer call it to get a unique ID for the object. If you want to get a unique ID (within an AppDomain) for an object, the FCL provides a method that you can call. In the **System.Runtime.CompilerServices** namespace, see the **RuntimeHelpers** class's public, static **GetHashCode** method that takes a reference to an **Object** as an argument. **RuntimeHelpers**' **GetHashCode** method returns a unique ID for an object even if the object's type overrides **Object**'s **GetHashCode** method. This method got its name because of its heritage, but it would have been better if Microsoft had named it something like **GetUniqueObjectID**.
