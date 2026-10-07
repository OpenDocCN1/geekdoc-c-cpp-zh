```
return lineCount;
}
private static int CountLines(string file)
{
    string? line;
    int lineCount = 0;
    // This can be improved with a using statement
    // which is not yet described.
    FileStream stream = new(file, FileMode.Open);
    StreamReader reader = new(stream);
    line = reader.ReadLine();

    while (line != null)
    {
        if (line.Trim() != "")
        {
            lineCount++;
        }
        line = reader.ReadLine();
    }

    reader.Dispose(); // Automatically closes the stream
    return lineCount;
}
```

Output 5.8 shows the results of Listing 5.22.

# OUTPUT 5.8

104

The program begins by passing the first command-line argument to DirectoryCountLines() or using the current directory if no argument is provided. This method first iterates through all the files in the current directory and totals the source code lines for each file. After processing each file in the directory, the code processes each subdirectory by passing the subdirectory back into the DirectoryCountLines() method, rerunning the method using the subdirectory. The same process is repeated recursively through each subdirectory until no more directories remain to process.