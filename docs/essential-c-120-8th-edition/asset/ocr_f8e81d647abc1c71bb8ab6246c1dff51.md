```
// ...
using System;
using System.Collections.Generic;
using System.Linq;
// ...
private static void ShowContextualKeywords() {
    IEnumerable<string> selection = =
    from word in CSharp.keywords
    where word.Contains('*')
    select word;
```

```
foreach (string keyword in selection) {
    Console.Write(keyword + " ");
}
```

# OUTPUT 16.1

abstract as base pool break byte case catch checked class const continue decimal default delegate do double else event explicit extern false finally fixed float for foreach goto if implicit in interface internal is lock namespace null object operator over override params private protected readonly return turn sbyte sealed short sizeof stackalloc static string struct switch this throw true type uint ulong unchecked unsafe ushort using virtual void volatile while

In this query expression, selection is assigned the collection of C# reserved keywords. The query expression in this example includes a clause that filters out the noncontextual keywords.

Query expressions always begin with a clause and end with a select clause or a group clause, identified by the from, select, or group contextual keyword, respectively. The identifier word in from clause is called a range variable; it represents each item in the collection, as the loop variable in a foreach loop represents each item in a collection.

Developers familiar with SQL notice that query expressions have a syntax that is similar to that of SQL. This design was deliberate—it was intended that programmers who already know SQL find it easy to learn LINQ. However, there are some obvious differences. The first difference that most SQL-experienced