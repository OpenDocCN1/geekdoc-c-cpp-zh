
GetHashCode() is also a good practice when you are using it as a key into a hash table collection (System.Collections.Hashtable and System.Collections.Generic.Dictionary, for example).

The purpose of the hash code is to efficiently balance a hash table by generating a number that corresponds to the value of an object. Here are some implementation principles for a good GetHashCode() implementation.

- Required: Equal objects must have equal hash codes (if a.Equals(b), then a.GetHashCode() == b.GetHashCode()).
- Required: GetHashCode()'s returns over the life of a particular object should be constant (the same value), even if the object's data changes. In many cases, you should cache the method return to enforce this.
- Required: GetHashCode() should not throw any exceptions; GetHashCode() must always successfully return a value.
- Performance: Hash codes should be unique whenever possible. However, since hash code returns only an int, there has to be an overlap in hash codes for objects that have potentially more values than an int can hold—virtually all types. (An obvious example is long, since there are more possible long values than an int could uniquely identify.)
- Performance: The possible hash code values should be distributed evenly over the range of an int. For example, creating a hash that doesn't consider the fact that distribution of a string in Latin-based languages primarily centers on the initial 128 ASCII characters would result in a very uneven distribution of string values and would not be a strong GetHashCode() algorithm.
- Performance: GetHashCode() should be optimized for performance. GetHashCode() is generally used in Equals() implementations to short-circuit a full equals comparison if the hash codes are different. As a result, it is frequently called when the type is used as a key type in dictionary collections.
- Performance: Small differences between two objects should result in large differences between hash code values—ideally, a 1-bit difference in the object results in around 16 bits of the hash code changing, on average. This helps ensure that the hash table remains balanced no matter how it is “bucketing” the hash values.

- Security: It should be difficult for an attacker to craft an object that has a particular hash code. The attack is to flood a hash table with large amounts of data that all hash to the same value. The hash table implementation then becomes O(n) instead of O(1), resulting in a possible denial-of-service attack.

Consider the GetHashCode() implementation for the Coordinate type shown in Listing 9.2.

### Listing 9.2: Implementing GetHashCode()

```csharp
public struct Coordinate
{
    public Coordinate(Longitude longitude, Latitude latitude)
    {
        _Longitude = longitude;
        _Latitude = latitude;
    }

    public Longitude Longitude { get { return _Longitude; } }
    private readonly Longitude _Longitude;

    public Latitude Latitude { get { return _Latitude; } }
    private readonly Latitude _Latitude;

    public override int GetHashCode()
    {
        int hashCode = Longitude.GetHashCode();
        // As long as the hash codes are not equal
        if(Longitude.GetHashCode() != Latitude.GetHashCode())
        {
            hashCode ^= Latitude.GetHashCode(); // eXclusive OR
        }
        return hashCode;
    }
}
// ...
}
```

Generally, the key is to use the XOR operator over the hash codes from the relevant types, and to make sure the XOR operands are not likely to be close or equal—or else the result will be all zeroes. (In those cases where the operands are close or equal, consider using bitshifts and adds instead.) The alternative operands, AND and OR, have similar restrictions, but the restrictions occur more frequently. Applying AND multiple times tends toward all 0 bits, and applying OR tends toward all 1 bits.

For finer-grained control, split larger-than-int types using the shift operator. For example, GetHashCode() for a long called value is implemented as follows:

```csharp
int GetHashCode() { return ((int)value ^ (int)(value >> 32)); };
```

Also, note that if the base class is not object, then base.GetHashCode() should be included in the XOR assignment.

Finally, Coordinate does not cache the value of the hash code. Since each field in the hash code calculation is readonly, the value can't change. However, implementations should cache the hash code if calculated values could change or if a cached value could offer a significant performance advantage.

## Overriding Equals()

Overriding Equals() without overriding GetHashCode() results in a warning such as that shown in Output 9.1.

