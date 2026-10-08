
## The Directory and File Classes

If you don't want to create an instance of a DirectoryInfo or FileInfo class, you can use the Directory or File class instead. These classes provide only static methods for performing the same directory and file operations provided by the DirectoryInfo and FileInfo classes.

The commonly used methods of the Directory class are shown in Table 13.5.

### TABLE 13.5 Commonly Used Methods of the Directory Class

| Method | Description |
| :--- | :--- |
| CreateDirectory | Creates all the directories in the specified path |
| Delete | Deletes the specified directory |
| EnumerateDirectories | Gets an enumerable collection of directory names in the specified path |
| EnumerateFiles | Gets an enumerable collection of filenames in the specified path |
| EnumerateFileSystemEntries | Gets an enumerable collection of the names of all files and subdirectories in the specified path |
| Exists | Indicates if the specified path exists on disk |
| GetCurrentDirectory | Gets the current working directory |
| GetDirectoryRoot | Gets the volume information, root information, or both, for the specified path |
| GetLogicalDrives | Gets the names of the logical drives on the current computer |
| GetParent | Gets the parent directory of the specified path |
| Move | Moves a file or a directory, including all files and subdirectories, to a new location |

Listing 13.3 shows the same operations from Listing 13.1, but using the Directory class instead of the DirectoryInfo class.

## LISTING 13.3 Using the Directory Class

```csharp
public class DirectoryInfoExample
{
    public static void Main()
    {
        string tempPath = Path.GetTempFileName();

        try
        {
            if (Directory.Exists(tempPath))
            {
                Console.WriteLine("The directory already exists.");
            }
            else
            {
                Directory.CreateDirectory(tempPath);
                Console.WriteLine("The directory was successfully created.");
                Directory.Delete(tempPath);
                Console.WriteLine("The directory was deleted.");
            }
        }
        catch (IOException e)
        {
            Console.WriteLine("An error occurred: {0}", e.Message);
        }
    }
}
```

One significant difference between the Directory and DirectoryInfo classes is the EnumerateFiles, EnumerateDirectories, and EnumerateFileSystemEntries methods. In the Directory class, these methods return an IEnumerable<string> of just directory and filenames, whereas in the DirectoryInfo class, they return an IEnumerable<FileInfo>, IEnumerable<DirectoryInfo>, and IEnumerable<FileSystemInfo>, respectively.

The commonly used methods of the File class are shown in Table 13.6, and Listing 13.4 shows the same operations used in Listing 13.2, but using the File class instead of the FileInfo class.

### TABLE 13.6 Commonly Used Methods of the File Class

| Method | Description |
| :--- | :--- |
| AppendAllLines | Appends lines to a file and then closes the file |
| AppendAllText | Appends the specified strings to a file, creating the file if it doesn't already exist |
| AppendText | Creates a StreamWriter for appending text to the current file |
| Copy | Copies an existing file to a new file |
| Create | Creates a file |
| CreateText | Creates or opens a file for writing text |
| Delete | Deletes the specified file |
| GetAttributes | Gets the attributes of the specified file |
| Move | Moves the specified file to a new location |
| OpenRead | Opens an existing file for reading |
| OpenText | Opens an existing text file for reading |
| OpenWrite | Opens an existing file for writing |
| ReadAllBytes | Opens a binary file, reads the contents into a byte array, and then closes the file |
| ReadAllLines | Opens a text file, reads all the lines into a string array, and then closes the file |
| ReadAllText | Opens a text file, reads all the lines into a string, and then closes the file |
| ReadLines | Reads the lines of a file |
| Replace | Replaces the contents of the specified file with the contents of another file |
| SetAttributes | Sets the attributes of the specified file |
| WriteAllBytes | Writes the specified bytes to a new file and then closes the file |
| WriteAllLines | Writes one or more strings to a new text file and then closes the file |
| WriteAllText | Writes a string to a new file and then closes the file |

## LISTING 13.4 Using the File Class

```csharp
public class FileExample
{
    public static void Main()
    {
        string tmpFile = Path.GetTempFileName();
        try
        {
            if (!File.Exists(tmpFile))
            {
                using (StreamWriter writer = File.CreateText(tmpFile))
                {
                    writer.WriteLine("Line 1");
                    writer.WriteLine("Line 2");
                }
            }

            File.Copy(tmpFile, Path.GetTempFileName());
            File.Delete(tmpFile);
        }
        catch (IOException e)
        {
            Console.WriteLine("An error occurred: {0}", e.Message);
        }
    }
}
```

## Working with the Directory and File Classes

By following these steps, you learn how to work with the Directory and File classes. If you closed Visual Studio, repeat the previous exercise first. Be sure to keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Modify the call to `EnumerateDirectories` to call the method on Directory of the same name, enumerating over the C:\Windows\Web\Wallpaper directory. Use the following code to retrieve this folder path:

```csharp
Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Windows),
    "Web",
    "WallPaper")
```

- 2. Modify the nested foreach statement to call `Directory.EnumerateFiles`. Because this returns a path string rather than a FileInfo, you also need to modify the statement that prints the filename and creation time to get the file-name from the resulting path string and use the appropriate static method on the File class to retrieve the creation date and time.

- 3. Run the application using Ctrl+F5. The output should match the output generated from step 6 of the previous exercise.

## Reading and Writing Data

Working with the data contained in files (by either reading or writing) uses streams, represented by the Stream class. All stream-based classes provided by the .NET Framework derive from this class. The commonly used members of the Stream class are shown in Table 13.7.

### TABLE 13.7 Commonly Used Members of the Stream Class

| Member | Description |
| :--- | :--- |
| CanRead | Indicates if the current stream supports reading |
| CanWrite | Indicates if the current stream supports writing |
| Close | Closes the current stream |
| CopyTo | Copies the contents of the current stream into another stream |
| Flush | Clears all buffers and writes any buffered data to the backing store |
| Read | Reads a sequence of bytes from the current stream |
| Write | Writes a sequence of bytes to the current stream |

## Binary Files

When you aren’t certain about the content of a file, it is usually best to treat it as a binary file, which is simply a stream of bytes. To read data from a binary file, you use the static OpenRead method of the File class, which returns a FileStream:

```csharp
FileStream input = File.OpenRead(Path.GetTempFileName());
```

You can then use the Read method on the resulting FileStream to read data into a buffer that you provide. A buffer is simply an array of bytes that holds the data returned by the Read method. You pass the buffer, the number of bytes to read, and an offset into the buffer at which data then will be stored. The Read method reads the number of bytes specified from the backing store into the buffer and returns the total number of bytes actually read:

```csharp
byte[] buffer = new byte[1024];
int bytesRead = input.Read(buffer, 0, 1024);
```

Of course, reading from a stream isn’t the only operation you can perform. Writing binary data to a stream is also a common activity and is accomplished in a similar manner. You first open a binary file for writing using the OpenWrite method of the File class and then use the Write method on the resulting FileStream to write a buffer of data to the backing store. The Write method is passed the buffer containing the data to write, the offset into the buffer at which to start reading, and the number of bytes to write:

```csharp
FileStream output = File.OpenWrite(Path.GetTempFileName());
output.Write(buffer, 0, bytesRead);
```
