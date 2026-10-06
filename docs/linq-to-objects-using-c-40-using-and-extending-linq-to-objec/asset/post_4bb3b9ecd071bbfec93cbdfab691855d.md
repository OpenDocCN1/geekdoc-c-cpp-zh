
"Own Key Comparison Function" section and in Chapter 6 under "Custom EqualityComparers When Using LINQ Set Operators.") The Console output from this example is shown in Output 5-21.

**Listing 5-33** The Contains operator returns true if the test element is in the sequence—see Output 5-21

```
string[] names = new string[] { "peter", "paul", "mary" };

bool b1 = names.Contains("PETER");
bool b2 = names.Contains("peter");

// Custom comparators or the built-in comparers can be used
bool b3 = names.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine("PETER: {0}, peter: {1}, PETER: {2}",
b1, b2, b3);
```

# **Output 5-21**

PETER: False, peter: True, PETER: True

Some collection types that implement IEnumerable<T> and are in scope for the Contains extension method implement their instance method called Contains(List<T> for instance). This doesn't cause any problems in most cases, but if you explicitly want to call the extension Contains, specify the generic type. Listing 5-34 demonstrates how to explicitly control what gets called (instance method or extension method) when using a collection of type List<T>. The Console output from this example is shown in Output 5-22.

**Listing 5-34** How to explicitly specify which Contains you want to call when a collection has an instance method called Contains—see Output 5-22

```
// List<T> already has an instance method called "Contains"
// The instance method doesn't have an overload that
// supports EqualityComparer's, and the Contains
// extension method can be used for this call.
```

# SUMMARY 171

```
List<string> list =
    new List<string> { "peter", "paul", "mary" };

// will use the List<T>.Contains method
bool b4 = list.Contains("PETER");

// will force use of the Contains Extension method
bool b5 = list.Contains<string>("PETER");

// or better still, just call the Extension Method
bool b6 = Enumerable.Contains(list, "PETER");

// will use the Contains Extension method because
// the List<T>.Contains has no overload taking
// an IEqualityComparer
bool b7 = list.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine(
    "Instance: {0}, Extension: {1}, With Comparator: {2}",
    b4, b5, b6);
```

# Output 5-22

Instance: False, Extension: False, With Comparator: True

# Summary

This chapter introduced many of the remaining standard query operators that are available to you in .NET Framework 4. The next chapter covers the last few operators that specifically apply set-based functions over data sources.

# CHAPTER 6

# WORKING WITH SET DATA

Goals of this chapter:

- Define the two options for working with set data using LINQ.
- Introduce the HashSet type and how this relates to LINQ.
- Introduce the LINQ standard query operators that relate to working with set data.

There are two ways of applying set-based functions over data sequences using LINQ. This chapter explores the merits of both options and explains when and why to use one method over another.

# Introduction

Set operations allow various functions to compare elements against each other in collections (and in some cases, the same collection) against each other to determine overlapping and unique elements within a collection.

Framework libraries for set operations were missing in the .NET Framework 1, 2, and 3. The HashSet was introduced in .NET Framework 3.5, and this collection type solves most set problems often faced by developers. LINQ extended set function capability with specific operators, some of which overlap with HashSet functionality. It is important to understand the benefits of both strategies and when to choose one over another. This section looks in detail at the two main choices:

- LINQ standard query operators
- HashSet<T> class from the System.Collections.Generic namespace

The decision of how to approach a set-based task depends on problem specifics, but in general the strengths of each can be described in the following ways:

Use HashSet and its operators when

- Duplicate items are not allowed in the collections.
- Modifying the original collection is desired. These operators allow changes to the original collection.

Use LINQ Operators when

- Duplicate items are allowed in the collections.
- When returning a new IEnumerable<T> is desired rather than modifying the original collection.

# The LINQ Set Operators

LINQ to Objects has standard query operators for working on sets of elements within collections. These operators allow two different collections (containing the same types of elements) to be merged into a single collection using various methods.

The set operators all implement a deferred execution pattern, simply meaning that they do not evaluate the next element until they are iterated over one element at a time. Each operator is detailed in this section, including the method signatures for each operator.

# Concat Operator

Concat combines the contents of two collections. It operates by looping over the first collection yielding each element, looping over the second collection yielding each element. If returning the duplicate elements is not the desired behavior, consider using the Union operator instead. An ArgumentNullException is thrown if either collection is null when this operator is called.

