Console.WriteLine("Are any contacts under 21 years old? {0}",nanyUnder21);

Console.WriteLine("Are any records without email or phone? {0}",nanyMissingContactData);

# Output 5-20

Are any contacts under 21 years old? False
Are any records without email or phone? False

# Contains Operator

The Contains operator returns the Boolean value of true if the sequence con-tains an equivalent element as the test argument passed into this operator.
There are two overloads for this operator—one that takes a single argument of the test value and the second that takes the test value and an IEqualityComparer<T> instance that is employed for equality testing. The method signatures for the Contains operator are:

```
// Returns true if the test element is in the
// sequence, otherwise returns false.
public static bool Contains<TSource>(
this IEnumerable<TSource> source, TSource value);
```

```
// Returns true if the test element is in the
// sequence, otherwise returns false. Uses the
// Equality Comparer passed in test equality.
public static bool Contains<TSource>(
this IEnumerable<TSource> source,
TSource value,
IEqualityComparer<TSource> comparer);
```

To demonstrate the Contains operator, Listing 5-33 looks to see if var-ious versions of the name Peter are contained in the elements of a string array. The test b1 will be false because the default comparison of a string is case sensitive. Test b2 will be true because it is an exact string match, and test b3 will be true even though the string case is a cus-tomEqualityComparer<T> was used to determine string equality. (Creating custom IEqualityComparers is covered in Chapter 4 in the “Specifying Your