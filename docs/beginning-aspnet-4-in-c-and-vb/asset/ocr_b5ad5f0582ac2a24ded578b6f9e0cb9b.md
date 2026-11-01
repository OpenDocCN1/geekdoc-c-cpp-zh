requires a string parameter and returns IEnumerable<Racer>, similar to the method that was implemented before. For doing this, several generic Func<> delegates are defined, so you do not need to declare your own delegate. A Lambda expression is assigned to the variable racersByCar. The left side of the Lambda expression defines a car variable of the type that is the first generic parameter of the Func delegate (a string). The right side defines the LINQ query that uses the parameter with the where clause:

```
Func<string, IEnumerable<Racer>> racersByCar =
    car => from r in Formula1.GetChampions()
           from c in r.Cars
           where c == car
           orderby r.LastName
           select r;
```

Now you can use the Intersect() extension method to get all racers that won the championship with a Ferrari and a McLaren:

```
Console.WriteLine("World champion with Ferrari and McLaren");
foreach (var racer in racersByCar("Ferrari").Intersect(
    racersByCar("McLaren")))
{
    Console.WriteLine(racer);
}
```

The result is just one racer, Niki Lauda:

```
World champion with Ferrari and McLaren
Niki Lauda
```

> The Set operations compares the objects by invoking the GetHashCode() and Equals() method of the entity class. For custom comparison, you can also pass an object that implements the interface IEqualityComparer<>. In the sample here, the GetChampions() method always returns the same objects and thus the default comparison works.

# Zip

The Zip() method is new with .NET 4 and enables you to merge two related sequences into one with a predicate function.

First, two related sequences are created, both with the same filtering (country Italy) and ordering. For merging this is important, as item 1 from the first collection is merged with item 1 from the second collection, item 2 with item 2, and so on. In case the count of the two sequences is different, Zip() just stops when the end of the smaller collection is reached.

The items in the first collection have a Name property and the items in the second collection have LastName and Starts properties.

Using the Zip() method on the collection racerNames requires the second collection racerNamesAndStarts as the first parameter. The second parameter is of type Func<TFirst, TSecond, TResult>. This parameter is implemented as a Lambda expression and receives the elements of the first collection with the parameter first, and the elements of the second collection with the parameter second. The implementation creates and returns a string containing the Name property of the first element and the Starts property of the second element:

```
var racerNames = from r in Formula1.GetChampions()
                 where r.Country == "Italy"
                 orderby r.Wins descending
                 select new
```