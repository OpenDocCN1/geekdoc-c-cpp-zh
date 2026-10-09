Here fileList is of type IEnumerable<string>. However, using the projection offered by Select, we can transform each item in the collection to a System.IO.FileInfo object.
Lastly, capitalizing on tuples, we could create an IEnumerable<T> collection where T is a tuple (see Listing 15.13 and Output 15.3).

# LISTING 15.13: Projection to Tuple

```
```csharp
// ...
IEnumerable<string> fileList = Directory.EnumerateFiles(
    rootDirectory, searchPattern);

IEnumerable<(string FileName, long Size)> items = fileList.Select(
    file =>
    {
        FileInfo fileInfo = new FileInfo(file);
        return (
            FileName: fileInfo.Name,
            Size: fileInfo.Length
        );
    });
// ...
```
```

# OUTPUT 15.3

```
```
FileName = AssemblyInfo.cs, Size = 1704
FileName = CodeAnalysisRules.xml, Size = 735
FileName = CustomDictionary.xml, Size = 199
FileName = EssentialCSharp.sln, Size = 40415
FileName = EssentialCSharp.suo, Size = 454656
FileName = EssentialCSharp.vsmnd, Size = 499
FileName = EssentialCSharp.vssscc, Size = 256
FileName = IntelliTechture.ConsoleTester.dll, Size = 24576
FileName = IntelliTechture.ConsoleTester.pdb, Size = 30208
```
```

The output of an anonymous type automatically shows the property names and their values as part of the generated ToString() method associated with the anonymous type.
Projection using the Select() method is very powerful. We already saw how to filter a collection vertically (reducing the number of items in the collection) using the Where() standard query operator. Now, via the Select() standard query operator, we can also reduce the collection horizontally (making fewer columns) or transform the data entirely. In combination, Where() and Select() provide a means for extracting only those pieces of the original collection that are desirable for the current algorithm. These two methods alone provide a powerful collection manipulation API that would otherwise result in significantly more code that is less readable.