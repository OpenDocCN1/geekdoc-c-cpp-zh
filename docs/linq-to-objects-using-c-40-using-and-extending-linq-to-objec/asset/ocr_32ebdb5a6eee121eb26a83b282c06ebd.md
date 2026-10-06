# Table 6-2 Comparison of the LINQ Set Operators and the HashTable Type Methods

| HashSet<T> operator | LINQ equivalent operator | Description |
|---|---|---|
| IsSubsetOf | Not provided. To approximate the same result using LINQ, return the Boolean of true if the intersect count with the second collection equals the count of the distinct elements in the collection in the following fashion:
```csharp
var aCount =
 a.Distinct().Count();
var intersectCount =
  a.Intersect(b)
  .Distinct()
  .Count();
return intersectCount == aCount;
``` | Returns the Boolean value of true if all of the elements in the given collection are present in the second collection. Will return the Boolean value of true if the collections share the same elements. |
| IsProperSubsetOf | Not provided. To approximate the same result using LINQ, return the Boolean of true if the intersect count with the second collection is less than the count of the distinct elements in the second collection, and the intersect count equals the count of the distinct elements in the collection in the following fashion:
```csharp
var aCount =
 a.Distinct().Count();
var bCount =
 b.Distinct().Count();
var intersectCount =
  a.Intersect(b)
  .Distinct()
  .Count();
return (intersectCount < bCount) && (intersectCount == aCount);
``` | Returns the Boolean value of true if all of the elements in the given collection are present in the second collection. Will return the Boolean value of false if the same elements exactly; the collection must be an actual subset with at least one element less than that in the second collection.