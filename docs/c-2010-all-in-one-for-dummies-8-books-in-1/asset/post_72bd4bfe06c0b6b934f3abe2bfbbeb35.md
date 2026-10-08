
## 156 Looping Around the Iterator Block

More generally, regardless of what an iterable collection does under the hood, it produces a "stream" of values, which you get with foreach. (I cover streams in Book III — I'm liberating the concept to make a point about iterators.)

To drive the home point, there's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```csharp
//StringChunks -- Define an iterable returns chunks of text,
// one per iteration -- another oddball 'collection' class.
class StringChunks
{
    // GetEnumerator -- This is an iterator; see how it's invoked
    // twice in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "using iterator *;";
        yield return "blocks";
        yield return "isn't all";
        yield return "that hard";
        yield return "";
    }
}
```

Oddly, the StringChunks stores nothing in the usual sense. It doesn't contain an array. So where's the collection? It's in sequence of yield until all have been returned. The collection "contains" five objects, each a single string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate these objects with a simple foreach loop because the yield returns one string at a time, in sequence. Here's a simple main method:

```csharp
// Instantiate a StringChunks 'collection' class.
StringChunks sc = new StringChunks();
// Iterate it: it prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## Iterator syntax gives up so easily

As of C# 2.0, the language introduced two bits of iterator syntax. The yield return statement resembles MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you out of a loop or switch statement.

### Yield return: Okay, I give up

The yield return syntax works this way:

- 1. The first time it's called, it returns the first value in the collection.
- 2. The next time it's called, it returns the second value.
- 3. And so on. . . .

Using yield is much like an old-fashioned iterator's MoveNext() method explicitly, as in the LinkedList code. Each MoveNext() call produces a new item from the collection. But here you don't need to call MoveNext(). (You can bet, though, it's being done for you somewhere behind yield return syntax, and in line with us.)

You might wonder what I mean by “the next time it's called?” Here again, the foreach loop is used to iterate the StringChunks collection:

```csharp
foreach (string chunk in sc)
    Console.WriteLine(chunk);
```

Each time the loop obtains a new chunk from the iterator (on each pass through the loop), the iterator stores its position in the collection (as all iterators). On the next pass through the foreach loop, the iterator returns the next value in the collection, and so on.

### Yield break: I want out of here!

I need to mention one bit of syntax related to yield. You can stop the progress of the iterator at some point by specifying the yield break statement in the iterator. A threshold is reached after testing a condition in the collection's iterator block, and you want to stop the iterator at that point. Here's a brief example of an iterator block that uses yield break in that way:

```csharp
//YieldBreakEx -- Another example of a yield break keyword
class YieldBreakEx{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- Returns a sequence of prime numbers
    // demonstrates yield return and yield break
    public System.Collections.IEnumerator GetEnumerator()
    {
        foreach (int prime in primes)
        {
            if (prime > 13) yield break;
            yield return prime;
        }
    }
}
```

In this case, the iterator block contains an if statement that checks each prime number the iterator reaches it in the collection (using another foreach inside the iterator, by the way). If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up another prime number until the collection is exhausted.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_0.png)

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter, as static methods parallel to Main() in the Program class. cases as many of the examples in this chapter, the collection is inside the method. Special-purpose collections can have many uses, and they're typically quick and easy to use.

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_1.png)

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. That can be quite useful when you have a class that be thought of an iterator block. You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

```csharp
//Numbers Define an iterator returns even numbers
class Numbers
{
    yield return 2;
    yield return 4;
    yield return 6;

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_2.png)

### Iterator forms

In this case, the iterator block contains an if statement that checks each prime number the iterator reaches it in the collection (using another foreach inside the iterator, by the way). If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up another prime number until the collection is exhausted.

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter, as static methods parallel to Main() in the Program class. cases as many of the examples in this chapter, the collection is inside the method. Special-purpose collections can have many uses, and they're typically quick and easy to use.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block.

You can also make an extension on a class (another type) that behaves as an iterator block. That can be quite useful when you have a class that be thought of an iterator block. This method takes two parameters (a handy addition), which set the upper limit of even numbers that you want to start from and the lower limit you want to stop. The first even number generated will equal top (if odd, the nearest even below it). The last even number will equal the stop parameter (if stop is odd, the nearest even above it). The method does not return an int, however; it returns the IEnumerable. It still contains a yield statement to return one number and then waits until the next time it's invoked from foreach. That's where it is yielded. This example shows another collection with no underlying collection - such as StringChunks, mentioned earlier in this chapter. Note that this one is computed - the method "yield" returns a value rather than a hard-coded value. That's another way to implement a complex collection. (You can also retrieve items from a data source or service.) And, finally, the example shows that you can collect it with any way you like: instead of or by steps of one, for example.

An iterator needn't be finite, either. Consider the following iterator, which delivers a new number as long as you request them:

```csharp
public System.Collections.IEnumerable PositiveIntegers()
{
    for (int i = 0; ; i++)
    {
        yield i;
    }
}
```

This example is, in effect, an infinite loop. You might want to pass a value to stop the iteration. Here's how you would call DescendingEvents() from a foreach loop in Main(). (Calling PositiveIntegers() in the

```csharp
//DescendingEvents - This is a yield keyword
// See how it's invoked in Main().
public System.Collections.IEnumerable DescendingEvents(int top, int stop)
{
    // Start at even number.
    if (top % 2 != 0)
        top--;
    // Iterate from top down to stop.
    for (int i = top; i >= stop; i -= 2)
    {
        if (i < stop)
            break;
        // Return the next even number on each iteration.
        yield i;
    }
}
```

```csharp
//Numbers Define an iterator returns even numbers
class Numbers
{
    yield return 2;
    yield return 4;
    yield return 6;
```

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_183_2.png)
