# # Part I: C# Fundamentals

In this example, you first create an instance of the DirectoryInfo class by instantiating it with a path (C:\My Folder). You check if the path exists by using the Exists property. If it does not exist, you create the folder (C:\My Folder) and then create two subdirectories underneath it (Subdir1 and Subdir2).

Next, you print out the full pathname (using the FullName property) of the folder and its creation date (using the CreationTime property). You then get all the subdirectories under C:\My Folder and display their full pathnames. You can get the parent of the C:\My Folder using the Parent property.

Finally, you create a subdirectory named Subdir3 under C:\My Folder and pass a reference to the newly created subdirectory to the newlyCreatedFolder object. You then delete the folder, using the Delete() method.

# ## Directory Class

The Directory class is similar to DirectoryInfo class. The key difference between is that Directory exposes static members instead of instance members. The Directory class also exposes only methods — no properties. Some of the commonly used methods are described in the following table.

| Method | Description |
| --- | --- |
| CreateDirectory | Creates a subdirectory. |
| Delete | Deletes a specified directory. |
| Exists | Indicates if a specified path exists. |
| GetCurrentDirectory | Gets the current working directory. |
| GetDirectories | Gets the subdirectories of the specified path. |
| GetFiles | Gets the file list from a specified directory. |
| SetCurrentDirectory | Sets the current working directory. |

> > Refer to the MSDN documentation for a full list of methods and properties.

Here's the previous program using the DirectoryInfo class rewritten to use the Directory class:

```
```csharp
static void Main(string[] args)
{
    string path = @"C:\My Folder";
    try
    {
        //---if directory does not exists---
        if (!Directory.Exists(path))
        {
            //---create the directory---
            Directory.CreateDirectory(path);

            //---set the current directory to C:\My Folder---
            Directory.SetCurrentDirectory(path);
```
```