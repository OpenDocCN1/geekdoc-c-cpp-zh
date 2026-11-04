
```
Order By Memory Descending
Select ProcessName, Memory
```

Other operators, such as Take, Skip, and Distinct, also have syntactical language integration in Visual Basic.

## Predicates

In the world of LINQ, predicate operators express Boolean-valued truths about sequences and their elements. Operators such as Any and All should sound familiar to those who’ve learned basics of predicate logic. Other operators include SequenceEqual (to compare two sequences) and Contains (to ask membership questions about elements in sequences). Let’s take a look at all of those.

### All and Any

All and Any evaluate a predicate for each of the elements in a given sequence. If all the elements pass the predicate, All will return true. If some of the elements pass the predicate, Any will also return true:

```
static bool All<T>(this IEnumerable<T> source, Func<T, bool> predicate);
static bool Any<T>(this IEnumerable<T> source);
static bool Any<T>(this IEnumerable<T> source, Func<T, bool> predicate);
```

The extra overload for Any checks whether a sequence has any elements, returning false for an empty sequence. Some examples of the use of those operators are shown here:

```
var allEven = new[] { 2, 4, 6, 8, 10 }.All(x => x % 2 == 0); // true
var someOdd = new[] { 2, 3, 4, 5 }.Any(x => x % 2 == 1); // true
var anyElement = new int[] {}.Any(); // false, sequence empty
```

In fact, those operators are also special forms of aggregation operations. For example, All can be written in terms of an aggregation using &&. One subtle difference is that the All and Any operators will stop iteration over the source sequence as soon as the result is known. All will return false as soon as an element doesn’t match the predicate; Any will return true as soon as an element does match the predicate:

```
var allEven = new[] { 1, 2, 3 }.Aggregate(true,
    (all, x) => all && x % 2 == 0);
```

### Contains

As the name implies, Contains performs a membership check for a given element in a given sequence. Two overloads exist, one with and one without an equality comparer:

```csharp
static bool Contains<T>(this IEnumerable<T> source, T value);
static bool Contains<T>(this IEnumerable<T> source, T value,
                        EqualityComparer<T> comparator);
```

Use of this operator doesn't require further explanation. One important remark is that the operator will terminate iteration over the source sequence as soon as an element is found that matches the equality check. Also notice there's no In operator because that would create an extension method on a generic parameter T, which would appear everywhere.

### SequenceEqual

To compare whether two sequences have the same elements, a check carried out by means of an equality test, the SequenceEqual operator can be used. Equality over a sequence is defined in an element-by-element pairwise equality check, also requiring that both sequences have the same number of elements:

```csharp
static bool SequenceEqual<T>(this IEnumerable<T> first, IEnumerable<T> second);
static bool SequenceEqual<T>(this IEnumerable<T> first, IEnumerable<T> second,
                             EqualityComparer<T> comparator);
```

A few examples illustrate the operator's behavior:

```csharp
var f = new[] { 1, 2, 3 }.SequenceEqual(new[] { 1 }); // false
var s = new[] { 1, 2, 3 }.SequenceEqual(new[] { 2, 3, 1 }); // false
var t = new[] { 1, 2, 3 }.SequenceEqual(new[] { 1, 2, 3 }); // true
```

## Set Theoretical and Sequencing Operators

So far, we've always been talking about sequences as the sources of data which LINQ operates on. Even though the use of sequences implies an ordering of elements, it doesn't preclude certain set theoretical operations, such as intersection and union, to be defined. Besides those, some operations that have an inherent affinity to sequences exist.

### Intersect

The intersection of two sequences consists of all the elements that exist in both of the sequences, where an existence check is based on an equality check:

```csharp
static IEnumerable<T> Intersect<T>(this IEnumerable<T> first,
                                   IEnumerable<T> second);
static IEnumerable<T> Intersect<T>(this IEnumerable<T> first,
                                   IEnumerable<T> second,
                                   EqualityComparer<T> comparator);
```

### Union

To merge two sequences without retaining duplicates, the Union operator can be used. Just like the Intersect operator, an equality check lies at the heart of membership tests:

```
static IEnumerable<T> Union<T>(this IEnumerable<T> first,
                             IEnumerable<T> second);
static IEnumerable<T> Union<T>(this IEnumerable<T> first,
                             IEnumerable<T> second,
                             IEqualityComparer<T> comparer);
```

### Except

To retain all elements in a sequence that do not occur in another sequence, the Except operator is your workhorse. Overloads are predictable once more:

```
static IEnumerable<T> Except<T>(this IEnumerable<T> first,
                              IEnumerable<T> second);
static IEnumerable<T> Except<T>(this IEnumerable<T> first,
                              IEnumerable<T> second,
                              IEqualityComparer<T> comparer);
```

A diagram of those three operators can be found in any textbook on set theory, using Venn diagrams to represent sets.

### Concat

Concatenation is a meaningful operation on any number of things that can be done in a sequential manner. Sequences obviously have a sequential nature, so it shouldn’t be a surprise to see LINQ providing a Concat operator:

```
static IEnumerable<T> Concat<T>(this IEnumerable<T> first,
                              IEnumerable<T> second);
```

### BEWARE OF QUADRATIC EFFECTS

Although Concat is a great operator, its current use of iterators that foreach over both sequences is a little pitfall that can come costly when lots of Concat operations are strung together.

At the heart of this problem lies the fact that the iterators in C# don’t provide for nested iterators, sometimes referred to as “yield foreach.” Code generated for iterators is one of the most complex things emitted by the C# compiler, and so far there has been little incentive to introduce this optimization for yielding of entire sequences to the consumer of the iterator (as Concat does).

Further details are outside the scope of this book. If you're curious, however, just search for the "Iterators revisited: proof rules and implementation" paper on the Internet. Realistically, you are unlikely to face this problem unless you're using operators like Concat very heavily.

### Reverse

If a sequence has an order, it has an opposite order too. To reverse the order of a sequence, you can use the Reverse operator. Be aware that this operator is very eager (as in "not lazy") because it needs to iterate over the whole sequence before it can yield the first result element, which obviously is the last element of the input sequence:

```csharp
static IEnumerable<T> Reverse<T>(this IEnumerable<T> source);
```

## QUERY OPTIMIZATION

On a related note, LINQ to Objects does provide very little query optimization intelligence for a variety of reasons. One example of an optimization one could dream of is the elimination of two Reverse calls because the net effect would be the same as retaining the original sequence. Yet other more complex optimizations could involve various properties of ordering and filtering, based on the observation that some of those query operations are seemingly commutative.

However, care must be taken in a stateful and effectful language like C#. Because sequences built on iterators could exhibit certain side effects during iteration, the slightest reordering of query logic would yield a different sequencing of those effects or even eliminate some of them.

Query optimization for in-memory queries definitely could be done, and in fact technologies like Parallel LINQ do so in a rather brute-force manner by running portions of the query in parallel, also disordering sequencing of possible side effects in favor of performance. More intelligent query optimization, exploiting semantic properties of query operators, could be done but is a highly specialized task. For one thing, you don't want the cost of optimizing a query at runtime to exceed the cost of just running the nonoptimized query.

## Sequence Persistence

The lazy nature of iterators and query operators defined over them is a very nice property for a variety of reasons (as mentioned in passing). For example, it enables you to define a query once and execute it multiple times, yet providing possibly different results every time because the underlying data store might have changed. In addition to this, it allows for query optimization and wholesale remoting of a query expression into some domain-specific query language like SQL.
