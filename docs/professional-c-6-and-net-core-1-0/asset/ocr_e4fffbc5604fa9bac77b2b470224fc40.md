Argentina: Fangio, Juan Manuel
Australia: Brabham, Jack
Australia: Jones, Alan
Austria: Lauda, Niki
Austria: Rindt, Jochen
Brazil: Fittipaldi, Emerson
Brazil: Piquet, Nelson
Brazil: Senna, Ayrton
Canada: Villeneuve, Jacques
Finland: Hakkinen, Mika

Doing the same with extension methods makes use of the `OrderBy` and `ThenBy` methods:

```
var racers = Formula1.GetChampions()
    .OrderBy(r => r.Country)
    .ThenBy(r => r.LastName)
    .ThenBy(r => r.FirstName)
    .Take(10);
```

# Grouping

To group query results based on a key value, the `group` clause can be used. Now the Formula-1 champions should be grouped by country, and the number of champions within a country should be listed. The clause `group r by r.Country into g` groups all the racers based on the `Country` property and defines a new identifier `g` that can be used later to access the group result information. The result from the `group` clause is ordered based on the extension method `Count` that is applied on the group result; and if the count is the same, the ordering is done based on the key. This is the country because this was the key used for grouping. The `where` clause filters the results based on groups that have at least two items, and the `select` clause creates an anonymous type with the `Country` and `Count` properties (code file `EnumerableSample/Program.cs`):

```
var countries = from r in Formula1.GetChampions()
    group r by r.Country into g
    orderby g.Count() descending, g.Key
    where g.Count() >= 2
    select new {
        Country = g.Key,
        Count = g.Count()
    };

foreach (var item in countries)
{
    WriteLine($"{item.Country, -10} {item.Count}");
}
```

The result displays the collection of objects with the `Country` and `Count` properties:

UK          10
Brazil      3
Finland     3
Australia   2
Austria     2
Germany     2
Italy       2