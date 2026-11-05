```
case "5-6":
    minCylinders = 5;
    maxCylinders = 6;
    break;
case "8":
    minCylinders = 8;
    maxCylinders = 8;
    break;
case "10+":
    minCylinders = 10;
    break;
}
if (minCylinders > 0) {
    query = query.Where(v => v.Cylinders >= minCylinders);
}
if (maxCylinders > 0) {
    query = query.Where(v => v.Cylinders <= maxCylinders);
}
}
```

We can add a sort order to the query based on a condition:

```
switch (search.SortingColumn.ToLower()) {
    case "make_model":
        query = query.OrderBy(v => v.Make).ThenBy(v => v.Model);
        break;
    case "year":
        query = query.OrderBy(v => v.Year);
        break;
    case "engine_size":
        query = query.OrderBy(v => v.EngineSize).ThenBy(v => v.Cylinders);
        break;
    default:
        query = query.OrderBy(v => v.Year); //The default sorting.
}
```

Our query can be defined to start from a given point:

```
query = query.Skip(start - 1);
```

and defined to return a specific number of records:

```
if (count > -1) {
    query = query.Take(count);
}
return query;
}
```

Once we have the query object, we can evaluate the results with a foreach loop, or one of the LINQ methods that returns a set of values, such as ToList or ToArray:

```
SearchModel sm;

// populate the search model here
// ...

List<VehicleModel> list = BuildQuery(5, sm).ToList();
```