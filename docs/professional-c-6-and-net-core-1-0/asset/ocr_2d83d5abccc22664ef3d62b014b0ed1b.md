the copied file is deleted by invoking FileInfo.Delete (code file WorkingWithFilesAndFolders/Program .cs):

```
private void DeleteDuplicateFiles(string directory, bool checkOnly)
{
    IEnumerable<string> fileNames =
    Directory.EnumerateFiles(directory,
        "*", SearchOption.AllDirectories);

    string previousFileName = string.Empty;

    foreach (string fileName in fileNames)
    {
        string previousName =
        Path.GetFileNameWithoutExtension(previousFileName);
        if (!string.IsNullOrEmpty(previousFileName) &&
            previousName.EndsWith("Copy") &&
            fileName.StartsWith(previousFileName.Substring(
                0, previousFileName.LastIndexOf(" - Copy"))))
        {
            var copiedFile = new FileInfo(previousFileName);
            var originalFile = new FileInfo(fileName);
            if (copiedFile.Length == originalFile.Length)
            {
                WriteLine($"delete {copiedFile.FullName}");
                if (!checkOnly)
                {
                    copiedFile.Delete();
                }
            }
        }
        previousFileName = fileName;
    }
}
```

# Working with Streams

Now let’s get into more powerful options that are available when you work with files: streams. The idea of a stream has been around for a very long time. A stream is an object used to transfer data. The data can be transferred in one of two directions:

+   - If the data is being transferred from some outside source into your program, it is called reading from the stream.
+   - If the data is being transferred from your program to some outside source, it is called writing to the stream.

Very often, the outside source will be a file, but that is not always the case. Other possibilities include the following:

+   - Reading or writing data on the network using some network protocol, where the intention is for this data to be picked up by or sent from another computer
+   - Reading from or writing to a named pipe
+   - Reading from or writing to an area of memory