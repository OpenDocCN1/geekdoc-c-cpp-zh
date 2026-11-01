DirectoryInfo and FileInfo implement roughly the same public methods as Directory and File, as well as some public properties and constructors, but they are stateful and the members of these classes are not static. You need to instantiate these classes before each instance is associated with a particular folder or file. This means that these classes are more efficient if you are performing multiple operations using the same object. That's because they read in the authentication and other information for the appropriate file system object on construction, and then do not need to read that information again, no matter how many methods you call against each object (class instance). In comparison, the corresponding stateless classes need to check the details of the file or folder again with every method you call.

In this section, you are mostly using the FileInfo and DirectoryInfo classes, but it so happens that many (though not all) of the methods called are also implemented by File and Directory (although in those cases these methods require an extra parameter — the pathname of the file system object; also, a couple of the methods have slightly different names). For example:

```
FileInfo myFile = new FileInfo(@"C:\Program Files\My Program\ReadMe.txt");
myFile.CopyTo(@"D:\Copies\ReadMe.txt");
```

has the same effect as:

```
File.Copy(@"C:\Program Files\My Program\ReadMe.txt", @"D:\Copies\ReadMe.txt");
```

The first code snippet takes slightly longer to execute because of the need to instantiate a FileInfo object, myFile, but it leaves myFile ready for you to perform further actions on the same file. By using the second example, there is no need to instantiate an object to copy the file.

You can instantiate a FileInfo or DirectoryInfo class by passing to the constructor a string containing the path to the corresponding file system object. You have just seen the process for a file. For a folder, the code looks similar:

```
DirectoryInfo myFolder = new DirectoryInfo(@"C:\Program Files");
```

If the path represents an object that does not exist, an exception will not be thrown at construction, but will instead be thrown the first time that you call a method that actually requires the corresponding file system object to be there. You can find out whether the object exists and is of the appropriate type by checking the Exists property, which is implemented by both of these classes:

```
FileInfo test = new FileInfo(@"C:\Windows");
Console.WriteLine(test.Exists.ToString());
```

Note that for this property to return true, the corresponding file system object must be of the appropriate type. In other words, if you instantiate a FileInfo object supplying the path of a folder, or you instantiate a DirectoryInfo object, giving it the path of a file, Exists will have the value false. Most of the properties and methods of these objects will return a value if possible — they won't necessarily throw an exception just because the wrong type of object has been called, unless they are asked to do something that really is impossible. For example, the preceding code snippet might first display false (because C:\Windows is a folder). However, it still displays the time the folder was created because a folder still has that information. But if you tried to open the folder as if it were a file, using the FileInfo.Open() method, you'd get an exception.

After you have established whether the corresponding file system object exists, you can (if you are using the FileInfo or DirectoryInfo class) find out information about it using the properties in the following table.

| PROPERTY | DESCRIPTION |
|---|---|
| CreationTime | Time in which the file or folder was created |
| DirectoryName (FileInfo only) | Full pathname of the containing folder |
| Parent (DirectoryInfo only) | The parent directory of a specified subdirectory |
| Exists | Whether a file or folder exists |
| Extension | Extension of the file; it returns blank for folders |
| FullName | Full pathname of the file or folder |