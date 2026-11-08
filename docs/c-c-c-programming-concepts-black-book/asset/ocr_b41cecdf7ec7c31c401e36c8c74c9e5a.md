```
```csharp
var setResult = (from s in set
                 select s).Distinct();
Console.WriteLine("The result of the Distinct operation is....");
foreach (int i in setResult)
{
    Console.WriteLine(i);
}
}
}
```
```

All the four set operations return an object of type `IEnumerable<int>`. However, in this program, the anonymous type is used, as it frees us from remembering the output type of each operation.

The output of the program is given as follows:

```
```
The result of union operation is....
1
2
3
4
5
6
7
8
The result of Except operation is....
1
2
4
The result of Intersection operation is....
3
5
The result of Distinct operation is....
1
2
3
5
9
```
```

# Conversion Operators

Conversion operators in LINQ convert a collection of one type into another. These operators can be categorized into two groups:

+   - One group converts the type of an entire collection without changing the underlying types of the collection elements. This group includes the operators, such as `ToList`, `ToArray`, and `ToDictionary`.
+   - Another group converts a collection into a sequence, which implements the `IEnumerable<T>` interface by changing the underlying types of the collection elements. This group includes the operators, such as `Cast` and `OfType`.

Let's learn about the first group of conversion operators.

When the `ToList` operator is applied to a collection, it returns the value of type `System.Collections.Generic.List<T>`. Similarly, the `ToArray` operator returns a new array when it is applied on a collection. The third operator, `ToDictionary`, can be implemented with the help of `ToDictionary()` extension method, which returns a dictionary that holds the value in key/value pair manner. When this extension method is applied to any collection, it immediately generates a new collection holding the data from the source collection. The `ToDictionary()` method accepts an argument which defines the key selector. Listing 19.33 shows the implementation of the first group of conversion operators.