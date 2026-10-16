
`LINQIntro/Program.cs`:

```csharp
static void ExtensionMethods()
{
    var champions = new List<Racer>(Formula1.GetChampions());
    IEnumerable<Racer> brazilChampions =
        champions.Where(r => r.Country == "Brazil").
            OrderByDescending(r => r.Wins).
            Select(r => r);

    foreach (Racer r in brazilChampions)
    {
        WriteLine($"{r:A}");
    }
}
```

## Deferred Query Execution

During runtime, the query expression does not run immediately as it is defined. The query runs only when the items are iterated.

Let’s have a look once more at the extension method `Where`. This extension method makes use of the `yield return` statement to return the elements where the predicate is `true`. Because the `yield return` statement is used, the compiler creates an enumerator and returns the items as soon as they are accessed from the enumeration:

```csharp
public static IEnumerable<T> Where<T>(this IEnumerable<T> source,
    Func<T, bool> predicate)
{
    foreach (T item in source)
    {
        if (predicate(item))
        {
            yield return item;
        }
    }
}
```

This has a very interesting and important effect. In the following example a collection of string elements is created and filled with first names. Next, a query is defined to get all names from the collection whose first letter is J. The collection should also be sorted. The iteration does not happen when the query is defined. Instead, the iteration happens with the `foreach` statement, where all items are iterated. Only one element of the collection fulfills the requirements of the `where` expression by starting with the letter J: Juan. After the iteration is done and Juan is written to the console, four new names are added to the collection. Then the iteration is done again:

```csharp
var names = new List<string>
{ "Nino", "Alberto", "Juan", "Mike", "Phil" };

var namesWithJ = from n in names
                 where n.StartsWith("J")
                 orderby n
                 select n;

WriteLine("First iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
WriteLine();
names.Add("John");
names.Add("Jim");
names.Add("Jack");
names.Add("Denny");

WriteLine("Second iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
```

Because the iteration does not happen when the query is defined, but does happen with every `foreach`, changes can be seen, as the output from the application demonstrates:

```
First iteration
Juan

Second iteration
Jack
Jim
John
Juan
```

Of course, you also must be aware that the extension methods are invoked every time the query is used within an iteration. Most of the time this is very practical, because you can detect changes in the source data. However, sometimes this is impractical. You can change this behavior by invoking the extension methods `ToArray`, `ToList`, and the like. In the following example, you can see that `ToList` iterates through the collection immediately and returns a collection implementing `IList<string>`. The returned list is then iterated through twice; in between iterations, the data source gets new names:

```csharp
var names = new List<string>
{ "Nino", "Alberto", "Juan", "Mike", "Phil" };
var namesWithJ = (from n in names
                  where n.StartsWith("J")
                  orderby n
                  select n).ToList();

WriteLine("First iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
WriteLine();
names.Add("John");
names.Add("Jim");
names.Add("Jack");
names.Add("Denny");
WriteLine("Second iteration");
foreach (string name in namesWithJ)
{
    WriteLine(name);
}
```

| Operator | Description |
| --- | --- |
| `GroupBy`<br>`ToLookup` | `GroupBy` operator groups elements with a common key. `ToLookup` groups the elements by creating a one-to-many dictionary. |
| `Any`<br>`All`<br>`Contains` | *Quantifier operators* return a Boolean value if elements of the sequence satisfy a specific condition. `Any`, `All`, and `Contains` are quantifier operators. `Any` determines whether any element in the collection satisfies a predicate function; `All` determines whether all elements in the collection satisfy a predicate. `Contains` checks whether a specific element is in the collection. |
| `Take`<br>`Skip`<br>`TakeWhile`<br>`SkipWhile` | *Partitioning operators* return a subset of the collection. `Take`, `Skip`, `TakeWhile`, and `SkipWhile` are partitioning operators. With these, you get a partial result. With `Take`, you have to specify the number of elements to take from the collection; `Skip` ignores the specified number of elements and takes the rest. `TakeWhile` takes the elements as long as a condition is true. `SkipWhile` skips the elements as long as the condition is true. |
| `Distinct`<br>`Union`<br>`Intersect`<br>`Except`<br>`Zip` | *Set operators* return a collection set. `Distinct` removes duplicates from a collection. With the exception of `Distinct`, the other set operators require two collections. `Union` returns unique elements that appear in either of the two collections. `Intersect` returns elements that appear in both collections. `Except` returns elements that appear in just one collection. `Zip` combines two collections into one. |
| `First`<br>`FirstOrDefault`<br>`Last`<br>`LastOrDefault`<br>`ElementAt`<br>`ElementAtOrDefault`<br>`Single`<br>`SingleOrDefault` | *Element operators* return just one element. `First` returns the first element that satisfies a condition. `FirstOrDefault` is similar to `First`, but it returns a default value of the type if the element is not found. `Last` returns the last element that satisfies a condition. With `ElementAt`, you specify the position of the element to return. `Single` returns only the one element that satisfies a condition. If more than one element satisfies the condition, an exception is thrown. All the `XXOrDefault` methods are similar to the methods that start with the same prefix, but they return the default value of the type if the element is not found. |
| `Count`<br>`Sum`<br>`Min`<br>`Max`<br>`Average`<br>`Aggregate` | *Aggregate operators* compute a single value from a collection. With aggregate operators, you can get the sum of all values, the number of all elements, the element with the lowest or highest value, an average number, and so on. |
| `ToArray`<br>`AsEnumerable`<br>`ToList`<br>`ToDictionary`<br>`Cast<TResult>` | *Conversion operators* convert the collection to an array, `IEnumerable`, `IList`, `IDictionary`, and so on. The `Cast` method casts every item of the collection to the generic argument type. |
| `Empty`<br>`Range`<br>`Repeat` | *Generation operators* return a new sequence. The collection is empty using the `Empty` operator; `Range` returns a sequence of numbers, and `Repeat` returns a collection with one repeated value. |

The following sections provide examples demonstrating how to use these operators.

## Filtering

This section looks at some examples for a query.

With the `where` clause, you can combine multiple expressions—for example, get only the racers from Brazil and Austria who won more than 15 races. The result type of the expression passed to the `where` clause just needs to be of type `bool`:

```csharp
var racers = from r in Formula1.GetChampions()
             where r.Wins > 15 &&
                 (r.Country == "Brazil" || r.Country == "Austria")
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

```csharp
var racers = Formula1.GetChampions().
    Where(r => r.Wins > 15 &&
        (r.Country == "Brazil" || r.Country == "Austria")).
    Select(r => r);
```
