string values, each inner pair of curly braces contains one of each, separated by a comma. The key/value pairs are separated by commas as well.

Initializing sets (see the next section) is much like initializing lists:

```
HashSet<int> biggerPrimes = new HashSet<int> { 19, 23, 29, 31, 37, 41 };
```

The UsingVarWithArraysAndCollections example on this book’s Web site demonstrates the var keyword used with arrays and collections.

![](bbox=[0.142, 0.219, 0.245, 0.296])

# Using Sets

C# 3.0 added the new collection type HashSet<T>. A set is an unordered collection with no duplicate items.

The set concept comes from mathematics. Think of the set of genders (female and male), the set of days in a week, or the set of variations on the triangle (isosceles, equilateral, scalene, right, obtuse). Unlike math sets, C# sets can’t be infinite, though they can be as large as available memory.

You can do things to a set in common with other collections, such as add, delete, and find items. But you can also perform specially set-like operations, such as union and intersection. Union joins the members of two sets into one. Intersection finds the overlap between two sets and results in a set containing only the overlapping members. So sets are good for combining and eliminating items.

Like dictionaries, sets are implemented using hash tables. Sets resemble dictionaries with keys but no values, making them list-like in shape. See the earlier section “Using Dictionaries” for details.

To create a HashSet<T>, you can do this:

```
HashSet<int> smallPrimeNumbers = new HashSet<int>();
smallPrimeNumbers.Add(2);
smallPrimeNumbers.Add(3);
```

Or, more conveniently, you can use a collection initializer:

```
HashSet<int> smallPrimeNumbers = new HashSet<int> { 2, 3, 5, 7, 11, 13 };
```

Or create the set from an existing collection of any list-like kind, including arrays:

```
List<int> ints = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7 };
HashSet<int> numbers = new HashSet<int>(ints);
```

If you attempt to add to a hash set an item that the set already contains, as in this example:

![](bbox=[0.141, 0.593, 0.246, 0.738])