### OUTPUT 9.1:

```
warning CS0659: '<Class Name>' overrides Object.Equals(object o) but does not override Object.GetHashCode()
```

Generally, programmers expect overriding Equals() to be trivial, but it includes a surprising number of subtleties that require careful thought and testing.

### Object Identity versus Equal Object Values

Two references are identical if both refer to the same instance. object, and therefore, all objects, include a static method called ReferenceEquals() that explicitly checks for this object identity (see Figure 9.1)

![](img/ef1bd88b5fdf5fb56f8510479607fe66_410_0.png)

Figure 9.1: Identity

However, identical reference is not the only type of equality. Two object instances can also be equal if the values that identify them are equal. Consider the comparison of two ProductSerialNumbers shown in Listing 9.3.

### Listing 9.3: Equal

```csharp
public sealed class ProductSerialNumber
{
    // See Appendix B
}

class Program
{
    static void Main()
    {
        ProductSerialNumber serialNumber1 =
            new ProductSerialNumber("PV", 1008, 09187234);
        ProductSerialNumber serialNumber2 =
        ProductSerialNumber serialNumber3 =
            new ProductSerialNumber("PV", 1008, 09187234);

        // These serial numbers ARE the same object identity.
        if(ProductSerialNumber.ReferenceEquals(serialNumber1,
            serialNumber2))
        {
            throw new Exception(
                "serialNumber1 does NOT " +
                "reference equals serialNumber2");
        }
        // and, therefore, they are equal
        else if(serialNumber1.Equals(serialNumber2))
        {
            throw new Exception(
                "serialNumber1 does NOT equal serialNumber2");
        }
        else
        {
            Console.WriteLine(
                "serialNumber1 reference equals serialNumber2");
            Console.WriteLine(
                "serialNumber1 equals serialNumber2");
        }

        // These serial numbers are NOT the same object identity.
        if (ProductSerialNumber.ReferenceEquals(serialNumber1,
            serialNumber3))
        {
            throw new Exception(
                "serialNumber1 DOES reference " +
                "equal serialNumber3");
        }
        // but they are equal (assuming Equals is overloaded).
        else if((serialNumber1.Equals(serialNumber3) ||
            serialNumber1 == serialNumber3))
        {
            throw new Exception(
                "serialNumber1 does NOT equal serialNumber3");
        }

        Console.WriteLine( "serialNumber1 equals serialNumber3" );
        Console.WriteLine( "serialNumber1 == serialNumber3" );
    }
}
```

The results of Listing 9.3 appear in Output 9.2.

### Output 9.2:

```
serialNumber1 reference equals serialNumber2
serialNumber1 equals serialNumber3
serialNumber1 == serialNumber3
```

As the last assertion demonstrates with ReferenceEquals(), serialNumber1 and serialNumber3 are not the same reference. However, the code constructs them with the same values and both logically associate with the same physical product. If one instance was created from data in the database and another was created from manually entered data, you would expect the instances would be equal and, therefore, that the product would not be duplicated (reentered) in the database. Two identical references are obviously equal; however, two different objects can be equal but not reference equal. Such objects will not have identical object identities, but they may have key data that identifies them as being equal objects.

Only reference types can be reference equal, thereby supporting the concept of identity. Calling ReferenceEquals() on value types will always return false since, by definition, the value type directly contains its data, not a reference. Even when ReferenceEquals() passes the same variable in both (value type) parameters to ReferenceEquals(), the result will still be false because the very nature of value types is that they are copied into the parameters of the called method. Listing 9.4 demonstrates this behavior. In other words, ReferenceEquals() boxes the value types. Since each argument is put into a “different box” (location on the stack), they are never reference equal.

### Listing 9.4: Value Types Do Not Even Reference Equal Themselves

```csharp
public struct Coordinate
{
    public Coordinate(Longitude longitude, Latitude latitude)
    {
```
