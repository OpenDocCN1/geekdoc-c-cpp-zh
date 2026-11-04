
> Remember to import the `System.IO` namespace when using the various classes in the `System.IO` namespace.

# Working with Directories

The .NET Framework class library provides two classes for manipulating directories:

- `DirectoryInfo` class
- `Directory` class

The `DirectoryInfo` class exposes instance methods for dealing with directories while the `Directory` class exposes static methods.

## DirectoryInfo Class

The `DirectoryInfo` class provides various instance methods and properties for creating, deleting, and manipulating directories. The following table describes some of the common methods you can use to programmatically manipulate directories.

| Method | Description |
|---|---|
| `Create` | Creates a directory. |
| `CreateSubdirectory` | Creates a subdirectory. |
| `Delete` | Deletes a directory. |
| `GetDirectories` | Gets the subdirectories of the current directory. |
| `GetFiles` | Gets the file list from a directory. |

And here are some of the common properties:

| Properties | Description |
|---|---|
| `Exists` | Indicates if a directory exists. |
| `Parent` | Gets the parent of the current directory. |
| `FullName` | Gets the full path name of the directory. |
| `CreationTime` | Gets or sets the creation time of current directory. |

> *Refer to the MSDN documentation for a full list of methods and properties.*

To see how to use the DirectoryInfo class, consider the following example:

```csharp
static void Main(string[] args)
{
    string path = @"C:\My Folder";
    DirectoryInfo di = new DirectoryInfo(path);

    try
    {
        //---if directory does not exists---
        if (!di.Exists)
        {
            //---create the directory---
            di.Create();  //---c:\My Folder---

            //---creates subdirectories---
            di.CreateSubdirectory("Subdir1");  //---c:\My Folder\Subdir1---
            di.CreateSubdirectory("Subdir2");  //---c:\My Folder\Subdir2---
        }

        //---print out some info about the directory---
        Console.WriteLine(di.FullName);
        Console.WriteLine(di.CreationTime);

        //---get and print all the subdirectories---
        DirectoryInfo[] subDirs = di.GetDirectories();
        foreach (DirectoryInfo subDir in subDirs)
            Console.WriteLine(subDir.FullName);

        //---get the parent of C:\My folder---
        DirectoryInfo parent = di.Parent;
        if (parent.Exists)
        {
            //---prints out C:\---
            Console.WriteLine(parent.FullName);
        }

        //---creates C:\My Folder\Subdir3---
        DirectoryInfo newlyCreatedFolder =
            di.CreateSubdirectory("Subdir3");

        //---deletes C:\My Folder\Subdir3---
        newlyCreatedFolder.Delete();
    }
    catch (IOException ex)
    {
        Console.WriteLine(ex.Message);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }

    Console.ReadLine();
}
```

In this example, you first create an instance of the DirectoryInfo class by instantiating it with a path (`C:\My Folder`). You check if the path exists by using the `Exists` property. If it does not exist, you create the folder (`C:\My Folder`) and then create two subdirectories underneath it (`Subdir1` and `Subdir2`).

Next, you print out the full pathname (using the `FullName` property) of the folder and its creation date (using the `CreationTime` property). You then get all the subdirectories under `C:\My Folder` and display their full pathnames. You can get the parent of the `C:\My Folder` using the `Parent` property.

Finally, you create a subdirectory named `Subdir3` under `C:\My Folder` and pass a reference to the newly created subdirectory to the `newlyCreatedFolder` object. You then delete the folder, using the `Delete()` method.

## Directory Class

The `Directory` class is similar to the `DirectoryInfo` class. The key difference between them is that `Directory` exposes static members instead of instance members. The `Directory` class also exposes only methods — no properties. Some of the commonly used methods are described in the following table.

| Method | Description |
| --- | --- |
| `CreateDirectory` | Creates a subdirectory. |
| `Delete` | Deletes a specified directory. |
| `Exists` | Indicates if a specified path exists. |
| `GetCurrentDirectory` | Gets the current working directory. |
| `GetDirectories` | Gets the subdirectories of the specified path. |
| `GetFiles` | Gets the file list from a specified directory. |
| `SetCurrentDirectory` | Sets the current working directory. |

> Refer to the MSDN documentation for a full list of methods and properties.

Here's the previous program using the `DirectoryInfo` class rewritten to use the `Directory` class:

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

            //---creates subdirectories---
            //---c:\My Folder\Subdir1---
            Directory.CreateDirectory("Subdir1");
            //---c:\My Folder\Subdir2---
            Directory.CreateDirectory("Subdir2");
        }

        //---set the current directory to C:\My Folder---
        Directory.SetCurrentDirectory(path);

        //---print out some info about the directory---
        Console.WriteLine(Directory.GetCurrentDirectory());
        Console.WriteLine(Directory.GetCreationTime(path));

        //---get and print all the subdirectories---
        string[] subDirs = Directory.GetDirectories(path);
        foreach (string subDir in subDirs)
            Console.WriteLine(subDir);

        //---get the parent of C:\My Folder---
        DirectoryInfo parent = Directory.GetParent(path);
        if (parent.Exists)
        {
            //---prints out C:\---
            Console.WriteLine(parent.FullName);
        }

        //---creates C:\My Folder\Subdir3---
        Directory.CreateDirectory("Subdir3");

        //---deletes C:\My Folder\Subdir3---
        Directory.Delete("Subdir3");
    }
    catch (IOException ex)
    {
        Console.WriteLine(ex.Message);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
    Console.ReadLine();
}
```

As you can see, most of the methods in the `Directory` class require you to specify the directory you are working with. If you like to specify the directory path by using relative path names, you need to set the current working directory using the `SetCurrentDirectory()` method; if not, the default current directory is always the location of your program. Also, notice that some methods (such as `GetParent()`) still return `DirectoryInfo` objects.

> In general, if you are performing a lot of operations with directories, use the `DirectoryInfo` class. Once it is instantiated, the object has detailed information about the directory you are currently working on. In contrast, the `Directory` class is much simpler and is suitable if you are occasionally dealing with directories.

# Working with Files Using the File and FileInfo Classes

The .NET Framework class library contains two similar classes for dealing with files — `FileInfo` and `File`.

The `File` class provides static methods for creating, deleting, and manipulating files, whereas the `FileInfo` class exposes instance members for file manipulation.

Like the `Directory` class, the `File` class only exposes static methods and does not contain any properties.

Consider the following program, which creates, deletes, copies, renames, and sets attributes in files, using the `File` class.

```csharp
static void Main(string[] args)
{
    string filePath = @"C:\temp\textfile.txt";
    string fileCopyPath = @"C:\temp\textfile_copy.txt";
    string newFileName = @"C:\temp\textfile_newcopy.txt";

    try
    {
        //---if file already existed---
        if (File.Exists(filePath))
        {
            //---delete the file---
            File.Delete(filePath);
        }

        //---create the file again---
        FileStream fs = File.Create(filePath);
        fs.Close();

        //---make a copy of the file---
        File.Copy(filePath, fileCopyPath);

        //---rename the file---
        File.Move(fileCopyPath, newFileName);

        //---display the creation time---
        Console.WriteLine(File.GetCreationTime(newFileName));

        //---make the file read-only and hidden---
        File.SetAttributes(newFileName, FileAttributes.ReadOnly);
        File.SetAttributes(newFileName, FileAttributes.Hidden);
    }
    catch (IOException ex)
    {
        Console.WriteLine(ex.Message);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
    Console.ReadLine();
}
```
