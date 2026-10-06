// Returns the last element in a sequence. If the
// sequence is empty a default (TSource) instance
// is returned.
public static TSource LastOrDefault<TSource>(
 this IEnumerable<TSource> source);

// Returns the last element in a sequence that
// satisfies the predicate function. If the
// sequence is empty or no elements satisfy the
// predicate, a default (TSource) instance
// is returned.
public static TSource LastOrDefault<TSource>(
 this IEnumerable<TSource> source,
 Func<TSource, bool> predicate);

To demonstrate the use of the Last and LastOrDefault operators, Listing
5-18 calls these operators with a simple array of integers and an empty array.
To avoid an exception being thrown when there is no last element or last
element that passes the predicate function, the LastOrDefault operator is
used instead. The Console output from this example is shown in Output 5-9.

# Listing 5-18 The Last operator returns the last element in a sequence—see Output 5-9

```
var nums = new int[] { 1, 2, 3, 4, 5 };
var empty = new int[] { };

// get the last element
var last = nums.Last();

// get the last element < 4
var third = nums.Last(i => i < 4);

// ERROR: System.InvalidOperationException
var error = empty.Last();

// returns a default(T), 0 for a value int type.
var no_error = empty.LastOrDefault();

// ERROR: System.InvalidOperationException.
// No value > 10 in this sequence.
var error = nums.Last(i => i > 10);
```