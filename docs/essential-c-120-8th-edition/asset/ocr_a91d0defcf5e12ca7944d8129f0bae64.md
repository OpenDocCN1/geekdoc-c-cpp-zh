# Chapter 9: Introducing Structs and Records

update the Equals() method, you should update GetHashCode(), so use the same data elements. A failure to override GetHashCode() when overriding Equals(), and vice-versa, will generate a warning:

```
CS8851 '<ClassName>' defines 'Equals' but not 'GetHashCode'
```

While this snippet differs from the record-generated version of Equals() shown in Listing 9.3, internally the tuple (System.ValueTuple<...>) uses EqualityComparer<T> as well. In turn, EqualityComparer<T> relies on the type parameters implementation of IEquatable<T> (which contains only a single Equals<T>(T other member). Therefore, to correctly override Equals, you need to implement IEquatable<T>.

Once Equals() is overridden, there is a possible inconsistency. That is, two objects could return true for Equals() but false for the == operator performs reference equality check by default. To correct this flaw, it is important to override the equals (=) and not equals (!) operators as well. Of course, this is generated for you as part of the record implementation as you can see in Listing 9.18:

+   Listing 9.18: Overriding the == and != Operators

```
public static bool operator ==(Coordinate left, Coordinate? right) =>
    ReferenceEquals(left, right) || (left?.Equals(right) ?? false);
//
public static bool operator !=(Angle left, Angle right) =>
    !(left != right);
```

For the most part, implementation for these operators can delegate the logic to Equals(), or vice versa. Take care, not to invoke an infinite recursive loop with the == operator calling on itself. In this case, a recursion is avoided because we use ReferenceEquals() initially, which will return true if both values are null. For value types, there is, of course, no need to check for null. See Chapter 10 (https://essentialsharp.com/operator-overloading/) for more information on operator overloading.

Lastly, consider implementing IComparable<T> if the custom type can be sorted along with the IFormattable interface for localization is needed. For the full