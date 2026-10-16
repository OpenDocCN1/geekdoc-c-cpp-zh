| Max\nAverage\nAggregate | average number, and so on. |
| ToArray\nAsEnumerable\nToList\nToDictionary\nCast<TResult> | *Conversion operators* convert the collection to an array: `IEnumerable`, `IList`, `IDictionary`, and so on. The `Cast` method casts every item of the collection to the generic argument type. |
| Empty\nRange\nRepeat | *Generation* operators return a new sequence. The collection is empty using the `Empty` operator; `Range` returns a sequence of numbers, and `Repeat` returns a collection with one repeated value. |

The following sections provide examples demonstrating how to use these operators.

# Filtering

This section looks at some examples for a query.

With the `where` clause, you can combine multiple expressions—for example, get only the racers from Brazil and Austria who won more than 15 races. The result type of the expression passed to the `where` clause just needs to be of type `bool`:

```
var racers = from r in Formula1.GetChampions()
    where r.Wins > 15 &&
        (r.Country =="Brazil" || r.Country =="Austria")
    select r;

foreach (var r in racers)
{
    WriteLine($"{r:A}");
}
```

Starting the program with this LINQ query returns Niki Lauda, Nelson Piquet, and Ayrton Senna, as shown here:

```
Niki Lauda, Austria, Starts: 173, Wins: 25
Nelson Piquet, Brazil, Starts: 204, Wins: 23
Ayrton Senna, Brazil, Starts: 161, Wins: 41
```

Not all queries can be done with the LINQ query syntax, and not all extension methods are mapped to LINQ query clauses. Advanced queries require using extension methods. To better understand complex queries with extension methods, it’s good to see how simple queries are mapped. Using the extension methods `Where` and `Select` produces a query very similar to the LINQ query done before:

```
var racers = Formula1.GetChampions().
    Where(r => r.Wins > 15 &&
        (r.Country =="Brazil" || r.Country =="Austria")).
```