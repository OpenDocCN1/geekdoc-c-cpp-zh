interface would leave us with a problem: how should CompareTo behave for two Color values? We could choose one plausible implementation, but that might not satisfy every use case, leading to difficulties in other aspects of our code. This is why, while records and record structs provide a default implementation of the IEquatable<T> interface, they don’t also implement IComparable<T>. Even when the individual fields can be compared with CompareTo, it doesn’t always mean that the whole type can be compared that way. All the fields for Color are int values that implement IComparable<int>, after all, but less than isn’t a meaningful comparison for Color values.

The purpose of overriding the Equals method for value types isn’t primarily to allow them to be used as keys. Values have no use for referential equality, because one value is as good as any other value with the same properties. Value-based equality is the single, natural way to compare those variables that are values.

Reference types, by contrast, often depend on identity-based equality. Any type not specifically intended to have value semantics probably shouldn’t be used as a key in a Dictionary.

# Arithmetic and Nonarithmetic Types

Just as not all values have a natural ordering, some values are arithmetic by nature, and some are not. We might, for example, define operations to allow instances of the Speed type from Listing 6-11 to be added together. Operations like addition have a natural representation with arithmetic operators, such as in an expression like startingSpeed + Speed.FromKmh(10).

Introducing support for arithmetic operations, or indeed any operation, requires a certain amount of discretion on our part as designers. We need to be mindful of both the common use cases for the types we create and the wider expectation from, for example, being able to add two instances together with a + operator.

Unlike Speed, the LogEntry type in Listing 6-17 isn’t arithmetic in nature, so we should avoid overloading the arithmetic operators for it. Adding two LogEntry instances makes no sense.

It does make sense for LogEntry to overload operator== and its counterpart operator!= for equality comparisons. The LogEntry type is a record struct, so the compiler will provide the equality operator definitions automatically. Since we’ve implemented IComparable<LogEntry> for LogEntry, we should also consider overloading operator< and operator>, which the compiler won’t provide. Listing 6-21 shows that implementing these operators in terms of the CompareTo method is straightforward.

```
public static bool operator<(LogEntry left, LogEntry right)
    => left.CompareTo(right) < 0;

public static bool operator>(LogEntry left, LogEntry right)
    => left.CompareTo(right) > 0;
```

Listing 6-21: Equivalence comparison operator definitions