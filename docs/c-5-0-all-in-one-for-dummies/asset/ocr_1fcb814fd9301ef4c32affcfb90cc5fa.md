extra apparatus of a class such as MonthDays, but iterators go well beyond the MonthDays example, as I'll show you.)

More generally, regardless of what an iterable collection does under the hood, it produces a "stream" of values, which you get at with foreach. (I cover file streams in Book III — I'm liberating the stream concept to make a point about iterators.)

To drive home the point, here's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```
// StringChunks -- Define an iterator that returns chunks of text,
// one per iteration -- another oddball "collection" class.
class StringChunks
{
    // GetEnumerator -- This is an iterator; see how it's invoked
    // (twice) in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "Using iterator ";
        yield return "blocks ";
        // yield return "isn't all ";
        yield return "that hard";
        yield return ".";
    }
}
```

Oddly, the StringChunks collection stores nothing in the usual sense. It doesn't even contain an array. So where's the collection? It's in that sequence of yield return calls, which use a special syntax to return one item at a time until all have been returned. The collection "contains" five objects, each a simple string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate those objects with a simple foreach loop because the yield return statements deliver one string at a time, in sequence. Here's part of a simple Main() method that iterates a StringChunks collection:

```
// Instantiate a StringChunks "collection" class.
StringChunks sc = new StringChunks();
// Iterate in: prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

# Iterator syntax gives up so easily

As of C# 2.0, the language introduced two new bits of iterator syntax. The yield return statement resembles the old combination of MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you break out of a loop or switch statement.