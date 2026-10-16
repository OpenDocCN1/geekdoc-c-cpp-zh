
Racers are selected based on their country by using the lambda expression `r => r.Country`. The `foreach` loop accesses only the racers from Australia by using the indexer (code file `LookupSample/Program.cs`):

```csharp
var racers = new List<Racer>();
racers.Add(new Racer("Jacques","Villeneuve","Canada", 11));
racers.Add(new Racer("Alan","Jones","Australia", 12));
racers.Add(new Racer("Jackie","Stewart","United Kingdom", 27));
racers.Add(new Racer("James","Hunt","United Kingdom", 10));
racers.Add(new Racer("Jack","Brabham","Australia", 14));

var lookupRacers = racers.ToLookup(r => r.Country);

foreach (Racer r in lookupRacers["Australia"])
{
    WriteLine(r);
}
```

> NOTE You can read more about extension methods in Chapter 13, “Language Integrated Query.” Lambda expressions are explained in Chapter 9, “Delegates, Lambdas, and Events.”

The output shows the racers from Australia:

```
Alan Jones
Jack Brabham
```

## Sorted Dictionaries

SortedDictionary<TKey, TValue> is a binary search tree in which the items are sorted based on the key. The key type must implement the interface IComparable<TKey>. If the key type is not sortable, you can also create a comparer implementing IComparer<TKey> and assign the comparer as a constructor argument of the sorted dictionary.

Earlier in this chapter you read about SortedList<TKey, TValue>. SortedDictionary<TKey, TValue> and SortedList<TKey, TValue> have similar functionality, but because SortedList<TKey, TValue> is implemented as a list that is based on an array, and SortedDictionary<TKey, TValue> is implemented as a dictionary, the classes have different characteristics:

- SortedList<TKey, TValue> uses less memory than SortedDictionary<TKey, TValue>.
- SortedDictionary<TKey, TValue> has faster insertion and removal of elements.
- When populating the collection with already sorted data, SortedList<TKey, TValue> is faster if capacity changes are not needed.

> NOTE SortedList consumes less memory than SortedDictionary. SortedDictionary is faster with inserts and the removal of unsorted data.

## Sets

A collection that contains only distinct items is known by the term set. The .NET Framework includes two sets, HashSet<T> and SortedSet<T>, that both implement the interface ISet<T>. HashSet<T> contains an unordered list of distinct items; with SortedSet<T> the list is ordered.

The ISet<T> interface offers methods to create a union of multiple sets, to create an intersection of sets, or to provide information if one set is a superset or subset of another.

In the following sample code, three new sets of type string are created and filled with Formula-1 cars. The HashSet<T> class implements the ICollection<T> interface. However, the Add method is implemented explicitly and a different Add method is offered by the class, as you can see here. The Add method differs by the return type; a Boolean value is returned to provide the information if the element was added. If the element was already in the set, it is not added, and false is returned (code file SetSample/Program.cs):

```csharp
var companyTeams = new HashSet<string>()
{"Ferrari","McLaren","Mercedes" };
var traditionalTeams = new HashSet<string>()
{"Ferrari","McLaren" };
var privateTeams = new HashSet<string>()
{"Red Bull","Lotus","Toro Rosso","Force India","Sauber" };

if (privateTeams.Add("Williams"))
{
    WriteLine("Williams added");
}
if (!companyTeams.Add("McLaren"))
{
    WriteLine("McLaren was already in this set");
}
```

The result of these two Add methods is written to the console:

```
Williams added
McLaren was already in this set
```

The methods IsSubsetOf and IsSupersetOf compare a set with a collection that implements the IEnumerable<T> interface and returns a Boolean result. Here, IsSubsetOf verifies whether every element in traditionalTeams is contained in companyTeams, which is the case; IsSupersetOf verifies whether traditionalTeams has any additional elements compared to companyTeams:

```csharp
if (traditionalTeams.IsSubsetOf(companyTeams))
{
    WriteLine("traditionalTeams is a subset of companyTeams");
}

if (companyTeams.IsSupersetOf(traditionalTeams))
{
    WriteLine("companyTeams is a superset of traditionalTeams");
}
```

The output of this verification is shown here:

```
traditionalTeams is a subset of companyTeams
companyTeams is a superset of traditionalTeams
```

