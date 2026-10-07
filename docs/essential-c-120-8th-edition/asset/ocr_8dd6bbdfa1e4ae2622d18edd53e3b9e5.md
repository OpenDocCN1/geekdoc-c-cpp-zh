# LISTING 16.9: Ordering the Results in a Query Expression

```
//...
Iumerable<FileInfo> files =
    from fileName in Directory.EnumerateFiles(
        rootDirectory, searchPattern)
    let file = new FileInfo(fileName)
    order by file.Length, fileName
    select file;
//...
```

the query after the first from clause but before the final select/group clause.

# Grouping

A common data manipulation scenario is the grouping of related items. In SQL, this generally involves aggregating the items to produce a summary or total or some other aggregate value. LINQ, however, is notably expressive. LINQ expressions allow individual items to be grouped into a series of subcollections, and those groups can then be associated with items in the collection being queried. For example, Listing 16.10 and Output 16.6 demonstrate how to group together the contextual keywords and the regular keywords.

# LISTING 16.10: Grouping Together Query Results

```
using System;
using System.Collections.Generic;
using System.Linq;
//
    private static void GroupKeywords()
{
        Iumerable<IGrouping<bool, string>> selection =
            from word in CSharp.Keywords
            group word by word.Contains('*');

        foreach(IGrouping<bool, string> wordGroup
        in selection)
        {
            Console.WriteLine(Environment.NewLine + "{0}:",
                wordGroup.Key ? "Contextual Keywords" : "Keywords";");
            foreach(string keyword in wordGroup)
```