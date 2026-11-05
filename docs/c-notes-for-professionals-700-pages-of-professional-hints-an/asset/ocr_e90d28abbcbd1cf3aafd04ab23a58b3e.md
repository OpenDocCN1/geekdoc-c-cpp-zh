# Section 66.46: Count and LongCount

Count returns the number of elements in an IEnumerable<T>. Count also exposes an optional predicate parameter that allows you to filter the elements you want to count.

```
int[] array = { 1, 2, 3, 4, 2, 5, 3, 1, 2 };

int n = array.Count(); // returns the number of elements in the array
int x = array.Count(i => i > 2); // returns the number of elements in the array greater than 2
```

LongCount works the same way as Count but has a return type of long and is used for counting IEnumerable<T> sequences that are longer than int.MaxValue

```
int[] array = GetLargeArray();

long n = array.LongCount(); // returns the number of elements in the array
long x = array.LongCount(i => i > 100); // returns the number of elements in the array greater than 100
```

# Section 66.47: Incrementally building a query

Because LINQ uses deferred execution, we can have a query object that doesn't actually contain the values, but will return the values when evaluated. We can thus dynamically build the query based on our control flow, and evaluate it once we are finished:

```
IEnumerable<VehicleModel> BuildQuery(int vehicleType, SearchModel search, int start = 1, int count = -1) {
    IEnumerable<VehicleModel> query = _entities.Vehicles
        .Where(x => x.Active && x.Type == vehicleType)
        .Select(x => new VehicleModel {
            Id = v.Id,
            Year = v.Year,
            Class = v.Class,
            Make = v.Make,
            Model = v.Model,
            Cylinders = v.Cylinders ?? 0
        });
}
```

We can conditionally apply filters:

```
if (!search.Years.Contains("all", StringComparer.OrdinalIgnoreCase))
    query = query.Where(v => search.Years.Contains(v.Year));

if (!search.Makes.Contains("all", StringComparer.OrdinalIgnoreCase)) {
    query = query.Where(v => search.Makes.Contains(v.Make));
}

if (!search.Models.Contains("all", StringComparer.OrdinalIgnoreCase)) {
    query = query.Where(v => search.Models.Contains(v.Model));
}

if (!search.Cylinders.Equals("all", StringComparer.OrdinalIgnoreCase)) {
    decimal minCylinders = 0;
    decimal maxCylinders = 0;
    switch (search.Cylinders) {
        case "2-4":
            maxCylinders = 4;
            break;
```