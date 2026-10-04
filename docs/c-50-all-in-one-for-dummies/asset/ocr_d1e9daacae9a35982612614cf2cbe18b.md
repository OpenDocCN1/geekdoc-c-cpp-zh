This example is, in effect, an infinite loop. You might want to pass a value used to stop the iteration. Here’s how you would call DescendingEvens() from a foreach loop in Main(). (Calling PositiveIntegers() in the preceding example would work similarly.) This example demonstrates what happens if you pass odd numbers as the limit values, too — another use of the % operator:

```
// Instantiate an EvenNumbers "collection" class.
EvenNumbers en = new EvenNumbers();
// Iterate it: prints even numbers from 10 down to 4.
Console.WriteLine("\nstream of descending evens :\n");
foreach (int even in en.DescendingEvens(11, 3))
{
    Console.WriteLine(even);
}
```

This call produces a list of even-numbered integers from 10 down through 4. Notice also how the foreach is specified. You have to instantiate an EvenNumbers object (the collection class). Then, in the foreach statement, you invoke the named iterator method through that object:

```
EvenNumbers en = new EvenNumbers();
foreach(int even in en.DescendingEvens(nTop, nStop)) ...
```

If DescendingEvens() were static, you wouldn’t even need the class instance. You would call it through the class itself, as usual:

```
foreach(int even in EvenNumbers.DescendingEvens(nTop, nStop)) ...
```

# It’s a regular wetland out there!

If you can produce a “stream” of even numbers with a foreach statement, think of all the other useful things you may produce with special-purpose collections like these: streams of powers of two or of terms in a mathematical series such as prime numbers or squares — or even something exotic such as Fibonacci numbers. Or, how about a stream of random numbers (that’s what the Random class already does) or of randomly generated objects?

If you look at the PriorityQueue example in Chapter 8 of this minibook, you may want to check out the PackageFactoryWithIterator example — which appears only on this book’s website. The example illustrates the use of an iterator block to generate a stream of randomly generated objects representing packages coming into a shipping company. It performs the same function as the PackageFactory class in the original PriorityQueue example, but with an iterator block.

# Iterated property doesn’t mean “a house that keeps getting sold”

You can also implement an iterator block as a property of a class — specifically in the get() accessor for the property. In this simple class with a DoubleProp property, the property’s get() accessor acts as an iterator block to return a stream of double values: