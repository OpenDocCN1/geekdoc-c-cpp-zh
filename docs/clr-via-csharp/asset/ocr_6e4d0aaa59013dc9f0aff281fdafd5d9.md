Defining a **GetHashCode** method can be easy and straightforward. But depending on your data types and the distribution of data, it can be tricky to come up with a hashing algorithm that returns a well-distributed range of values. Here's a simple example that will probably work just fine for **Point** objects:

```
```csharp
internal sealed class Point {
    private readonly Int32 m_x, m_y;
    public override Int32 GetHashCode() {
        return m_x ^ m_y;  // m_x XOR'd with m_y
    }
    ...
}
```
```

When selecting an algorithm for calculating hash codes for instances of your type, try to follow these guidelines:

+   - Use an algorithm that gives a good random distribution for the best performance of the hash table.
+   - Your algorithm can also call the base type's **GetHashCode** method, including its return value. However, you don't generally want to call **Object**'s or **ValueType**'s **GetHashCode** method, because the implementation in either method doesn't lend itself to high-performance hashing algorithms.
+   - Your algorithm should use at least one instance field.
+   - Ideally, the fields you use in your algorithm should be immutable; that is, the fields should be initialized when the object is constructed, and they should never again change during the object's lifetime.
+   - Your algorithm should execute as quickly as possible.
+   - Objects with the same value should return the same code. For example, two **String** objects with the same text should return the same hash code value.

**System.Object**'s implementation of the **GetHashCode** method doesn't know anything about its derived type and any fields that are in the type. For this reason, **Object**'s **GetHashCode** method returns a number that is guaranteed to uniquely identify the object within the AppDomain; this number is guaranteed not to change for the lifetime of the object. After the object is garbage collected, however, its unique number can be reused as the hash code for a new object.

> **Note** If a type overrides **Object**'s **GetHashCode** method, you can no longer call it to get a unique ID for the object. If you want to get a unique ID (within an AppDomain) for an object, the FCL provides a method that you can call. In the **System.Runtime.CompilerServices** namespace, see the **RuntimeHelpers** class's public, static **GetHashCode** method that takes a reference to an **Object** as an argument. **RuntimeHelpers**' **GetHashCode** method returns a unique ID for an object even if the object's type overrides **Object**'s **GetHashCode** method. This method got its name because of its heritage, but it would have been better if Microsoft had named it something like **GetUniqueObjectID**.