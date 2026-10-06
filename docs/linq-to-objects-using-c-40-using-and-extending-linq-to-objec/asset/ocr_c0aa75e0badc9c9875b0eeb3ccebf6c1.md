```
// result selector function
// (finesses the final sum into the variance)
// mean = sum / count
// variance = (sum_sqr sum * mean) / (n - 1)
result =>
(result[2] - (result[1] * (result[1] / result[0]))
/ (result[0] - 1)
);
```

As Table 9.2 shows, the performance benefits gained by optimizing the sequential algorithm are substantial—more substantial than relying on parallel optimizations alone.
Now that the Variance operator has been written, the StandardDeviation operator simply builds upon the result as shown in Listing 9-11. This example also demonstrates the generally accepted pattern of defining an overload that takes a value Selector function—this follows the pattern set forth by the supplied aggregation standard query operators and is recommended.

# Listing 9-11 Sequential implementation of the StandardDeviation operator

```
public static double StandardDeviation(
    this IEnumerable<int> source)
{
    return Math.Sqrt(source.Variance());
}

public static double StandardDeviation<T>(
    this IEnumerable<T> source,
    Func<T, int> selector)
{
    return StandardDeviation(
    Enumerable.Select(source, selector));
}
```