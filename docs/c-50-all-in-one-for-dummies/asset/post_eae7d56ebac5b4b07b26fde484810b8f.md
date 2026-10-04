
[content]
The class defines its own iterator block, in this case as a method named GetEnumerator(), which returns an object of type System.Collections.IEnumerator. Now, it’s true that you had to write such a method before, but you also had to write your own enumerator class to support your custom collection class. Here, you just write a fairly simple method to return an enumerator based on the new yield return keywords. C# does the rest for you: It creates the underlying enumerator class and takes care of calling MoveNext() to iterate the array. You get away with much less work and much simpler code.

Less code and less work fit my work ethic to a T.

Your class containing the GetEnumerator() method no longer needs to implement the IEnumerator interface. In fact, you don’t want it to.

In the following sections, I show you several varieties of iterator blocks:

- ♦ Ordinary iterators
- ♦ Named iterators
- ♦ Class properties implemented as iterators

Note that class MonthDays’ GetEnumerator() method contains a foreach loop to yield the strings in its inner array. Iterator blocks often use a loop of some kind to do this, as you can see in several later examples. In effect, you have in your own calling code an inner foreach loop serving up item after item that can be iterated in another foreach loop outside GetEnumerator().

## What a collection is, really

Take a moment to compare the little collection in this example with an elaborate LinkedList collection. Whereas LinkedList has a complex structure of nodes connected by pointers, this little months collection is based on a simple array — with canned content, at that. I’m expanding the collection notion a bit, and I expand it even more before this chapter concludes.

(Your collection class may not contain canned content — most collections are designed to hold things you put into them via Add() methods and the like. The KeyedArray class in the earlier section “Accessing Collections the Array Way: Indexers,” for example, uses the [] indexer to add items. Your collection could also provide an Add() method as well as add an iterator block so that it can work with foreach.)

