Live Demo on .NET Fiddle

Any functions that both extend and return the generic IEnumerable<T> type can be used as chained clauses in a single statement. This style of fluent programming is powerful, and should be considered when creating your own extension methods.

# Section 66.2: First, FirstOrDefault, Last, LastOrDefault, Single, and SingleOrDefault

All six methods return a single value of the sequence type, and can be called with or without a predicate.

Depending on the number of elements that match the predicate or, if no predicate is supplied, the number of elements in the source sequence, they behave as follows:

# First()

+   - Returns the first element of a sequence, or the first element matching the provided predicate.
+   - If the sequence contains no elements, an InvalidOperationException is thrown with the message: "Sequence contains no elements".
+   - If the sequence contains no elements matching the provided predicate, an InvalidOperationException is thrown with the message "Sequence contains no matching element".

# Example

```
// Returns "a":
new[] { "a" }.First();

// Returns "a":
new[] { "a", "b" }.First();

// Returns "b":
new[] { "a", "b" }.First(x => x.Equals("b"));

// Returns "ba":
new[] { "ba", "be" }.First(x => x.Contains("b"));

// Throws InvalidOperationException:
new[] { "ca", "ce" }.First(x => x.Contains("b"));

// Throws InvalidOperationException:
new string[0].First();
```

Live Demo on .NET Fiddle

# FirstOrDefault()

+   - Returns the first element of a sequence, or the first element matching the provided predicate.
+   - If the sequence contains no elements, or no elements matching the provided predicate, returns the default value of the sequence type using default(T).

# Example

```
// Returns "a":
new[] { "a" }.FirstOrDefault();

// Returns "a":
new[] { "a", "b" }.FirstOrDefault();
```