# Aggregation Operators—Working with Numbers 123

# Aggregation Operators—Working with Numbers

LINQ's aggregation operators enumerate a sequence of values (normally numeric, but not mandatory), perform some operation for each element, and ultimately return a result (normally numeric, but not mandatory). In pure form, Sum, Average, Min, and Max can all be built using the Aggregate operator; however, the specifically named operators make queries cleaner in syntax by spelling out the exact operation being performed. Each of these operators are covered in detail in the following sections, starting with the Aggregate operator.

# Aggregate Operator

The Aggregate operator performs a folding pattern on each element using a lambda expression and passing the accumulated result to the next element when processed. This operator is powerful, both in building day-to-day queries to process an entire sequence and building other operators that carry out numeric operations on a sequence (the Aggregate operator is used as the basis for a custom operator to calculate the standard deviation and variance, as discussed in Chapter 9,"Parallel LINQ to Objects")

The Aggregate operator has three overloaded method signatures. These overload allow you to specify a seed value and/or a selection function in addition to the aggregation function. The method signatures available are:

```
// Applies an accumulator function to each element.
public static TSource Aggregate<TSource>(
	this IEnumerable<TSource> source,
	Func<TSource, TSource, TSource> func);
```

```
// Applies an accumulator function to each element.
// The accumulator can be a different type than the elements,
// and a starting (seed) value must be specified.
public static TAccumulate Aggregate<TSource, TAccumulate>(
	this IEnumerable<TSource> source,
	TAccumulate seed,
	Func<TAccumulate, TSource, TAccumulate> func);
```

```
// Applies an accumulator function to each element.
// The accumulator can be a different type than the elements
```