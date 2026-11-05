This result has created anonymous objects on the fly, which is fine, but we have already created a proper class - so we can specify it: Instead of SELECT NEW { f.ID, s.RegionDescription }; we can say SELECT NEW Region(f.ID, s.RegionDescription);, which will return the same data but will create objects of type Region - that will maintain compatibility with the other objects.

Live demo on .NET fiddle

# Section 66.7: Skip and Take

The Skip method returns a collection excluding a number of items from the beginning of the source collection. The number of items excluded is the number given as an argument. If there are less items in the collection than specified in the argument then an empty collection is returned.

The Take method returns a collection containing a number of elements from the beginning of the source collection. The number of items included is the number given as an argument. If there are less items in the collection than specified in the argument then the collection returned will contain the same elements as the source collection.

```
var values = new [] { 5, 4, 3, 2, 1 };

var skipTwo = values.Skip(2); // { 3, 2, 1 }
var takeThree = values.Take(3); // { 5, 4, 3 }
var skipOneTakeTwo = values.Skip(1).Take(2); // { 4, 3 }
var takeZero = values.Take(0); // An IEnumerable<int> with 0 items
```

Live Demo on .NET Fiddle

Skip and Take are commonly used together to paginate results, for instance:

```
IEnumerable<T> GetPage<T>(IEnumerable<T> collection, int pageNumber, int resultsPerPage) {
    int startIndex = (pageNumber - 1) * resultsPerPage;
    return collection.Skip(startIndex).Take(resultsPerPage);
}
```

> Warning: LINQ to Entities only supports Skip on ordered queries. If you try to use Skip without ordering you will get a NotSupportedException with the message "The method 'Skip' is only supported for sorted input in LINQ to Entities. The method 'OrderBy' must be called before the method 'Skip'."

# Section 66.8: Defining a variable inside a Linq query (let keyword)

In order to define a variable inside a linq expression, you can use the let keyword. This is usually done in order to store the results of intermediate sub-queries, for example:

```
int[] numbers = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };

var aboveAverages = from number in numbers
    let average = numbers.Average()
    let nSquared = Math.Pow(number,2)
    where nSquared > average
    select number;
```

Console.WriteLine("The average of the numbers is {0}.", numbers.Average());

```
foreach (int n in aboveAverages)
```