Concat has a single overload with the following method signature:

```
// Combines the contents of two collections.
// Returns all elements from the
IEnumerable<TSource> Concat<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second);
```

# **Output 5-21**

PETER: False, peter: True, PETER: True

Some collection types that implement IEnumerable<T> and are in scope for the Contains extension method implement their instance method called Contains(List<T> for instance). This doesn't cause any problems in most cases, but if you explicitly want to call the extension Contains, specify the generic type. Listing 5-34 demonstrates how to explicitly control what gets called (instance method or extension method) when using a collection of type List<T>. The Console output from this example is shown in Output 5-22.

**Listing 5-34** How to explicitly specify which Contains you want to call when a collection has an instance method called Contains—see Output 5-22

```
// List<T> already has an instance method called "Contains"
// The instance method doesn't have an overload that
// supports EqualityComparer's, and the Contains
// extension method can be used for this call.
```

# SUMMARY 171

```
List<string> list =
    new List<string> { "peter", "paul", "mary" };

// will use the List<T>.Contains method
bool b4 = list.Contains("PETER");

// will force use of the Contains Extension method
bool b5 = list.Contains<string>("PETER");

// or better still, just call the Extension Method
bool b6 = Enumerable.Contains(list, "PETER");

// will use the Contains Extension method because
// the List<T>.Contains has no overload taking
// an IEqualityComparer
bool b7 = list.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine(
    "Instance: {0}, Extension: {1}, With Comparator: {2}",
    b4, b5, b6);
```

# Output 5-22

Instance: False, Extension: False, With Comparator: True

# Summary

This chapter introduced many of the remaining standard query operators that are available to you in .NET Framework 4. The next chapter covers the last few operators that specifically apply set-based functions over data sources.

# CHAPTER 6

# WORKING WITH SET DATA

Goals of this chapter:

- Define the two options for working with set data using LINQ.
- Introduce the HashSet type and how this relates to LINQ.
- Introduce the LINQ standard query operators that relate to working with set data.

There are two ways of applying set-based functions over data sequences using LINQ. This chapter explores the merits of both options and explains when and why to use one method over another.

# Introduction

Set operations allow various functions to compare elements against each other in collections (and in some cases, the same collection) against each other to determine overlapping and unique elements within a collection.

Framework libraries for set operations were missing in the .NET Framework 1, 2, and 3. The HashSet was introduced in .NET Framework 3.5, and this collection type solves most set problems often faced by developers. LINQ extended set function capability with specific operators, some of which overlap with HashSet functionality. It is important to understand the benefits of both strategies and when to choose one over another. This section looks in detail at the two main choices:

- LINQ standard query operators
- HashSet<T> class from the System.Collections.Generic namespace

The decision of how to approach a set-based task depends on problem specifics, but in general the strengths of each can be described in the following ways:

Use HashSet and its operators when

- Duplicate items are not allowed in the collections.
- Modifying the original collection is desired. These operators allow changes to the original collection.

Use LINQ Operators when

- Duplicate items are allowed in the collections.
- When returning a new IEnumerable<T> is desired rather than modifying the original collection.

# The LINQ Set Operators

LINQ to Objects has standard query operators for working on sets of elements within collections. These operators allow two different collections (containing the same types of elements) to be merged into a single collection using various methods.

The set operators all implement a deferred execution pattern, simply meaning that they do not evaluate the next element until they are iterated over one element at a time. Each operator is detailed in this section, including the method signatures for each operator.

# Concat Operator

Concat combines the contents of two collections. It operates by looping over the first collection yielding each element, looping over the second collection yielding each element. If returning the duplicate elements is not the desired behavior, consider using the Union operator instead. An ArgumentNullException is thrown if either collection is null when this operator is called.

Concat has a single overload with the following method signature:

```
// Combines the contents of two collections.
// Returns all elements from the
IEnumerable<TSource> Concat<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second);
```

# **Output 5-21**

PETER: False, peter: True, PETER: True

Some collection types that implement IEnumerable<T> and are in scope for the Contains extension method implement their instance method called Contains(List<T> for instance). This doesn't cause any problems in most cases, but if you explicitly want to call the extension Contains, specify the generic type. Listing 5-34 demonstrates how to explicitly control what gets called (instance method or extension method) when using a collection of type List<T>. The Console output from this example is shown in Output 5-22.

