# LISTING 15.9: Ordering the Results in a Query Expression

```
// ...
IEnumerable<FileInfo> files =
    from fileName in Directory.EnumerateFiles(
        rootDirectory, searchPattern)
    let file = new FileInfo(fileName)
    orderby file.Length, fileName
    select file;
// ...
```

The let clause introduces a new range variable that can hold the value of an expression that is used throughout the remainder of the query expression. You can add as many let clauses as you like; simply add each as an additional clause to the query after the first from clause but before the final select/group by clause.

# Grouping

A common data manipulation scenario is the grouping of related items. In SQL, this generally involves aggregating the items to produce a summary or total or other aggregate value. LINQ, however, is notably more expressive. LINQ expressions allow for individual items to be grouped into a series of subcollections, and those groups can then be associated with items in the collection being queried. For example, Listing 15.10 and Output 15.6 demonstrate how to group together the contextual keywords and the regular keywords.

# LISTING 15.10: Grouping Together Query Results

```
using System;
using System.Collections.Generic;
using System.Linq;

// ...

private static void GroupKeywords1()
{
    IEnumerable<IGrouping<bool, string>> selection =
        from word in Keywords
        group word by word.Contains('*');

    foreach (IGrouping<bool, string> wordGroup
        in selection)
    {
        Console.WriteLine(Environment.NewLine + "{0}:",
            wordGroup.Key ?
```