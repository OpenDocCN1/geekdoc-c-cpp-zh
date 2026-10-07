
# 518 Chapter 9: Introducing Structs and Records

- 3. Implement the strongly typed Equals() helper method, as shown in Listing 9.21, and check if obj is null (reference types only).

```csharp
public bool Equals(Foo? other)
{
    if (other is null) return false;
    // Step 5
    return (this.Number, this.Name) == (other.Number, other.Name);
    return true;
}
```

- 4. For reference types that don't derive from System.Object, check base.Equals(), enabling refactoring.

- 5. Compare each identifying data for equality, preferably using a tuple.

- 6. Override GetHashCode().

- 7. Override the == and != operators (see Chapter 10 – Operator Overloading).

Steps 3 to 4 in an overload of Equals() that takes the custom data type specifically (such as Coordinate). This way, a comparison of two Coordinates will avoid Equals(object? obj) and its type check altogether.

Equals() should never throw any exceptions. It is a valid choice to compare any object with any other object, and doing so should never result in an exception.

> Guidelines

> DO implement GetHashCode(), Equals(), the == operator, and the = operator—not one of these without the three.

> DO use the same algorithm when implementing Equals(), ==, and !=.

> DO NOT throw exceptions from implementations of GetHashCode(), Equals(), =, and !=.

> AVOID including mutable data when overriding the equality-related members on mutable reference types or if the implementation would be significantly slower with such overriding.

> DO implement all the equality-related methods when implementing IEquatable.

## ADVANCED TOPIC

## Overriding GetHashCode()

If you rely on a record construct, GetHashCode() is automatically implemented for you as part of the value equality implementation (see Listing 9.3 and Listing 9.5). Without the record implementation, you have to implement GetHashCode() on your own, however, if you are providing an equality implementation. Even with a record, if you customize the Equals() implementation, you will likely want to override GetHashCode() to use a similar set of values as the new Equals() implementation. And, if you override only Equals() and not GetHashCode(), you will have a warning:

```text
CS0659: '<Class Name>' overrides Object.Equals(object o) but does not override Object.GetHashCode();
```

In other words, when not leveraging the record construct, overriding equals requires that you also override GetHashCode().

The purpose of the hash code is to efficiently balance a hash table by generating a number that corresponds to the value of an object. And, while there are numerous guidelines (see https://bit.ly/39yp8lm for a discussion), the easiest approach is as follows:

- 1. Rely on the record generated implementation (see Listing 9.2). If you need to override GetHashCode(), you are probably overriding Equals() and using a record is the best approach by default.

- 2. Call System.HashCode's Combine() method, specifying each of the identifying fields (see Listing 9.22):

### LISTING 9.22: Overriding GetHashCode with Combine Method

```csharp
public override int GetHashCode() =>
    HashCode.Combine(Degrees, Minutes, Seconds);
```

- 3. Invoke ValueTuple.GetHashCode() method using the fields that produce your object's uniqueness as the tuple elements, as demonstrated in Listing 9.23. (If the identifying fields are numbers, be wary of mistakenly using the fields themselves rather than their hash code values.)

### LISTING 9.23: Overriding GetHashCode with Combine Method

```csharp
public override int GetHashCode() =>
    (Degrees, Minutes, Seconds).GetHashCode();
```

- 4. ValueTuple invokes HashCode.Combine(); thus, it may be easier to remember that you can adequately create a ValueTuple with the same identifying fields and invoke the resulting tuple's GetHashCode() member

In summary, use a record for overriding GetHashCode() and Equals() unless there is a strong reason not to (such as an older version of C# in which records are not available).

Fortunately, once you have determined that you need GetHashCode(), you can follow some well-established GetHashCode() implementation principles:

- Required: Equal objects must have equal hash codes (if a.Equals(b), then a.GetHashCode() == b.GetHashCode()).

- Required: GetHashCode()'s returns should be constant (the same value), even if the object's data changes. In many cases, you should cache the method return to enforce this constraint. However, when caching the value, be sure not to use the hash code when checking equality; if you do, two identical objects—one with a cached hash code of changed identity properties—will not return the correct result.

- Required: GetHashCode() should not throw any exceptions; GetHashCode() must always successfully return a value.

- Performance: Hash codes should be unique whenever possible. However, since hash codes return only an int, there inevitably be an overlap in hash codes for objects that have potentially more values than an int can hold, which is virtually all types. (An obvious example is long, since there are more possible long values than an int could uniquely identify).

- Performance: The possible hash code values should be distributed evenly over the range of an int. For example, creating a hash that doesn't consider the distribution of a string in Latin-based languages primarily centered on the initial 122 ASCII characters would result in a uneven distribution of string values and to rely on a strong GetHashCode() algorithm.

- Performance: GetHashCode() should be optimized for performance. GetHashCode() is generally used in Equals() to short-circuit a full comparison if the hash codes are different. As a result, it is frequently called when the type is used as a key in dictionary collections.

- Performance: Small differences between two objects should result in large differences between hash values—ideally, 16 bits of the hash code changing, or average. This helps ensure that the hash table remains balanced no matter how it is "bucketing" the values.

These guidelines and rules are, of course, contradictory: It is very difficult to come up with a hash algorithm that is fast and meets all of these guidelines. With any design problem, you will need to use a combination of good judgment and realistic performance measurements to come up with a good solution. The easiest approach, of course, is to rely on one of the previously identified Customizing Record Behavior

Clearly, the C# compiler generates a significant amount of code for the record struct and class constructs. However, all the behavior is customizable. As mentioned earlier in the chapter, for example, you can add any additional members, including properties, fields, constructors, and methods. More importantly, you can provide your own versions of the generated members. Coding any record member with a matching signature to the otherwise synthesized member, you can replace the default behavior with your own. If you prefer a read-only property rather than an init-only setter property, you simply declare the property (or field) to match the positional property name. Or, by providing your own copy constructor, you can inject custom behavior into how a record handles cloning (via the with operator). Similarly, if you want to change the semantics of equality, perhaps to simplify it to a subset of the record's properties/fields, you can define your own Equals() method, likely only the method that takes a single parameter of the containing type. Listing 9.24 provides examples of possible customizations on a record.

### LISTING 9.24: Customizing a Record

```csharp
public readonly struct Angle(
    int Degrees, int Minutes, int Seconds, string Name = null)
{
    public int Degrees { get; } = Degrees;

    public Angle(
        string degrees, string minutes, string seconds)
        : this(int.Parse(degrees),
        int.Parse(minutes), int.Parse(seconds))
    {}

    public override readonly string ToString()
    {
        string prefix =
            string.IsNullOrWhiteSpace(Name)?string.Empty : Name+":": ";
        return $"{prefix}{Degrees}:{Minutes}:{Seconds}";
    }
}
```