Williams is a traditional team as well, which is why this team is added to the traditionalTeams collection:

```csharp
traditionalTeams.Add("Williams");
if (privateTeams.Overlaps(traditionalTeams))
{
    WriteLine("At least one team is the same with traditional and private teams.");
}
```

Because there’s an overlap, this is the result:

```
At least one team is the same with traditional and private teams.
```

The variable allTeams that references a new SortedSet<string> is filled with a union of companyTeams, privateTeams, and traditionalTeams by calling the UnionWith method:

```csharp
var allTeams = new SortedSet<string>(companyTeams);
allTeams.UnionWith(privateTeams);
allTeams.UnionWith(traditionalTeams);

WriteLine();
WriteLine("all teams");
foreach (var team in allTeams)
{
    WriteLine(team);
}
```

Here, all teams are returned but every team is listed just once because the set contains only unique values; and because the container is a SortedSet<string>, the result is ordered:

```
Ferrari
Force India
Lotus
McLaren
Mercedes
Red Bull
Sauber
Toro Rosso
Williams
```

The method ExceptWith removes all private teams from the allTeams set:

```csharp
allTeams.ExceptWith(privateTeams);
WriteLine();

WriteLine("no private team left");
foreach (var team in allTeams)
{
    WriteLine(team);
}
```

The remaining elements in the collection do not contain any private teams:

```
Ferrari
McLaren
Mercedes
```

## Performance

Many collection classes offer the same functionality as others; for example, SortedList offers nearly the same features as SortedDictionary. However, often there’s a big difference in performance. Whereas one collection consumes less memory, the other collection class is faster with retrieval of elements. The MSDN documentation often provides performance hints about methods of the collection, giving you information about the time the operation requires in big-O notation:

- O(1)
- O(log n)
- O(n)

O(1) means that the time this operation needs is constant no matter how many items are in the collection. For example, the ArrayList has an Add method with O(1) behavior. No matter how many elements are in the list, it always takes the same amount of time when adding a new element to the end of the list. The Count property provides the number of items, so it is easy to find the end of the list.

O(n) means it takes the worst-case time of N to perform an operation on the collection. The Add method of ArrayList can be an O(n) operation if a reallocation of the collection is required. Changing the capacity causes the list to be copied, and the time for the copy increases linearly with every element.

O(log n) means that the time needed for the operation increases with every element in the collection, but the increase of time for each element is not linear but logarithmic. SortedDictionary<TKey, TValue> has O(log n) behavior for inserting operations inside the collection; SortedList<TKey, TValue> has O(n) behavior for the same functionality. Here, SortedDictionary<TKey, TValue> is a lot faster because it is more efficient to insert elements into a tree structure than into a list.

The following table lists collection classes and their performance for different actions such as adding, inserting, and removing items. Using this table you can select the best collection class for the purpose of your application.

| Collection | Add | Insert | Remove | Item | Sort | Find |
|---|---|---|---|---|---|---|
| List<T> | O(1) or O(n) if the collection must be resized | O(n) | O(n) | O(1) | O(n log n), worst case O(n^2) | O(n) |
| Stack<T> | Push, O(1), or O(n) if the stack must be resized | n/a | Pop, O(1) | n/a | n/a | n/a |
| Queue<T> | Enqueue, O(1), or O(n) if the queue must be resized | n/a | Dequeue, O(1) | n/a | n/a | n/a |
| HashSet<T> | O(1) or O(n) if the set must be resized | Add O(1) or O(n) | O(1) | n/a | n/a | n/a |
| SortedSet<T> | O(log n) | Add O(log n) | O(log n) | n/a | n/a | n/a |
| LinkedList<T> | AddLast O(1) | AddAfter O(1) | O(1) | n/a | n/a | O(n) |
| Dictionary<TKey, TValue> | O(1) or O(n) | n/a | O(1) | O(1) | n/a | n/a |
| SortedDictionary<TKey, TValue> | O(log n) | n/a | O(log n) | O(log n) | n/a | n/a |
| SortedList<TKey, TValue> | O(n) for unsorted data, O(log n) for end of list, O(n) if resize is needed | n/a | O(n) | O(log n) to read/write, O(log n) if the key is in the list, O(n) if the key is not in the list | n/a | n/a |
