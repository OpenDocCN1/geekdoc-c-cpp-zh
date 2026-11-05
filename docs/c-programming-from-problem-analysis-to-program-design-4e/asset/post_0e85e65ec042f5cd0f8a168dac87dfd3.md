

```csharp
else
{
    Console.WriteLine("{0} not found – using current " +
                       "directory", fileName);
}
Console.ReadKey( );
}
}
}
```

The output produced from the DirectoryStructure application is shown in Figure 13-3.

![](img/36e48639a06772bcb0fa1ea2525b33a3_882_0.png)

**FIGURE 13-3**  Output from the DirectoryStructure application

Archive is shown as the value for the Attributes of the file. Depending on the operating system version you are running, you might see Normal instead of Archive. Normal attributes indicate the file is a standard file that has no special attributes, such as ReadOnly. Archive indicates the file is a candidate for backup or removal. The method GetAttributes() returns a FileAttributes enumeration. An enumeration is a special form of value type that supplies alternate names for the values of an underlying primitive type. An enumeration type has a name, an underlying type, and a set of fields.

One example of a programmer-defined enumeration might be a type called DayOfWeek. The possible fields could be Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, and Saturday. Sunday could be associated with the integer 0, Monday with 1 and each consecutive day 2, 3, 4, 5, and 6. The enumeration could be defined as follows:

```csharp
public enum DayOfWeek
{
    Sunday,
    Monday,
    Tuesday,
    Wednesday,
    Thursday,
    Friday,
    Saturday
}
```

The enumeration is defined outside of the class, uses the `enum` keyword, and normally offers `public` access. After the enumeration is defined, you may use the values as fields for the data type. For example, to print the string "Tuesday", you could write:

```csharp
Console.WriteLine("Today is {0}!", DayOfWeek.Tuesday);
```

The output produced would be as follows:

```
Today is Tuesday!
```

You can also use explicit type casting to access the associated integer assigned to the value. For example, to display the number associated with Wednesday, you could write:

```csharp
Console.WriteLine("{0} = {1}", DayOfWeek.Wednesday,
                 (int)DayOfWeek.Wednesday );
```

The output produced would be as follows:

```
Wednesday = 3
```

Now look back at Example 13-1. The method `GetAttributes(fileName)` returns the `FileAttributes` for the file. `FileAttributes` is an enumeration. As shown in Figure 13-3, the field it returned was `Archive`. Other enumerated `FileAttributes` values include `Compressed`, `Device`, `Directory`, `Encrypted`, `Hidden`, `Normal`, `ReadOnly`, and `System`. Using enumerations such as this one makes coding simpler and the output more readable.

## Directory Class

Like the members of the File class, all members in the Directory class are `public static` methods. The Directory class provides static methods for creating and moving through directories and subdirectories. Table 13-3 lists some of the more interesting methods of the Directory class.

**TABLE 13-3**  Directory class members

| Public static member | Description |
|---|---|
| `CreateDirectory()` | Creates all the directories in a specified path |
| `Delete()` | Deletes a specified directory |
| `Exists()` | Determines whether the given path refers to an existing directory |
| `GetCreationTime()` | Gets the creation date and time of a directory |
| `GetCurrentDirectory()` | Gets the current working directory of the application |
| `GetDirectories()` | Gets the names of subdirectories in a specified directory |
| `GetFiles()` | Returns the names of files in a specified directory |
| `GetParent()` | Retrieves the parent directory of the specified path, including both absolute and relative paths |
| `GetLastWriteTime()` | Returns the date and time the specified file or directory was last written to |
| `Move()` | Moves a file or a directory and its contents to a new location |
| `SetCurrentDirectory()` | Sets the application's current working directory to the specified directory |

.NET also includes DirectoryInfo and FileInfo classes. These classes are very similar to their name counterparts, Directory and File. They differ in that the DirectoryInfo and FileInfo classes both have instance methods instead of static members. They are direct descendants of the FileSystemInfo class.

Objects can be instantiated from the DirectoryInfo and FileInfo classes. No objects can be instantiated from the File and Directory classes.

## FileInfo and DirectoryInfo Classes

The FileInfo and DirectoryInfo classes add functionality beyond method members of the File and Directory classes. They both have a number of public properties and, of course, both offer a public constructor. Neither class can be inherited. If you plan to make reference to and use a file or directory several times, you will want to consider instantiating objects of one or both of these classes and use its instance methods. Table 13-4 shows some of the key properties of the FileInfo class.

**TABLE 13-4**  FileInfo properties

| Public member | Description |
|---|---|
| `Attributes` | Gets or sets the FileAttributes of the current FileSystemInfo |
| `Directory` | Gets an instance of the parent directory |
| `DirectoryName` | Gets a string representing the directory's full path |
| `Exists` | Gets a value indicating whether a file exists |
| `Extension` | Gets the string representing the extension part of the file |
| `FullName` | Gets the full path of the directory or file |
| `LastAccessTime` | Gets or sets the time the current file or directory was last accessed |
| `LastWriteTime` | Gets or sets the time when the current file or directory was last written to |
| `Length` | Gets the size of the current file |
| `Name` | Gets the name of the file |

The public methods for the FileInfo or DirectoryInfo classes are not shown in the tables. Note, however, that most of the public static methods of the File and Directory classes are available as instance methods in the FileInfo and DirectoryInfo classes.

The DirectoryInfo class adds two other key properties: Parent and Root. Parent gets the parent directory of a specified subdirectory. Root gets the root portion of a path. You should be very careful when you are working with paths in conjunction with files and/or directories. The path must be accurate or an exception is raised.

Example 13-2 adds additional functionality to the DirectoryStructure example illustrated in Example 13-1. An object of the DirectoryInfo is instantiated, and the foreach loop structure uses the FileInfo class.

### EXAMPLE 13.2

```csharp
DirectoryInfo dir = new DirectoryInfo(".");
Console.WriteLine("Current Directory: \n{0}\n",
                  Directory.GetCurrentDirectory());
Console.WriteLine("File Name".PadRight(52) +
                  "Size".PadRight(10) + "Creation Time");
foreach (FileInfo fil in dir.GetFiles("*.*"))
{
    string name = fil.Name;
    long size = fil.Length;
    DateTime creationTime = fil.CreationTime;
    Console.WriteLine("{0} {1,12:N0} {2,20:g}", name.PadRight(45),
                      size, creationTime);
}
```

After an object of the DirectoryInfo is instantiated in Example 13-2, the GetCurrentDirectory() method is invoked to display the current directory. The GetFiles() method of the DirectoryInfo class is invoked to retrieve a collection of files in the current directory. The Name, Size or Length, and CreationTime properties of the FileInfo class are accessed for the display. The output for the revised example is shown in Figure 13-4.

![](img/36e48639a06772bcb0fa1ea2525b33a3_886_0.png)

**FIGURE 13-4**  Output from the revised DirectoryStructure application

As you review the code, you will notice that the PadRight() method of the string class was used to format the name of the file returned by the FileInfo Name property.

> **NOTE**
>
> PadRight() in Example 13-2 left aligned the file names and added spaces to the right filling up 45 character positions. The size or Length and CreationTime values were right aligned using the format specifiers. The positive integers (12 and 20) in the format specifiers indicate that the values should be right aligned.

