
```
// If this would be here, there'd be an additional state.
yield return default(T);
}
```

Finally, we've ended up with state 3, which should correspond to retrieving the next objects from the tail enumerator, exposing them to the iterator's consumer. This is done by a simple branch (`goto`) instruction jumping inside the loop from state 2:

```
bool MoveNext() {
    try {
        switch (_state) {
            case 0:
                ...
            case 1:
                _enum = _tail.GetEnumerator();
                while (_enum.MoveNext()) {
                    _current = _enum.Current; // yield return item;
                    _state = 3;
                    return true;                // we got an object in Current
Resume:
                }
                Finally();
                break;
            case 3:
                goto Resume;
        }
        return false;
    }
```

This causes the while loop to reevaluate `_enum.MoveNext()`, possibly yielding a next object by means of the same logic we saw before. If the call returned false, we get to the `Finally()` cleanup call once more and break out of the switch statement, causing the iterator to return false to the caller.

In short, iterators are not that frightening from the inside, though the compiler has to tear apart the iterator block's code quite a bit. Luckily, you don't need to know much (or anything) about this, but it still makes sense to get a feel for the plumbing required to realize iterators because it clearly shows their execution model.

Feel free to dig a little deeper into the generated code using .NET Reflector, which you should put in .NET 2.0 decompilation mode to clearly see the plumbing. Also try to reverse-engineer a more complex iterator with more yield statements, nested loops, and so on. The key takeaway message is that every yield statement needs to cause the iterator to suspend by returning from the `MoveNext` method. And to resume at the proper point, there needs to be enough captured state in the iterator object. Figure 20.7 shows the innards of an iterator, where you can clearly see a switch-table to keep track of the next operations to carry out upon a `MoveNext` call.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_1019_0.png)

FIGURE 20.7 An iterator unraveled.

## Standard Query Operators

One of the core strengths of LINQ is the fact it unifies query operators across different data domains, ranging from in-memory objects to relational databases. To do so, it not only provides query syntax for mainstream languages like C# and Visual Basic, it also establishes a set of commonly used query operators.

In this section, we take a look at all the standard query operators that ship with the .NET Framework, including some of their less commonly used, but useful, overloads. Keep in mind that some of those are exposed through language integrated query syntax, whereas others aren't. For the latter set of operators, you can just use method invocation syntax to use them.

### Source Generators

Source generators comprise our first big category of standard query operators. Although different source objects can be LINQ-enabled (for example, by implementing `IEnumerable<T>` for local query execution or by implementing `IQueryable<T>` for remote query execution; for example, as used in LINQ to SQL), it sometimes makes sense to create a sequence on the fly.

All the methods discussed here live on the `Enumerable` type and provide a means to generate a source without persisting it in memory, thanks to lazy evaluation. Obviously, you can also use arrays, lists, or other collection types as in-memory data sources, but with immediate memory-allocation needs.

### Range

The first source generator is called `Range` and produces `Int32` values starting from a given number. Its second parameter is used to specify how many numbers to yield to the consumer:

```
IEnumerable<int> firstTen = Enumerable.Range(0, 10); // { 0 .. 9 }
```

Although its use might seem limited, combined with other query operators it can produce more useful objects (for example, characters):

```
IEnumerable<char> aToz = Enumerable.Range(0, 26).Select(i => (char)('a' + i));
```

Also for simple query operator exploration, the use of `Range` provides a simple way to create a sequence to experiment with.

### Repeat

Given an element, it's sometimes useful to repeat it multiple times to create a sequence with a constant value. This can be achieved using the `Repeat` operator:

```
IEnumerable<string> heyHeyHey = Enumerable.Repeat("Hey", 3);
```

Notice how the type of the resulting sequence is inferred from the element specified as the first parameter to `Repeat`.

### Empty

In certain scenarios where an `IEnumerable<T>` is expected, you want to pass a default sequence. `Empty` produces such a statically typed sequence with no elements in it:

```
IEnumerable<int> nothing = Enumerable.Empty<int>();
```

### Return

A missing operator in the standard set of query operators is `Return`, or `Singleton`, which would return a sequence with a single given element:

```
static IEnumerable<T> Return<T>(T element) {
    yield return element;
}
```

This can easily be achieved by creating a single-element array instead, which as we know implements `IEnumerable<T>`. This operator is interesting because the mathematical foundation of query operators, called monads, is based on two essential operators: `Bind` and `Return`. The latter was just shown and has no presence in the LINQ operators, but the former one is actually there. It's called `SelectMany` and provides a way to combine sequences, as you will see in the “Projection” section, where we discuss this operator.

