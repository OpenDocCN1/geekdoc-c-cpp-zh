# Filtering

In Listing 16.1, where a clause filters out reserved keywords but not contextual keywords. This clause filters the collection "vertically": If you think of the collection as a vertical list of items, the where clause makes that list shorter so that the collection holds fewer items. The filter criteria are expressed with a predicate—a lambda expression that returns a bool such as .Contains() as in Listing 16.1 or File.GetLastWriteTime(fileName) < DateTime.Now.AddMonths(-1). The latter is in Listing 16.6, whose output appears in Output 16.5.

Listing 16.6: Query Expression Filtering Using where

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
//
public static void FindMonthOldFiles(
    string rootDirectory, string searchPattern)
{
    IEnumerable<FileInfo> files =
        from fileName in Directory.EnumerateFiles(
            rootDirectory, searchPattern)
        where File.GetLastWriteTime(fileName) <
            DateTime.Now.AddMonths(-1)
        select new FileInfo(fileName);

    foreach (FileInfo file in files)
    {
        // As a simplification, the current directory is
        // assumed to be a subory of
        // rootDirectory
        string relativePath = file.FullName.Substring(
            Directory.GetCurrentDirectory().Length);
        Console.WriteLine(
            "$ {relativePath} ({file.LastWriteTime})");
    }
}
//...
```