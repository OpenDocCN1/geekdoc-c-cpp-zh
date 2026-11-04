```
```csharp
//YieldBreakEx -- Another example of the yield break keyword
class YieldBreakEx
{
    int[] primes = { 2, 3, 5, 7, 11, 13, 17, 19, 23 };
    // GetEnumerator -- Returns a sequence of prime numbers
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
```

```
```csharp
//EvenNumbers -- Define a named iterator that returns even numbers
// from the "top" value you pass in DOWN to the "stop" value.
// Another oddball "collection" class
class EvenNumbers
{
    //DescendingEvens -- This is a "named iterator."
    // Also demonstrates the yield break keyword.
    // See how it's invoked in Main() with foreach.
    public System.Collections.IEnumerable DescendingEvens(int top, int stop)
    {
        // Start top at nearest lower even number.
        if (top % 2 != 0) // If remainder after top / 2 isn't 0.
            top -= 1;
        // Iterate from top down to nearest even above stop.
        for (int i = top; i >= stop; i -= 2)
        {
            if (i < stop)
                yield break;
            // Return the next even number on each iteration.
            yield return i;
        }
    }
}
```
```

```
```csharp
//PropertyIterator -- Demonstrate implementing a class
// property's get accessor as an iterator block
class PropertyIterator
{
    double[] doubles = { 1.0, 2.0, 3.5, 4.67 };
    // DoubleProp -- A "get" property with an iterator block
    public System.Collections.IEnumerable DoubleProp
    {
        get
        {
            foreach (double db in doubles)
            {
                yield return db;
            }
        }
    }
}
```
```