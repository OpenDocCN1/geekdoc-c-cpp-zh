# **Why Two Interfaces?**

By keeping a distinction between an enumerable object (**IEnumerable<T>**) and an enumerator over that object (**IEnumerator<T>**), you can perform multiple iterations over the same enumerable source. Obviously, you don’t want the iterations interfering with each other as they move through the data, so you need two independent representations (enumerators) providing you the current data element and the mechanism to move to the next one.

# **By the Way**

Fortunately, all the generic collections (and the non-generic ones as well) implement **IEnumerable<T>**, **IEnumerable**, **IEnumerator<T>**, and **IEnumerator** already, so you can use them without the extra complexity of writing the iterator mechanism yourself.

What happens if you want your own class to offer similar behavior? You can certainly make your class implement **IEnumerable<T>** and then write your own **IEnumerator<T>** derived class, but doing so isn’t necessary if you use an iterator. This enables the compiler to do all the hard work for you.

An iterator is a method, property get accessor, or operator that returns an ordered sequence of values all of which are the same type. The `yield` keyword tells the compiler the block it appears in is an iterator block. A `yield` return statement returns each element, and a `yield` break statement ends the iteration. The body of such an iterator method, accessor, or operator has the following restrictions:

+   ▶ Unsafe blocks are not permitted.

▶ Parameters cannot be ref or out parameters.

▶ A `yield` return statement cannot be located anywhere within a try-catch block. It can be located in a try block if it is followed by a `finally` block.

▶ A `yield` break statement can be located in either a try block or a catch block, but not a `finally` block.

▶ A `yield` statement cannot be in an anonymous method.

Listing 9.7 shows code that would produce the same output as that shown in Listing 9.6 using an iterator instead.

# **LISTING 9.7 A Simple Iterator**

```
class Program
{
static IEnumerable<int> GetEvenNumbers()
{
yield return 0;
yield return 2;
```