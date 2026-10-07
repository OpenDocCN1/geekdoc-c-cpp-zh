```
{
// Added in C# 4.0/Microsoft .NET Framework 4.0
if (!file.Attributes.HasFlag(FileAttributes.Hidden))
{
    throw new Exception("File is not hidden.");
}

if ((file.Attributes & FileAttributes.ReadOnly) != FileAttributes.ReadOnly)
{
    throw new Exception("File is not read-only.");
}
// ...
}
```

# Output 9.4

| Hidden | ReadOnly = 3 |

Using the bitwise OR operator allows you to set the file attributes to both read-only and hidden.

Each value within the enum does not need to correspond to only one flag. It is perfectly reasonable to define additional flags that correspond to frequent combinations of values. Listing 9.37 shows an example.

# Listing 9.37: Defining Enum Values for Frequent Combinations

```
[Flags]
enum DistributedChannel
{
None = 0,
Transacted = 1,
Queued = 2,
Encrypted = 4,
Persisted = 16,
FaultTolerant =
Transacted | Queued | Persisted
}
```

It is a good practice to have a zero None member in a flags enum because the initial default value of a field of enum type or an element of an array of enum type is