
## Stable

The result of x < y remains the same as long as neither value is changed.

## Safe

Comparing values of the same type does not throw exceptions.

We can define CompareTo and operator< for reference types in a similar way, although we also need to consider the null reference, which should always compare less than any non-null value.

## Other Kinds of Ordering

Ordering by DateTime or number is an example of ordering by magnitude, but other orderings are possible. Strings commonly use a lexicographical ordering, which broadly means that one string is less than another if it would appear before the other in a lexicon, better known as a dictionary.

Other values are ordinal in nature, such as months of the year. Ordinal comparisons sometimes need a bit of care. Take days of the week in English as an example: should Sunday come before Monday? The answer to that question depends on how we define the first day of the week.

Some values aren’t intrinsically less than another. The Color type is an example: red comes before blue when we enumerate the colors in a rainbow—a property of their relative wavelengths—but blue certainly comes before red in an English dictionary. We might apply one of several orderings to Color objects under different circumstances, but those definitions of ordering are external to the concept of a color.

We can customize the ordering of elements in a sequence on a case-by-case basis by creating our own comparer, or even multiple comparers to address different scenarios. The IComparer<T> interface complements the IEqualityComparer<T> interface from Chapter 5. Just as IEqualityComparer<T> establishes an equality comparison that’s external to the types being compared, an implementation of IComparer<T> is an externally defined ordering comparison. Listing 6-20 shows a custom comparer type for ordering LogEntry objects by their Message property rather than by time.

```
public sealed class LogEntryComparer : IComparer<LogEntry>
{
    public int Compare(LogEntry x, LogEntry y)
        => string.Compare(x.Message, y.Message, StringComparison.Ordinal);
}
```

Listing 6-20: Defining an external comparer for LogEntry objects

The semantics of the Compare method match those of IComparable.CompareTo, returning a negative integer when x is less than y, a positive integer when y is less than x, and 0 otherwise. Several of the sorting algorithms in the Standard Library have overloads that accept an explicit comparer object as an argument, including the Order method shown here:

```
var log = new List<LogEntry>();

--snip--

var comparer = new LogEntryComparer();
var alphabeticalLog = log.Order(comparer).ToList();
```

This alphabeticalLog is a new list of LogEntry elements sorted alphabetically by using the LogEntryComparer.Compare comparison. Similar overloads are provided for List<T>.Sort and List<T>.BinarySearch and the constructor for SortedList.

Ordering is a common characteristic of values, but not an essential one in the same way that value-based equality is. When a value has a natural ordering, implementing the CompareTo method makes sense. Reference types, on the other hand, generally don’t override CompareTo unless they also override Equals. Mixing identity-based equality with value-based ordering, or vice versa, will likely lead to confusion and probably errors that are hard to track down. In particular, references have no natural ordering; saying that the value of one reference is less than another makes no sense.

## The Perils of Uniformity and Consistency

Sometimes coding guidelines advise that we should override Equals and implement CompareTo for every type. The thinking behind such rules is usually to try to remove restrictions on the use of objects. Types that don’t implement IComparable can’t be used as keys in a SortedList. Types that don’t override Equals and GetHashCode can’t be used reliably as keys in a Dictionary. While we can use an implementation of IComparer<T> to address the former, and a custom IEqualityComparer<T> for the latter, we must remember to explicitly use those implementations.

Such guidelines aim to improve consistency and remove the barriers to commonplace requirements. The goal is usually to enable any object to be used as a key in a hashing container, or collections of them to be sorted according to their state, without needing explicitly defined external comparers.

Guidelines that suggest this kind of uniformity ignore the fact that values and non-values are semantically and conceptually different, and the differences go far beyond the technical characteristics of reference types and value types. Reference semantics have their own desirable characteristics, especially when we actively need multiple aliasing references to a single, mutable instance. Those characteristics don’t lend themselves well to being used as keys in collections, and they often cause conflict with ordering too. A sorted collection of mutable objects can easily become unordered by altering the state of its elements, which gives us one more reason for all our value types to be immutable. A collection of values that has been sorted should remain sorted.

As we’ve discussed, some types have no natural ordering. Let’s revisit the example of Color. Insisting that a Color type implement the IComparable

interface would leave us with a problem: how should CompareTo behave for two Color values? We could choose one plausible implementation, but that might not satisfy every use case, leading to difficulties in other aspects of our code. This is why, while records and record structs provide a default implementation of the IEquatable<T> interface, they don’t also implement IComparable<T>. Even when the individual fields can be compared with CompareTo, it doesn’t always mean that the whole type can be compared that way. All the fields for Color are int values that implement IComparable<int>, after all, but less than isn’t a meaningful comparison for Color values.

The purpose of overriding the Equals method for value types isn’t primarily to allow them to be used as keys. Values have no use for referential equality, because one value is as good as any other value with the same properties. Value-based equality is the single, natural way to compare those variables that are values.

Reference types, by contrast, often depend on identity-based equality. Any type not specifically intended to have value semantics probably shouldn’t be used as a key in a Dictionary.

## Arithmetic and Nonarithmetic Types

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
