It should always be a goal to minimize the enumerations of the source collection whenever possible. In our current incarnation of the Variance operator, there are two loops through the collection. The first in the aggregate function and the second in the call to Count in the final aggregation argument. If the source collection is indexed, then this might be avoided, but if it isn't, the Count extension method has no choice but to iterate the entire source and count as it goes.

The Aggregate operator can use any type as a seed. If we use an array as that type (double[]), we can store multiple values in each element loop. In this case, we can keep the running total of elements (count), the running sum of the elements (sum), and also the sum of the squares (sum of squares). This enables us to do a single pass through the values and have all the required data to calculate the variance value in the final Selector function of the Aggregate query operator.

Listing 9-10 shows the final refactoring, although a little more complex than its predecessors, it operates faster as seen in Table 9-2.

# Listing 9-10 Optimized sequential Variance operator code, the basis of our parallel implementation

```
public static double Variance(
    this IEnumerable<int> source)
{
    // optimization 2 - removing count and mean calcs
    return source.Aggregate(

        // seed - array of three doubles
        new double[3] { 0.0, 0.0, 0.0 },

        // item aggregation function, run for each element
        (subtotal, item) =>
        {
            subtotal[0]++; // count
            subtotal[1] += item; // sum
            // sum of squares
            subtotal[2] += (double)item * (double)item;
            return subtotal;
        }
    );
```