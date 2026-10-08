# **LISTING 13.3 Using the Directory Class**

```
```
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
                Directory.CreateDirectory(path);
                Console.WriteLine("The directory was successfully created.");
                Directory.Delete(path);
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
```

One significant difference between the Directory and DirectoryInfo classes is the EnumerateFiles, EnumerateDirectories, and EnumerateFileSystemEntries methods. In the Directory class, these methods return an IEnumerable<string> of just directory and filenames, whereas in the DirectoryInfo class, they return an IEnumerable<FileInfo>, IEnumerable<DirectoryInfo>, and IEnumerable<FileSystemInfo>, respectively.

The commonly used methods of the File class are shown in Table 13.6, and Listing 13.4 shows the same operations used in Listing 13.2, but using the File class instead of the FileInfo class.

# **TABLE 13.6 Commonly Used Methods of the File Class**

| Method | Description |
| --- | --- |
| AppendAllLines | Appends lines to a file and then closes the file |
| AppendAllText | Appends the specified strings to a file, creating the file if it doesn't already exist |
| AppendText | Creates a StreamWriter for appending text to the current file |
| Copy | Copies an existing file to a new file |