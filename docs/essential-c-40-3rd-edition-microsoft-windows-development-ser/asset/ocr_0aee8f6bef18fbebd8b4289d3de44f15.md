```
Directory.CreateDirectory(target);
}

for (int i = 0; i < searchPattern.length; i++)
{
    foreach (string file in
    Directory.GetFiles(
    sourceDirectory.FullName, searchPattern))
    {
    File.Copy(file,
    target + Path.GetFileName(file), true);
    }
}

//Copy SubDirectories (recursively)
if (option == SearchOption.AllDirectories)
{
    foreach (string element in
    Directory.GetDirectories(
    sourceDirectory.FullName))
    {
    Copy(element,
    target + Path.GetFileName(element),
    searchPattern);
    }
}
}
```

```
// ...
DirectoryInfo directory = new DirectoryInfo(".\\Source");
directory.MoveTo(".\\Root");
DirectoryInfoExtension.CopyTo(
directory, ".\\Target",
SearchOption.AllDirectories, "**");
// ...
```

The DirectoryInfoExtension.Copy() method takes a DirectoryInfo object and copies the underlying directory structure to a new location.

Because static methods are not referenced through a particular instance, the this keyword is invalid inside a static method. In addition, it is not possible to access either an instance field or an instance method directly from within a static method without a reference to the particular instance to which the field or method belongs. (Note that Main() is another example of a static method.)