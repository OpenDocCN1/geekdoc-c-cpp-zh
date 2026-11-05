# Section 66.18: Enumerating the Enumerable

The IEnumerable<T> interface is the base interface for all generic enumerators and is a quintessential part of understanding LINQ. At its core, it represents the sequence.

This underlying interface is inherited by all of the generic collections, such as Collection<T>, Array, List<T>, Dictionary<TKey, TValue> Class, and HashSet<T>.

In addition to representing the sequence, any class that inherits from IEnumerable<T> must provide an IEnumerator<T>. The enumerator exposes the iterator for the enumerable, and these two interconnected interfaces and ideas are the source of the saying "enumerate the enumerable".

"Enumerating the enumerable" is an important phrase. The enumerable is simply a structure for how to iterate, it does not hold any materialized objects. For example, when sorting, an enumerable may hold the criteria of the field to sort, but using .OrderBy() in itself will return an IEnumerable<T> which only knows how to sort. Using a call which will materialize the objects, as in iterate the set, is known as enumerating (for example .ToList()). The enumeration process will use the the enumerable definition of how in order to move through the series and return the relevant objects (in order, filtered, projected, etc.).

Only once the enumerable has been enumerated does it cause the materialization of the objects, which is when metrics like time complexity (how long it should take related to series size) and spacial complexity (how much space it should use related to series size) can be measured.

Creating your own class that inherits from IEnumerable<T> can be a little complicated depending on the underlying series that needs to be enumerable. In general it is best to use one of the existing generic collections. That said, it is also possible to inherit from the IEnumerable<T> interface without having a defined array as the underlying structure.

For example, using the Fibonacci series as the underlying sequence. Note that the call to Where simply builds an IEnumerable, and it is not until a call to enumerate that enumerable is made that any of the values are materialized.

```
```csharp
void Main()
{
    Fibonacci Fibo = new Fibonacci();
    IEnumerable<long> quadrillionplus = Fibo.Where(i => i > 100000000000);
    Console.WriteLine("Enumerable built");
    Console.WriteLine(quadrillionplus.Take(2).Sum());
    Console.WriteLine(quadrillionplus.Skip(2).First());

    IEnumerable<long> fibMod612 = Fibo.OrderBy(i => i % 612);
    Console.WriteLine("Enumerable built");
    Console.WriteLine(fibMod612.First());//smallest divisible by 612
}

public class Fibonacci : IEnumerable<long>
{
    private int max = 90;

    //Enumerator called typically from foreach
    public IEnumerator<long> GetEnumerator() {
        long n0 = 1;
        long n1 = 1;
        Console.WriteLine("Enumerating the Enumerable");
        for(int i = 0; i < max; i++){
            yield return n0+n1;
            n1 += n0;
            n0 = n1-n0;
        }
    }
}
```
```