**Listing 5-34** How to explicitly specify which Contains you want to call when a collection has an instance method called Contains—see Output 5-22

```
// List<T> already has an instance method called "Contains"
// The instance method doesn't have an overload that
// supports EqualityComparer's, and the Contains
// extension method can be used for this call.
```

# SUMMARY 171

```
List<string> list =
    new List<string> { "peter", "paul", "mary" };

// will use the List<T>.Contains method
bool b4 = list.Contains("PETER");

// will force use of the Contains Extension method
bool b5 = list.Contains<string>("PETER");

// or better still, just call the Extension Method
bool b6 = Enumerable.Contains(list, "PETER");

// will use the Contains Extension method because
// the List<T>.Contains has no overload taking
// an IEqualityComparer
bool b7 = list.Contains(
    "PETER", StringComparer.InvariantCultureIgnoreCase);

Console.WriteLine(
    "Instance: {0}, Extension: {1}, With Comparator: {2}",
    b4, b5, b6);
```

# Output 5-22

Instance: False, Extension: False, With Comparator: True

# Summary

This chapter introduced many of the remaining standard query operators that are available to you in .NET Framework 4. The next chapter covers the last few operators that specifically apply set-based functions over data sources.

# CHAPTER 6

# WORKING WITH SET DATA

Goals of this chapter:

- Define the two options for working with set data using LINQ.
- Introduce the HashSet type and how this relates to LINQ.
- Introduce the LINQ standard query operators that relate to working with set data.

There are two ways of applying set-based functions over data sequences using LINQ. This chapter explores the merits of both options and explains when and why to use one method over another.

# Introduction

Set operations allow various functions to compare elements against each other in collections (and in some cases, the same collection) against each other to determine overlapping and unique elements within a collection.

Framework libraries for set operations were missing in the .NET Framework 1, 2, and 3. The HashSet was introduced in .NET Framework 3.5, and this collection type solves most set problems often faced by developers. LINQ extended set function capability with specific operators, some of which overlap with HashSet functionality. It is important to understand the benefits of both strategies and when to choose one over another. This section looks in detail at the two main choices:

- LINQ standard query operators
- HashSet<T> class from the System.Collections.Generic namespace

The decision of how to approach a set-based task depends on problem specifics, but in general the strengths of each can be described in the following ways:

Use HashSet and its operators when

- Duplicate items are not allowed in the collections.
- Modifying the original collection is desired. These operators allow changes to the original collection.

Use LINQ Operators when

- Duplicate items are allowed in the collections.
- When returning a new IEnumerable<T> is desired rather than modifying the original collection.

# The LINQ Set Operators

LINQ to Objects has standard query operators for working on sets of elements within collections. These operators allow two different collections (containing the same types of elements) to be merged into a single collection using various methods.

The set operators all implement a deferred execution pattern, simply meaning that they do not evaluate the next element until they are iterated over one element at a time. Each operator is detailed in this section, including the method signatures for each operator.

# Concat Operator

Concat combines the contents of two collections. It operates by looping over the first collection yielding each element, looping over the second collection yielding each element. If returning the duplicate elements is not the desired behavior, consider using the Union operator instead. An ArgumentNullException is thrown if either collection is null when this operator is called.

Concat has a single overload with the following method signature:

```
// Combines the contents of two collections.
// Returns all elements from the
IEnumerable<TSource> Concat<TSource>(
    this IEnumerable<TSource> first,
    IEnumerable<TSource> second);
```

# **Output 5-21**

PETER: False, peter: True, PETER: True

Some collection types that implement IEnumerable<T> and are in scope for the Contains extension method implement their instance method called Contains(List<T> for instance). This doesn't cause any problems in most cases, but if you explicitly want to call the extension Contains, specify the generic type. Listing 5-34 demonstrates how to explicitly control what gets called (instance method or extension method) when using a collection of type List<T>. The Console output from this example is shown in Output 5-22.

**Listing 5-34** How to explicitly specify which Contains you want to call when a collection has an instance method called Contains—see Output 5-22

```
// List<T> already has an instance method called "Contains"
// The instance method doesn't have an overload that
// supports EqualityComparer's, and the Contains
// extension method can be used for this call.
```
