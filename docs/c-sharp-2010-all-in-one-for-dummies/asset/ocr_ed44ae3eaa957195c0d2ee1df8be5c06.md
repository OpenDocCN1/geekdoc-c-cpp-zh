```
{
    //DescendingEvens -- This is a "named iterator."
    // Also demonstrates the yield break keyword
    // See how it's invoked in Main() with foreach.
    public System.Collections.IEnumerable DescendingEvens(int top, int stop)
    {
        // Start top at nearest lower even number.
        if (top % 2 != 0) // if remainder after top / 2 isn't 0.
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
```

The `DescendingEvens()` method takes two parameters (a handy addition), which set the upper limit of even numbers that you want to start from and the lower limit where you want to stop. The first even number that's generated will equal the top parameter or, if top is odd, the nearest even number below it. The last even number generated will equal the value of the stop parameter (or if stop is odd, the nearest even number above it). The method doesn't return an `int` itself, however; it returns the `IEnumerable` interface. But it still contains a `yield return` statement to return one even number and then waits until the next time it's invoked from a `foreach` loop. That's where the `int` is yielded up.

![](bbox=[0.03, 0.57, 0.11, 0.64])

REMEMBER

This example shows another collection with no underlying collection — such as `StringChunks`, mentioned earlier in this chapter. Note that this one is *computed* — the method "yield returns" a computed value rather than a stored or hard-coded value. That's another way to implement a collectionless collection. (You can also retrieve items from a data source or Web service.) And, finally, the example shows that you can iterate a collection pretty much any way you like: down instead of up or by steps of two instead of one, for example.

![](bbox=[0.03, 0.7, 0.11, 0.77])

TIP

An iterator needn't be finite, either. Consider the following iterator, which delivers a new number as long as you care to request them:

```
public System.Collections.IEnumerable PositiveIntegers()
{
    for (int i = 0; ; i++)
    {
        yield return i;
    }
}
```

![](bbox=[0.03, 0.86, 0.11, 0.93])

WARNING!

This example is, in effect, an infinite loop. You might want to pass a value used to stop the iteration. Here's how you would call `DescendingEvens()` from a `foreach` loop in `Main()`. (Calling `PositiveIntegers()` in the