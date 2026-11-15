```
System.IO.FileInfo file =
    new System.IO.FileInfo(fileName);

file.Attributes = FileAttributes.Hidden |
    FileAttributes.ReadOnly;

Console.WriteLine("{0} | {1} = {2}",
    FileAttributes.Hidden, FileAttributes.ReadOnly,
    (int)FileAttributes.Hidden);

if (( file.Attributes & FileAttributes.Hidden ) !=
    FileAttributes.Hidden)
{
    throw new Exception("File is not hidden.");
}

if (( file.Attributes & FileAttributes.ReadOnly ) !=
    FileAttributes.ReadOnly)
{
    throw new Exception("File is not read-only.");
}

// ...
```

The results of Listing 8.16 appear in Output 8.5.

# Output 8.5:

```
Hidden | ReadOnly = 3
```

Using the bitwise OR operator allows you to set the file to both read-only and hidden. In addition, you can check for specific settings using the bitwise AND operator.

Each value within the enum does not need to correspond to only one flag. It is perfectly reasonable to define additional flags that correspond to frequent combinations of values. Listing 8.17 shows an example.

# LISTING 8.17: Defining Enum Values for Frequent Combinations

```
enum DistributedChannel
{
    None = 0,
    Transacted = 1,
    Queued = 2,
}
```