### DefaultIfEmpty

Where `Empty` sort of plays the role of a null reference, `DefaultIfEmpty` plays the role of the null coalescing `??` operator. If the sequence given to this operator is empty, it yield returns a single “default” element. This default element can either be specified explicitly or inferred based on the sequence's element type:

```
var src1 = Enumerable.Empty<int>();
var res1 = src1.DefaultIfEmpty(); // { 0 }
var res2 = src1.DefaultIfEmpty(99); // { 99 }

var src2 = Enumerable.Range(1, 9);
var res3 = src2.DefaultIfEmpty(); // { 1 .. 9 }
```

This operator has quite limited use, but it's nevertheless good to know about.

### Restriction

One of the most common query operations is obviously to filter out elements based on certain conditions. Those conditions can either be on a per-element basis (such as with the `Where` operator) or have a more global nature (as with `Skip` or `Take`). In essence, we're talking here about horizontal partitioning where a given number of objects in the input sequence are filtered down to a subset. Those restriction operators don't change the shape of the data and preserve the type of the input sequence.

### Where

The first restriction operator is one we're already familiar with. The `Where` operator evaluates a condition for each element in the input sequence, only retaining objects for which the condition evaluated to true. Two overloads exist:

```
static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, bool> predicate);
static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, int, bool> predicate);
```

From our discussion about query expression syntax and iterators, we remember the first one quite well. Iterating over the `source` parameter, the operator feeds every object into the predicate function. When that function evaluates to true, it yields the object into the output sequence. Any Boolean-returning expression will do, no matter how complex you make it. For illustration purposes, we keep the predicate function simple:

```
// { "Bart", "Lisa" }
var res = new [] { "Bart", "Homer", "Lisa" }.Where(s => s.Length == 4);
```

The second overload feeds an additional argument to the predicate function, standing for the zero-based index of the element in the input sequence. One example use is shown here, retaining elements at even positions:

```
// { "Zero", "Two" }
var res = new [] { "Zero", "One", "Two", "Three" }.Where((s, i) => i % 2 == 0);
```

Here, `s` stands for the string objects in the input sequence, while `i` stands for the index of the object in the input sequence. We're not using `s` (though we obviously could) to do the index-based filtering here.

### Distinct

Sequences may contain duplicate objects, which can be undesirable. To get rid of those duplicate entries, the `Distinct` operator can be used. Because this deals with equality checks between objects, you can expect two overloads (one that uses the default comparer for the element type and another that allows the use of a specific equality comparer):

```
static IEnumerable<T> Distinct<T>(this IEnumerable<T> source);
static IEnumerable<T> Distinct<T>(this IEnumerable<T> source,
    IEqualityComparer<T> comparer);
```

Use is quite straightforward:

```
var nums = new [] { 5, 2, 1, 3, 1, 4, 5 }.Distinct(); // { 5, 2, 1, 3, 4 }
```

I leave the use of the more specialized overload to your imagination. For more information about `IEqualityComparer<T>`, refer to our discussion about collection types in Chapter 16, “Collection Types.” A sample use is to implement a comparer for `Person` objects, only looking at the person’s identification number to determine whether objects are equal. However, if those are the semantics for a `Person` object, you most likely already have an overridden `Equals` method in place, which will be picked up by the default equality comparer for the `Person` type.

### Skip and SkipWhile

To skip a number of elements from the beginning of a sequence, the `Skip` operator can be used. Its more general-purpose `SkipWhile` brother can be used to skip elements as long as a given condition holds true. A few examples tell it all:

```
var res1 = Enumerable.Range(0, 10).Skip(5); // { 5, 6, 7, 8, 9 }
var res2 = Enumerable.Range(0, 10).SkipWhile(n => n < 8); // { 8, 9 }
```

If the skip count is longer than the input sequence length, or if the predicate never flips to false, the resulting sequence is empty. Notice `SkipWhile` is obviously not the same as a simple `Where`:

```
var res1 = new [] { 1, 2, 3, 4, 3, 2, 1 }.SkipWhile(n => n < 4); // { 4, 3, 2, 1 }
var res2 = new [] { 1, 2, 3, 4, 3, 2, 1 }.Where(n => n >= 4); // { 4 }
```
