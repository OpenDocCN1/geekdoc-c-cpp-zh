# HOW TO FILTER THE RESULTS (WHERE CLAUSE)

The C# compiler behind the scenes converts the lambda expression into a standard anonymous method call (the following code is functionally equivalent):

```
var q = animals.Where(
  delegate(string a) {
    return a.StartsWith("S") && a.Length > 5; });
```

What Is Deferred Execution?
The Where clause will only begin testing the predicate when somebody (you through a foreach statement or one of the other standard query operators that have an internal foreach statement) tries to iterate through the results; until then, the iterator framework remembers exactly where it was the last time it was asked for an element. This is called deferred execution, and it allows you some predictability and control over when and how a query is executed. If you want results immediately you can call List(), ToArray() or one of the other standard operators that cause immediate realization of the results to another format; otherwise, the query will begin evaluation only when you begin iterating over it.

# Where Filter Query Expressions (Preferred)

The query expression where clause syntax drops the explicit range variable definition and the lambda expression operator (=>), making it more concise and more familiar to the SQL-style clauses that many developers understand. It is the preferred syntax for these reasons. Rewriting the previous example using query expression syntax demonstrates these differences, as follows:

```
string[] animals = new string[] { "Koala", "Kangaroo",
"Spider", "Wombat", "Snake", "Emu", "Shark",
"Sting-Ray", "Jellyfish" };
```

```
var q = from animals
  a.StartsWith("S") && a.Length > 5
  select a;
```

```
foreach (string s in q)
  Console.WriteLine(s);
```