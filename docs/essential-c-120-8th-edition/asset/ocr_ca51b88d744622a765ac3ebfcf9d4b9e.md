Where() standard operator. Now, via the Select() standard query operator, we can reduce the collection horizontally (making fewer columns) or transform the data entirely. In combination, Where() and Select() provide a means for extracting only those pieces of the original collection that are desirable for the current algorithm. These two methods alone provide a powerful collection manipulation API that would otherwise result in significantly more—and less readable—code.

# ADVANCED TOPIC

# Running LINQ Queries in Parallel

With the widespread availability of computers having multiple processors and multiple cores within those processors, the ability to easily take advantage of the additional processing power becomes more important. To do so, programs need to support threads so that what can happen simultaneously on different CPUs within the computer. Listing 15.14 demonstrates one way to do this using Parallel LINQ (PLINQ).

Listing 15.14: Executing LINQ Queries in Parallel

```
//...
IEnumerable<string> fileList = Directory.EnumerateFiles(rootDirectory, searchPattern);
var items = fileList.AsParallel().Select(
file => {
    FileInfo fileInfo = new(file);
    return new {
        FileName = fileInfo.Name,
        Size = fileInfo.Length
    };
});
//...
```

As Listing 15.14 shows, only a minimal change in code is needed to enable parallel support. All that this example uses a Microsoft .NET Framework 4-introduced standard query operator, AsParallel(), on the static class System