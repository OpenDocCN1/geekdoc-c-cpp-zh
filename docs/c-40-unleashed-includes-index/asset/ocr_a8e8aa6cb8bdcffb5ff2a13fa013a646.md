```
Order By Memory Descending
Select ProcessName, Memory
```

Other operators, such as Take, Skip, and Distinct, also have syntactical language integration in Visual Basic.

# Predicates

In the world of LINQ, predicate operators express Boolean-valued truths about sequences and their elements. Operators such as Any and All should sound familiar to those who’ve learned basics of predicate logic. Other operators include SequenceEqual (to compare two sequences) and Contains (to ask membership questions about elements in sequences). Let’s take a look at all of those.

# All and Any

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

In fact, those operators also special forms of aggregation operations. For example, All can be written in terms of an aggregation using &&. One subtle difference is that the All and Any operators will stop iteration over the source sequence as soon as the result is known. All will return false as soon as an element doesn’t match the predicate; Any will return true as soon as an element does match the predicate:

```
var allEven = new[] { 1, 2, 3 }.Aggregate(true,
    (all, x) => all && x % 2 == 0);
```

# Contains

As the name implies, Contains performs a membership check for a given element in a given sequence. Two overloads exist, one with and one without an equality comparer: