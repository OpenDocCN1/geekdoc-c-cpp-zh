
## 17.9 Classes File and Directory

```csharp
54      // display the number of files with current extension
55      resultsTextBox.AppendText(
56          $"{found[current]} {current} files." + 
57          Environment.NewLine);
58  )
59  
60      found.Clear(); // clear results for new search
61      {
62      }

64      // search directory using LINQ
65      private void SearchDirectory(string folder)
66      {
67          // find files contained in the directory
68          string[] files = Directory.GetFiles(folder);

70          // subdirectories in the directory
71          string[] directories = Directory.GetDirectories(folder);

73          // find all extensions in this directory
74          var extensions = =
              75              from file in files
76              group file by Path.GetExtension(file);

78              foreach (var extension in extensions)
79              {
80                  if (found.ContainsKey(extension.Key))
81                      found[extension.Key] += extension.Count(); // update count
82                  else
83                  {
84                      found[extension.Key] = extension.Count(); // add count
85                  }
86              }
88  

90          // recursive call to search subdirectories
91              foreach (var subdirectory in directories)
92              {
93                  SearchDirectory(subdirectory);
94              }
95      } 

97      // allow user to delete backup files (.bak)
98      private void CleanDirectory(string folder)
99      {
100          // find files contained in the directory
101          string[] files = Directory.GetFiles(folder);

103          // subdirectories in the directory
104          string[] directories = Directory.GetDirectories(folder);
105      }
```

Fig. 17.14 | Using LINQ to search directories and determine file types (Part 2 of 3.)

## Chapter 17 Files and Streams

```csharp
// select all the backup files in the directory
var backupFiles =
    from file in files
    where Path.GetExtension(file) == ".bak"
    select file;
```

```csharp
// delete file if user clicked 'yes'
if (result == DialogResult.Yes)
{
    File.Delete(backup); // delete backup file
    found[".bak"]--; // decrement in Dictionary
```

```csharp
// if there are no .bak files, delete key in Dictionary
if (found(".bak") == 0)
{
    found.Remove(".bak");
}
```

```csharp
// recursive call to all subdirectories
foreach (var subdirectory in directories)
{
    CleanDirectory(subdirectory);
}
```

a GUI after entering a directory to search and pressing Directory

![](img/57baed2319be0bb1b5f98674846f2711_774_0.png)

Fig. 17.14 Using LINQ to search directories and determine file types. (Part 3 of 3.)

## 17.10 Wrap-Up

### Method SearchDirectory

Lines 36–38 get the current directory (if the user did not specify a path) or the specified directory. Line 46 passes the directory name to recursive method SearchDirectory (lines 65–95). Line 66 calls method GetFiles to get a string array containing filenames in the specified directory. Line 71 calls Directory method GetDirectories to get a string array containing the subdirectory names in the specified directory.

Lines 74–76 use LINQ to get the file extensions in the files array. Path method GetExtension provides the extension for the specified filename. We use LINQ group by to get the results by filename extension. For each filename-extension group returned by the LINQ query, lines 78–88 use LINQ method to count.

### Method CleanDirectory

Lines 36–38 get the current directory (if the user did not specify a path) or the specified directory. Line 46 passes the directory name to recursive method SearchDirectory (lines 65–95). Line 66 calls method GetFiles to get a string array containing filenames in the specified directory. Line 71 calls Directory method GetDirectories to get a string array containing the subdirectory names in the specified directory.

Lines 74–76 use LINQ to get the file extensions in the files array. Path method GetExtension provides the extension for the specified filename. We use LINQ group by to get the results by filename extension. For each filename-extension group returned by the LINQ query, lines 78–88 use LINQ method to count.

## 17.10 Wrap-Up

In this chapter, you used sequential access to manipulate persistent data. We showed how to use serialization to store objects in files and retrieve objects from files. Finally, you used class File and DirectoryInfo to manage directories. In Chapter 18, we begin our discussion of algorithms and data structures. Chapter 18 presents various searching algorithms for locating items in arrays and sorting algorithms for arranging elements into order.

## Summary

### 17.1 Introduction

- Files are used for long-term retention of large amounts of data.
- Data stored in files often called persistent data.
- Computers store files on secondary storage devices.

### 17.2 Files and Streams

- C views each file as a sequential stream of bytes that has a stream associated with it.
- Files are opened by creating an object that is large enough to hold the data.
- Streams provide communication channels between files and programs.
- File processing in C requires the System.IO namespace.
- Class Stream enables functionality for representing streams as bytes. This class is abstract, objects of this class cannot be instantiated.
- FileStream, MemoryStream and BufferedStream inherit from Stream.
- FileStream can be used to read and write data from sequential-access files.
- MemoryStream enables transfer of data directly from file to memory—this is much faster than other types of data transfer (e.g., to and from disk).
- BufferedStream uses buffers to transfer data to or from a stream. Buffering increases I/O performance by directing each output to a buffer large to hold many outputs. The actual transfer to the output device is performed in one file operation each time the buffer fills.

### 17.3 Creating a Sequential-Access Text File

- It imposes no structure on files. You must structure files to meet your app's requirements.
- A SaveFileDialog is a modal dialog—the user must interact with the dialog to dismiss it.
- A StreamWriter's constructor receives a FileStream that specifies the file in which to write text.
