```
Select(r => r);
```

# Filtering with Index

One scenario in which you can’t use the LINQ query is an overload of the Where method. With an overload of the Where method, you can pass a second parameter that is the index. The index is a counter for every result returned from the filter. You can use the index within the expression to do some calculation based on the index. In the following example, the index is used within the code that is called by the Where extension method to return only racers whose last name starts with A if the index is even (code file EnumerableSample/Program.cs):

```
var racers = Formula1.GetChampions().
    Where((r, index) => r.LastName.StartsWith("A") && index % 2 != 0);
foreach (var r in racers)
{
    WriteLine($"{r:A}");
}
```

The racers with last names beginning with the letter A are Alberto Ascari, Mario Andretti, and Fernando Alonso. Because Mario Andretti is positioned within an index that is odd, he is not in the result:

```
Alberto Ascari, Italy; starts: 32, wins: 10
Fernando Alonso, Spain; starts: 252, wins: 32
```

# Type Filtering

For filtering based on a type you can use the OfType extension method. Here the array data contains both string and int objects. Using the extension method OfType, passing the string class to the generic parameter returns only the strings from the collection (code file EnumerableSample/Program.cs):

```
object[] data = {"one", 2, 3,"four","five", 6 };
var query = data.OfType<string>();
foreach (var s in query)
{
    WriteLine(s);
}
```

Running this code, the strings one, four, and five are displayed:

```
one
four
five
```

# Compound from

If you need to do a filter based on a member of the object that itself is a sequence, you can use a compound from. The Racer class defines a property Cars, where Cars is a string array. For a filter of all racers who were champions with a Ferrari, you can use the LINQ query shown next. The first from clause accesses the Racer objects returned from Formula1.GetChampions. The second from clause accesses the Cars