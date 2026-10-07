
## Overriding object Members

Chapter 6 discussed how all classes and structs ultimately derive from object. In addition, it reviewed every method available on object and discussed how some of them are virtual. This section discusses the details concerning overriding virtual methods. Doing so is automatic for records, but the generated code also provides an example of what is required if you choose to customize the generated code or implement an override on a non-record type implementation.

## Overriding ToString()

By default, calling ToString() on any object will return the fully qualified name of the object type. Calling ToString() on a System.IO.FileStream object will return the System.IO.FileStream, for example. For some classes, however, ToString() can be more meaningful. String, for example, ToString() returns the string itself. Similarly, when invoking ToString() on an Angle (Listing 9.1), the result returns:

```
Angle { Degrees = 90, Minutes = 0, Seconds = 0, Name =
```

(This also happens to be the output of Listing 9.2.)

Write methods such as System.Console.WriteLine() and System.Diagnostics.Trace.Write() call an object's ToString() method, so overriding the method often outputs more meaningful than the default implementation.

Overriding ToString() requires nothing more than declaring the ToString() method as an override and returning a string. Take Listing 9.16 for:

Listing 9.16: Overriding the ToString Method

> 7. Unless there is an implicit cast operator, as described in "Advanced Topic: Cast Operator".

Regardless, do not return an empty string or null, as the lack of output will be very confusing. ToString() is useful for debugging from a developer IDE or writing to a log file. Be mindful of implementing localization overload methods and advanced formatting features to ensure suitability for general end-user text display. Also, keep the strings relatively short so that they are not truncated off the end of the screen — especially in debugging in an IDE.

Consider overriding the ToString() method whenever relevant diagnostic information can be provided from the output — specifically, when the target audience is developers, since the default.ToString() output is a type name and is not end-user friendly. Alternatively, starting in C# 10.0, you can seal a record's ToString() implementation, preventing its override by derived-type—including a code generated implementation.

| Guidelines |
| :--- |
| **DO** override ToString() whenever useful developer-oriented diagnostic strings can be returned. |
| **CONSIDER** trying to keep the string returned from ToString() short. |
| **DO NOT** return an empty string or *null* from ToString(). |
| **DO NOT** throw exceptions or make observable side effects (change the object state) from ToString(). |
| **DO provide** an overloaded ToString(string format) or implement IFormattable if the return value requires formatting or is culture-sensitive (e.g., DateTime). |
| **CONSIDER** returning a unique string from ToString() so as to identify the object instance. |

## Implementing Value Equality

Frequently, developers expect implementing value equivalence to be trivial. How hard could it be to compare two objects? However, it includes a surprising number of subtleties and complexities that require careful thought and testing. Fortunately, there are two approaches that significantly simplify the code. Firstly, if you use a record construct, then the C# compiler takes care of generating the Equals() method and all its associated members for you, comparing automatically implemented properties and fields of the record—whether they are included as positional parameters or not. Secondly, you can group the identifying data elements (automatically implemented properties and fields) into a tuple and then compare the tuples. In case of reference type, you also need to pay attention to any potential null values.

Listing 9.3 shows the implementation of Equals() that was generated for a record and enables value equality. One of the big advantages of C# records is that they generate a value equality implementation, relieving you of the exercise of manually implementing what could be a surprisingly complex method considering inheritance, null, varying data types, and value/reference type in addition to comparing the contained values themselves. If said, if the record-generated implementation doesn't suit your needs, this is not the case you will need to write your own. One reason to do that is that you may not want some of the properties to be included as part of the value equals determination. Perhaps you don't want the Name property on Angle to be part of an Angle's value identity, instead relying solely on Degrees, Minutes, and Seconds. Listing 9.24 provides such a full customized record struct with the following snippet of a custom equality implementation in Listing 9.17:

### LISTING 9.17: Custom Equality Implementation

```
public bool Equals(Angle other) =>
    (Degrees, Minutes, Seconds).Equals(
        other.Degrees, other.Minutes, other.Seconds));
```

Notice that the value-identifying properties are combined into tuples and compared with the same values of other. In addition, be aware that the equals implementation is overloaded. The previous snippet shows the implementation with an Angle parameter. That is because the C# compiler generates all the additional value equality functionality for you. However, this is not the case on types that are not records—you must provide all such customization yourself. Also, whenever you update the Equals() method, you should update GetHashCode(), so use the same data elements. A failure to override GetHashCode() when overriding Equals(), and vice-versa, will generate a warning:

```
CS8851 '<ClassName>' defines 'Equals' but not 'GetHashCode'
```

While this snippet differs from the record-generated version of Equals() shown in Listing 9.3, internally the tuple (System.ValueTuple<...>) uses EqualityComparer<T> as well. In turn, EqualityComparer<T> relies on the type parameters implementation of IEquatable<T> (which contains only a single Equals<T>(T other member). Therefore, to correctly override Equals, you need to implement IEquatable<T>.

Once Equals() is overridden, there is a possible inconsistency. That is, two objects could return true for Equals() but false for the == operator performs reference equality check by default. To correct this flaw, it is important to override the equals (=) and not equals (!) operators as well. Of course, this is generated for you as part of the record implementation as you can see in Listing 9.18:

-   Listing 9.18: Overriding the == and != Operators

```
public static bool operator ==(Coordinate left, Coordinate? right) =>
    ReferenceEquals(left, right) || (left?.Equals(right) ?? false);
//
public static bool operator !=(Angle left, Angle right) =>
    !(left != right);
```

For the most part, implementation for these operators can delegate the logic to Equals(), or vice versa. Take care, not to invoke an infinite recursive loop with the == operator calling on itself. In this case, recursion is avoided because we use ReferenceEquals(), which will return true if both values are null. For value types, there is, of course, no need to check for null. See Chapter 10 (https://essentialsharp.com/operator-overloading/) for more information on operator overloading.

Lastly, consider implementing IComparable<T> if the custom type can be sorted along with the IFormattable interface for localization is needed. For the full implementation of value equality without using a record construct, see “Advanced Topic: Overriding GetHashCode().” There are two important topics related to value types that we still need to cover. The first is boxing, and the second is enums, and both are discussed in the following sections.

## ADVANCED TOPIC

### Value Equality Principles

Notice that the signature of Equals() in Listing 9.24 does not match the signature object in Listing 9.19.

```
LISTING 9.19: Nonmatching Signature
public override bool Equals(object? obj)
```

(If it did, we would need to use the override modifier). When implementing Equals() on a class or struct (that are not records), there are several other considerations to be aware of. All are available in Listing 9.3 for a struct and Listing 9.5 for a class (because the record modifier generates them).

The steps for implementing value equality on a custom type are as:

- 1. Implement the IEquatable<T> interface.

- 2. Implement the Equals(object? obj) method, checking that obj is the same as the custom type and invoking the strongly typed Equals() helper method that can treat the operand as the custom type rather than an object (Listing 9.20).

```
LISTING 9.20: Implementing Value Equality on a Custom Type
public override bool Equals(object? obj)
{
    return Equals(obj as Foo);
}
```

- 3. Generics are discussed in Chapter 12.
