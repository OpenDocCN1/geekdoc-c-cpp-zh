In this example, the type FileInfo was chosen because it has the two relevant fields needed for the desired output: the filename and the last write time. There might not be such a convenient type if you needed other information not captured in the FileInfo object. Tuples (or anonymous types prior to C# 7.0) provide a convenient and concise way to project the exact data you need without having to find or create an explicit type. Listing 16.3 provides output similar to that in Listing 16.2, but via tuple syntax rather than FileInfo.

# **LISTING 16.3: Tuples within Query Expressions**

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.IO;

// ...

static void List2(string rootDirectory, string searchPattern)
{
    var fileNames =Directory.EnumerateFiles(
        rootDirectory, searchPattern)
    var fileResults =
        from fileName in fileNames
        select
        (
            Name: fileName,
            LastWriteTime: File.GetLastWriteTime(fileName)
        );

    foreach (var fileResult in fileResults)
    {
        Console.WriteLine(
            $"{0}{ fileResult.Name } ({
            fileResult.LastWriteTime })");
    }
}

// ...
```

In this example, the query projects out only the filename and its last file write time. A projection such as the one in Listing 16.3 makes little difference when working with something small, such as FileInfo. However, “horizontal” projection that filters down the amount of data associated with each item in the collection is extremely powerful when the amount of data is significant and retrieving it (perhaps from a different computer