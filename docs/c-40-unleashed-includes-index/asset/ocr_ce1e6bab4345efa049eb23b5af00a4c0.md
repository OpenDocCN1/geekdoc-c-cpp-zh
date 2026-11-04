# "DON'T CARE" PARAMETERS

Some functional languages provide a don't care identifier that can be used to state that a parameter to a function will not be used. Typically, the underscore character is used. Because this is a valid identifier in C#, you can play the same trick:

```
```csharp
source.Aggregate(0, (n, _) => n + 1)
```
```

Notice, though, an underscore is just an identifier like any other and therefore is subject to all rules that apply to identifiers, their declaration, and surrounding scopes. If multiple parameters to a function can be ignored, you won't be able to use an underscore to express the "don't care" characteristic on all of those. In functional languages, this "wildcard" syntax is really a special kind of identifier that allows such uses, but in C# it's an identifier like any other.

Additional overloads exist to compute the number of elements in a sequence that match a certain predicate:

```
```csharp
int Count<T>(this IEnumerable<T> source, Func<T, bool> predicate);
long LongCount<T>(this IEnumerable<T> source, Func<T, bool> predicate);
```
```

Use of those overloads is merely the same as using the Where operator in conjunction with the simple form (without a predicate) of Count or LongCount.

# Sum and Average

Sum and Average are closely related and compute what you expect them do. Lots of overloads exist for those aggregation operations, for all numeric primitives types and their nullable variants. Let's start by looking at Sum, illustrating the two overloads that are available for the various numeric types:

```
```csharp
static int Sum(this IEnumerable<int> source);
static int Sum<TSource>(this IEnumerable<TSource> source,
    Func<TSource, int> selector);
```
```

The first overload acts directly on a sequence of numeric values, whereas the latter carries out a projection first. The second form can be written in terms of Select followed by the first form of Sum, too.

When the result overflows the precision of the numeric type, an OverflowException is generated. If this is not desired, you can always use the general Aggregate operator to compute a sum manually, possibly returning a more precise type. An example to sum 32-bit integer values into a 64-bit integer, without using the checked keyword, is shown here:

```
```csharp
source.Aggregate(0L, (long sum, int item) => sum + item)
```
```