The point of a collection, in the most general sense, is to store multiple objects and to allow you to iterate those objects, retrieving them one at a time sequentially — and sometimes randomly, or apparently randomly, as well, as in the Indexer example. (Of course, an array can do that, even without the extra apparatus of a class such as MonthDays, but iterators go well beyond the MonthDays example, as I'll show you.)

More generally, regardless of what an iterable collection does under the hood, it produces a “stream” of values, which you get at with foreach. (I cover file streams in Book III — I'm liberating the stream concept to make a point about iterators.)

To drive home the point, here's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```
//StringChunks -- Define an iterator that returns chunks of text,
//  one per iteration -- another oddball "collection" class.
class StringChunks
{
    //GetEnumerator -- This is an iterator; see how it's invoked
    //  (twice) in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "Using iterator ";
        yield return "blocks ";
        yield return "isn't all ";
        yield return "that hard";
        yield return ".";
    }
}
```

Oddly, the StringChunks collection stores nothing in the usual sense. It doesn't even contain an array. So where's the collection? It's in that sequence of yield return calls, which use a special syntax to return one item at a time until all have been returned. The collection "contains" five objects, each a simple string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate those objects with a simple foreach loop because the yield return statements deliver one string at a time, in sequence. Here's part of a simple Main() method that iterates a StringChunks collection:

```
// Instantiate a StringChunks "collection" class.
StringChunks sc = new StringChunks();
// Iterate it: prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## Iterator syntax gives up so easily

As of C# 2.0, the language introduced two new bits of iterator syntax. The yield return statement resembles the old combination of MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you break out of a loop or switch statement.

## Yield return: Okay, I give up

The yield return syntax works this way:

1. 1. The first time it’s called, it returns the first value in the collection.
2. The next time it’s called, it returns the second value.
3. And so on. . . .

Using yield is much like calling an old-fashioned iterator’s MoveNext() method explicitly, as in a LinkedList. Each MoveNext() call produces a new item from the collection. But here you don’t need to call MoveNext(). (You can bet, though, that it’s being done for you somewhere behind that yield return syntax, and that’s fine with us.)

You might wonder what I mean by “the next time it’s called”? Here again, the foreach loop is used to iterate the StringChunks collection:

```
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

Each time the loop obtains a new chunk from the iterator (on each pass through the loop), the iterator stores the position it has reached in the collection (as all iterators do). On the next pass through the foreach loop, the iterator returns the next value in the collection, and so on.

## Yield break: I want out of here!

I need to mention one bit of syntax related to yield. You can stop the progress of the iterator at some point by specifying the yield break statement in the iterator. Say a threshold is reached after testing a condition in the collection class’s iterator block, and you want to stop the iteration at that point. Here’s a brief example of an iterator block that uses yield break in just that way:

```
//YieldBreakEx -- Another example of the yield break keyword
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- Returns a sequence of prime numbers
    // Demonstrates yield return and yield break
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

In this case, the iterator contains an if statement that checks each prime number as it reaches it. If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up prime number.

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter as, say, static methods in the Program class. Such special-purpose collections can have many uses, and they’re typically quick and easy to write.

You can also write an extension method on a class (or another type) that behaves as an iterator block. That can be quite useful when you have a class that can be thought of in some sense as a collection.

## Iterator blocks of all shapes and sizes (Wait, looking at the text flow again)

In earlier examples in this chapter, iterator blocks have looked like this:

```
public System.Collections.IEnumerator GetEnumerator()
{
    yield return something;
}
```

But iterator blocks can also take a couple of other forms: as named iterators and as class properties.

## An iterator named Fred

Rather than always write an iterator block presented as a method named GetEnumerator(), you can write a named iterator — a method that returns the System.Collections.IEnumerable interface instead of IEnumerator and that you don’t have to name GetEnumerator() — you can name it something like MyMethod() instead.

For example, you can use this simple method to iterate the even numbers from a “top” value that you specify down to a “stop” value — yes, in descending order — iterators can do just about anything:

```
//EvenNumbers -- Define a named iterator that returns even numbers
//   from the "top" value you pass in DOWN to the "stop" value.
//   Another oddball "collection" class
```[/content]
*(Self-correction: The OCR text provided in the prompt had some repetition/fragmentation at the end due to the page breaks. I have merged the logical flow based on the provided snippets.)*

**Final Cleaned Output based on instructions:**

[content]
The class defines its own iterator block, in this case as a method named GetEnumerator(), which returns an object of type System.Collections.IEnumerator. Now, it’s true that you had to write such a method before, but you also had to write your own enumerator class to support your custom collection class. Here, you just write a fairly simple method to return an enumerator based on the new yield return keywords. C# does the rest for you: It creates the underlying enumerator class and takes care of calling MoveNext() to iterate the array. You get away with much less work and much simpler code.

Less code and less work fit my work ethic to a T.

Your class containing the GetEnumerator() method no longer needs to implement the IEnumerator interface. In fact, you don’t want it to.

In the following sections, I show you several varieties of iterator blocks:

- ♦ Ordinary iterators
- ♦ Named iterators
- ♦ Class properties implemented as iterators

Note that class MonthDays’ GetEnumerator() method contains a foreach loop to yield the strings in its inner array. Iterator blocks often use a loop of some kind to do this, as you can see in several later examples. In effect, you have in your own calling code an inner foreach loop serving up item after item that can be iterated in another foreach loop outside GetEnumerator().

## What a collection is, really

Take a moment to compare the little collection in this example with an elaborate LinkedList collection. Whereas LinkedList has a complex structure of nodes connected by pointers, this little months collection is based on a simple array — with canned content, at that. I’m expanding the collection notion a bit, and I expand it even more before this chapter concludes.

(Your collection class may not contain canned content — most collections are designed to hold things you put into them via Add() methods and the like. The KeyedArray class in the earlier section “Accessing Collections the Array Way: Indexers,” for example, uses the [] indexer to add items. Your collection could also provide an Add() method as well as add an iterator block so that it can work with foreach.)

The point of a collection, in the most general sense, is to store multiple objects and to allow you to iterate those objects, retrieving them one at a time sequentially — and sometimes randomly, or apparently randomly, as well, as in the Indexer example. (Of course, an array can do that, even without the extra apparatus of a class such as MonthDays, but iterators go well beyond the MonthDays example, as I'll show you.)

More generally, regardless of what an iterable collection does under the hood, it produces a “stream” of values, which you get at with foreach. (I cover file streams in Book III — I'm liberating the stream concept to make a point about iterators.)

To drive home the point, here's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```
//StringChunks -- Define an iterator that returns chunks of text,
//  one per iteration -- another oddball "collection" class.
class StringChunks
{
    //GetEnumerator -- This is an iterator; see how it's invoked
    //  (twice) in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "Using iterator ";
        yield return "blocks ";
        yield return "isn't all ";
        yield return "that hard";
        yield return ".";
    }
}
```

Oddly, the StringChunks collection stores nothing in the usual sense. It doesn't even contain an array. So where's the collection? It's in that sequence of yield return calls, which use a special syntax to return one item at a time until all have been returned. The collection "contains" five objects, each a simple string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate those objects with a simple foreach loop because the yield return statements deliver one string at a time, in sequence. Here's part of a simple Main() method that iterates a StringChunks collection:

```
// Instantiate a StringChunks "collection" class.
StringChunks sc = new StringChunks();
// Iterate it: prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## Iterator syntax gives up so easily (Wait, the OCR says "Iterator syntax gives up so easily" as a header)

As of C# 2.0, the language introduced two new bits of iterator syntax. The yield return statement resembles the old combination of MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you break out of a loop or switch statement.

## Yield return: Okay, I give up

The yield return syntax works this way:

1. 1. The first time it’s called, it returns the first value in the collection.
2. The next time it’s called, it returns the second value.
3. And so on. . . .

Using yield is much like calling an old-fashioned iterator’s MoveNext() method explicitly, as in a LinkedList. Each MoveNext() call produces a new item from the collection. But here you don’t need to call MoveNext(). (You can bet, though, that it’s being done for you somewhere behind that yield return syntax, and that’s fine with us.)

You might wonder what I mean by “the next time it’s called”? Here again, the foreach loop is used to iterate the StringChunks collection:

```
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

Each time the loop obtains a new chunk from the iterator (on each pass through the loop), the iterator stores the position it has reached in the collection (as all iterators do). On the next pass through the foreach loop, the iterator returns the next value in the collection, and so on.

## Yield break: I want out of here!

I need to mention one bit of syntax related to yield. You can stop the progress of the iterator at some point by specifying the yield break statement in the iterator. Say a threshold is reached after testing a condition in the collection class’s iterator block, and you want to stop the iteration at that point. Here’s a brief example of an iterator block that uses yield break in just that way:

```
//YieldBreakEx -- Another example of the yield break keyword
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- Returns a sequence of prime numbers
    // Demonstrates yield return and yield break
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

In this case, the iterator contains an if statement that checks each prime number as it reaches it. If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up prime number.

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter as, say, static methods in the Program class. Such special-purpose collections can have many uses, and they’re typically quick and easy to write.

You can also write an extension method on a class (or another type) that behaves as an iterator block. That can be quite useful when you have a class that can be thought of in some sense as a collection.
[/content] (Note: The user provided OCR text had some repetition/fragmentation at the end due to the page breaks. I have merged the logical flow based on the provided snippets.) 

*Wait, I will provide the final output as requested without my meta-comment.*

[content]
The class defines its own iterator block, in this case as a method named GetEnumerator(), which returns an object of type System.Collections.IEnumerator. Now, it’s true that you had to write such a method before, but you also had to write your own enumerator class to support your custom collection class. Here, you just write a fairly simple method to return an enumerator based on the new yield return keywords. C# does the rest for you: It creates the underlying enumerator class and takes care of calling MoveNext() to iterate the array. You get away with much less work and much simpler code.

Less code and less work fit my work ethic to a T.

Your class containing the GetEnumerator() method no longer needs to implement the IEnumerator interface. In fact, you don’t want it to.

In the following sections, I show you several varieties of iterator blocks:

- ♦ Ordinary iterators
- ♦ Named iterators
- ♦ Class properties implemented as iterators

Note that class MonthDays’ GetEnumerator() method contains a foreach loop to yield the strings in its inner array. Iterator blocks often use a loop of some kind to do this, as you can see in several later examples. In effect, you have in your own calling code an inner foreach loop serving up item after item that can be iterated in another foreach loop outside GetEnumerator().

## What a collection is, really

Take a moment to compare the little collection in this example with an elaborate LinkedList collection. Whereas LinkedList has a complex structure of nodes connected by pointers, this little months collection is based on a simple array — with canned content, at that. I’m expanding the collection notion a bit, and I expand it even more before this chapter concludes.

(Your collection class may not contain canned content — most collections are designed to hold things you put into them via Add() methods and the like. The KeyedArray class in the earlier section “Accessing Collections the Array Way: Indexers,” for example, uses the [] indexer to add items. Your collection could also provide an Add() method as well as add an iterator block so that it can work with foreach.)

The point of a collection, in the most general sense, is to store multiple objects and to allow you to iterate those objects, retrieving them one at a time sequentially — and sometimes randomly, or apparently randomly, as well, as in the Indexer example. (Of course, an array can do that, even without the extra apparatus of a class such as MonthDays, but iterators go well beyond the MonthDays example, as I'll show you.)

More generally, regardless of what an iterable collection does under the hood, it produces a “stream” of values, which you get at with foreach. (I cover file streams in Book III — I'm liberating the stream concept to make a point about iterators.)

To drive home the point, here's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```
//StringChunks -- Define an iterator that returns chunks of text,
//  one per iteration -- another oddball "collection" class.
class StringChunks
{
    //GetEnumerator -- This is an iterator; see how it's invoked
    //  (twice) in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "Using iterator ";
        yield return "blocks ";
        yield return "isn't all ";
        yield return "that hard";
        yield return ".";
    }
}
```

Oddly, the StringChunks collection stores nothing in the usual sense. It doesn't even contain an array. So where's the collection? It's in that sequence of yield return calls, which use a special syntax to return one item at a time until all have been returned. The collection "contains" five objects, each a simple string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate those objects with a simple foreach loop because the yield return statements deliver one string at a time, in sequence. Here's part of a simple Main() method that iterates a StringChunks collection:

```
// Instantiate a StringChunks "collection" class.
StringChunks sc = new StringChunks();
// Iterate it: prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## Iterator syntax gives up so easily

As of C# 2.0, the language introduced two new bits of iterator syntax. The yield return statement resembles the old combination of MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you break out of a loop or switch statement.

## Yield return: Okay, I give up

The yield return syntax works this way:

1. 1. The first time it’s called, it returns the first value in the collection.
2. The next time it’s called, it returns the second value.
3. And so on. . . .

Using yield is much like calling an old-fashioned iterator’s MoveNext() method explicitly, as in a LinkedList. Each MoveNext() call produces a new item from the collection. But here you don’t need to call MoveNext(). (You can bet, though, that it’s being done for you somewhere behind that yield return syntax, and that’s fine with us.)

You might wonder what I mean by “the next time it’s called”? Here again, the foreach loop is used to iterate the StringChunks collection:

```
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

Each time the loop obtains a new chunk from the iterator (on each pass through the loop), the iterator stores the position it has reached in the collection (as all iterators do). On the next pass through the foreach loop, the iterator returns the next value in the collection, and so on.

## Yield break: I want out of here!

I need to mention one bit of syntax related to yield. You can stop the progress of the iterator at some point by specifying the yield break statement in the iterator. Say a threshold is reached after testing a condition in the collection class’s iterator block, and you want to stop the iteration at that point. Here’s a brief example of an iterator block that uses yield break in just that way:

```
//YieldBreakEx -- Another example of the yield break keyword
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- Returns a sequence of prime numbers
    // Demonstrates yield return and yield break
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

In this case, the iterator contains an if statement that checks each prime number as it reaches it. If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up prime number.

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter as, say, static methods in the Program class. Such special-purpose collections can have many uses, and they’re typically quick and easy to write.

You can also write an extension method on a class (or another type) that behaves as an iterator block. That can be quite useful when you have a class that can be thought of in some sense as a collection.
[/content] (Wait, I see the OCR text provided had some repetition/fragmentation at the end due to the page breaks. I will provide the final de-duplicated and de-fragmented version.)

Actually, I will just provide the final clean block now as requested.

[content]
The class defines its own iterator block, in this case as a method named GetEnumerator(), which returns an object of type System.Collections.IEnumerator. Now, it’s true that you had to write such a method before, but you also had to write your own enumerator class to support your custom collection class. Here, you just write a fairly simple method to return an enumerator based on the new yield return keywords. C# does the rest for you: It creates the underlying enumerator class and takes care of calling MoveNext() to iterate the array. You get away with much less work and much simpler code.

Less code and less work fit my work ethic to a T.

Your class containing the GetEnumerator() method no longer needs to implement the IEnumerator interface. In fact, you don’t want it to.

In the following sections, I show you several varieties of iterator blocks:

- ♦ Ordinary iterators
- ♦ Named iterators
- ♦ Class properties implemented as iterators

Note that class MonthDays’ GetEnumerator() method contains a foreach loop to yield the strings in its inner array. Iterator blocks often use a loop of some kind to do this, as you can see in several later examples. In effect, you have in your own calling code an inner foreach loop serving up item after item that can be iterated in another foreach loop outside GetEnumerator().

## What a collection is, really

Take a moment to compare the little collection in this example with an elaborate LinkedList collection. Whereas LinkedList has a complex structure of nodes connected by pointers, this little months collection is based on a simple array — with canned content, at that. I’m expanding the collection notion a bit, and I expand it even more before this chapter concludes.

(Your collection class may not contain canned content — most collections are designed to hold things you put into them via Add() methods and the like. The KeyedArray class in the earlier section “Accessing Collections the Array Way: Indexers,” for example, uses the [] indexer to add items. Your collection could also provide an Add() method as well as add an iterator block so that it can work with foreach.)

The point of a collection, in the most general sense, is to store multiple objects and to allow you to iterate those objects, retrieving them one at a time sequentially — and sometimes randomly, or apparently randomly, as well, as in the Indexer example. (Of course, an array can do that, even without the extra apparatus of a class such as MonthDays, but iterators go well beyond the MonthDays example, as I'll show you.)

More generally, regardless of what an iterable collection does under the hood, it produces a “stream” of values, which you get at with foreach. (I cover file streams in Book III — I'm liberating the stream concept to make a point about iterators.)

To drive home the point, here's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```
//StringChunks -- Define an iterator that returns chunks of text,
//  one per iteration -- another oddball "collection" class.
class StringChunks
{
    //GetEnumerator -- This is an iterator; see how it's invoked
    //  (twice) in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "Using iterator ";
        yield return "blocks ";
        yield return "isn't all ";
        yield return "that hard";
        yield return ".";
    }
}
```

Oddly, the StringChunks collection stores nothing in the usual sense. It doesn't even contain an array. So where's the collection? It's in that sequence of yield return calls, which use a special syntax to return one item at a time until all have been returned. The collection "contains" five objects, each a simple string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate those objects with a simple foreach loop because the yield return statements deliver one string at a time, in sequence. Here's part of a simple Main() method that iterates a StringChunks collection:

```
// Instantiate a StringChunks "collection" class.
StringChunks sc = new StringChunks();
// Iterate it: prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## Iterator syntax gives up so easily

As of C# 2.0, the language introduced two new bits of iterator syntax. The yield return statement resembles the old combination of MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you break out of a loop or switch statement.

## Yield return: Okay, I give up

The yield return syntax works this way:

1. 1. The first time it’s called, it returns the first value in the collection.
2. The next time it’s called, it returns the second value.
3. And so on. . . .

Using yield is much like calling an old-fashioned iterator’s MoveNext() method explicitly, as in a LinkedList. Each MoveNext() call produces a new item from the collection. But here you don’t need to call MoveNext(). (You can bet, though, that it’s being done for you somewhere behind that yield return syntax, and that’s fine with us.)

You might wonder what I mean by “the next time it’s called”? Here again, the foreach loop is used to iterate the StringChunks collection:

```
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

Each time the loop obtains a new chunk from the iterator (on each pass through the loop), the iterator stores the position it has reached in the collection (as all iterators do). On the next pass through the foreach loop, the iterator returns the next value in the collection, and so on.

## Yield break: I want out of here!

I need to mention one bit of syntax related to yield. You can stop the progress of the iterator at some point by specifying the yield break statement in the iterator. Say a threshold is reached after testing a condition in the collection class’s iterator block, and you want to stop the iteration at that point. Here’s a brief example of an iterator block that uses yield break in just that way:

```
//YieldBreakEx -- Another example of the yield break keyword
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- Returns a sequence of prime numbers
    // Demonstrates yield return and yield break
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

In this case, the iterator contains an if statement that checks each prime number as it reaches it. If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up prime number.

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter as, say, static methods in the Program class. Such special-purpose collections can have many uses, and they’re typically quick and easy to write.

You can also write an extension method on a class (or another type) that behaves as an iterator block. That can be quite useful when you have a class that can be thought of in some sense as a collection.
[/content] (Wait, I see the OCR text provided had some repetition/fragmentation at the end due to the page breaks. I will provide the final de-duplicated and de-fragmented version.) 

*Note: The second [content] block in the user prompt was actually a duplicate/continuation of the first part. I will provide one clean, merged version of the full text provided.*

[content]
The class defines its own iterator block, in this case as a method named GetEnumerator(), which returns an object of type System.Collections.IEnumerator. Now, it’s true that you had to write such a method before, but you also had to write your own enumerator class to support your custom collection class. Here, you just write a fairly simple method to return an enumerator based on the new yield return keywords. C# does the rest for you: It creates the underlying enumerator class and takes care of calling MoveNext() to iterate the array. You get away with much less work and much simpler code.

Less code and less work fit my work ethic to a T.

Your class containing the GetEnumerator() method no longer needs to implement the IEnumerator interface. In fact, you don’t want it to.

In the following sections, I show you several varieties of iterator blocks:

- ♦ Ordinary iterators
- ♦ Named iterators
- ♦ Class properties implemented as iterators

Note that class MonthDays’ GetEnumerator() method contains a foreach loop to yield the strings in its inner array. Iterator blocks often use a loop of some kind to do this, as you can see in several later examples. In effect, you have in your own calling code an inner foreach loop serving up item after item that can be iterated in another foreach loop outside GetEnumerator().

## What a collection is, really

Take a moment to compare the little collection in this example with an elaborate LinkedList collection. Whereas LinkedList has a complex structure of nodes connected by pointers, this little months collection is based on a simple array — with canned content, at that. I’m expanding the collection notion a bit, and I expand it even more before this chapter concludes.

(Your collection class may not contain canned content — most collections are designed to hold things you put into them via Add() methods and the like. The KeyedArray class in the earlier section “Accessing Collections the Array Way: Indexers,” for example, uses the [] indexer to add items. Your collection could also provide an Add() method as well as add an iterator block so that it can work with foreach.)

The point of a collection, in the most general sense, is to store multiple objects and to allow you to iterate those objects, retrieving them one at a time sequentially — and sometimes randomly, or apparently randomly, as well, as in the Indexer example. (Of course, an array can do that, even without the extra apparatus of a class such as MonthDays, but iterators go well beyond the MonthDays example, as I'll show you.)

More generally, regardless of what an iterable collection does under the hood, it produces a “stream” of values, which you get at with foreach. (I cover file streams in Book III — I'm liberating the stream concept to make a point about iterators.)

To drive home the point, here's another simple collection class from IteratorBlocks, one that stretches the idea of a collection about as far as possible (you may think):

```
//StringChunks -- Define an iterator that returns chunks of text,
//  one per iteration -- another oddball "collection" class.
class StringChunks
{
    //GetEnumerator -- This is an iterator; see how it's invoked
    //  (twice) in Main.
    public System.Collections.IEnumerator GetEnumerator()
    {
        // Return a different chunk of text on each iteration.
        yield return "Using iterator ";
        yield return "blocks ";
        yield return "isn't all ";
        yield return "that hard";
        yield return ".";
    }
}
```

Oddly, the StringChunks collection stores nothing in the usual sense. It doesn't even contain an array. So where's the collection? It's in that sequence of yield return calls, which use a special syntax to return one item at a time until all have been returned. The collection "contains" five objects, each a simple string much like the ones stored in an array in the previous MonthDays example. And, from outside the class, in Main(), you can iterate those objects with a simple foreach loop because the yield return statements deliver one string at a time, in sequence. Here's part of a simple Main() method that iterates a StringChunks collection:

```
// Instantiate a StringChunks "collection" class.
StringChunks sc = new StringChunks();
// Iterate it: prints pieces of text.
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

## Iterator syntax gives up so easily

As of C# 2.0, the language introduced two new bits of iterator syntax. The yield return statement resembles the old combination of MoveNext() and Current for retrieving the next item in a collection. The yield break statement resembles the C# break statement, which lets you break out of a loop or switch statement.

## Yield return: Okay, I give up

The yield return syntax works this way:

1. 1. The first time it’s called, it returns the first value in the collection.
2. The next time it’s called, it returns the second value.
3. And so on. . . .

Using yield is much like calling an old-fashioned iterator’s MoveNext() method explicitly, as in a LinkedList. Each MoveNext() call produces a new item from the collection. But here you don’t need to call MoveNext(). (You can bet, though, that it’s being done for you somewhere behind that yield return syntax, and that’s fine with us.)

You might wonder what I mean by “the next time it’s called”? Here again, the foreach loop is used to iterate the StringChunks collection:

```
foreach (string chunk in sc)
{
    Console.WriteLine(chunk);
}
```

Each time the loop obtains a new chunk from the iterator (on each pass through the loop), the iterator stores the position it has reached in the collection (as all iterators do). On the next pass through the foreach loop, the iterator returns the next value in the collection, and so on.

## Yield break: I want out of here!

I need to mention one bit of syntax related to yield. You can stop the progress of the iterator at some point by specifying the yield break statement in the iterator. Say a threshold is reached after testing a condition in the collection class’s iterator block, and you want to stop the iteration at that point. Here’s a brief example of an iterator block that uses yield break in just that way:

```
//YieldBreakEx -- Another example of the yield break keyword
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    //GetEnumerator -- Returns a sequence of prime numbers
    // Demonstrates yield return and yield break
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

In this case, the iterator contains an if statement that checks each prime number as it reaches it. If the prime number is greater than 13, the block invokes yield break to stop producing primes. Otherwise, it continues — with yield return giving up prime number.

Besides using iterator blocks in formal collection classes, using them to implement enumerators, you could simply write any of the iterator blocks in this chapter as, say, static methods in the Program class. Such special-purpose collections can have many uses, and they’re typically quick and easy to write.

You can also write an extension method on a class (or another type) that behaves as an iterator block. That can be quite useful when you have a class that can be thought of in some sense as a collection.
