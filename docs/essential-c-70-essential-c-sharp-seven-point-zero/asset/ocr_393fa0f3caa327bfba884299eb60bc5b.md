resultant code is more succinct and readable. In contrast, when the type is not obvious, such as when a method return is assigned, developers should favor an explicit variable type declaration such as the following:

```
Dictionary<string, List<Account>> dictionary = GetAccounts();
```

# Selecting into Anonymous Types with LINQ

Lastly, capitalizing on anonymous types, we could create an IEnumerable<T> collection where T is an anonymous type (see Listing 15.27 and Output 15.14).

# LISTING 15.27: Projection to an Anonymous Type

```
/// ...
IEnumerable<string> fileList = Directory.EnumerateFiles(
rootDirectory, searchPattern);
var items = fileList.Select(
file =>
{
FileInfo fileInfo = new FileInfo(file);
return new
{
FileName = fileInfo.Name,
Size = fileInfo.Length
};
});
/// ...
```

# Output 15.14

```
{ FileName = AssemblyInfo.cs, Size = 1704 }
{ FileName = CodeAnalysisRules.xml, Size = 735 }
{ FileName = CustomDictionary.xml, Size = 199 }
{ FileName = EssentialCSharp.sln, Size = 40415 }
{ FileName = EssentialCSharp.suo, Size = 454656 }
{ FileName = EssentialCSharp.vsmdb, Size = 499 }
{ FileName = EssentialCSharp.vssscc, Size = 256 }
{ FileName = IntelliTechturo.Consolerester.dll, Size = 24576 }
{ FileName = IntelliTechturo.Consolerester.pdb, Size = 30208 }
```

The output of an anonymous type automatically shows the property names and their values as part of the generated ToString() method associated with the anonymous type.

Projection using the Select() method is very powerful. We already saw how to filter a collection vertically (reducing the number of items in the collection) using the Where() standard query operator. Now, via the Select()