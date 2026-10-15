```
var game = new Pair<string>("Redskins", "Eagles");
foreach (string name in game.GetReverseEnumerator())
{
    Console.WriteLine(name);
}
```

Note that you return IEnumerable<T>, not IEnumerator<T>. This is different from IEnumerable<T>.GetEnumerator(), which returns IEnumerator<T>. The code in Main() demonstrates how to call GetReverseEnumerator() using a foreach loop.

# yield Statement Requirements

You can use the yield return statement only in members that return an IEnumerator<T> or IEnumerable<T> type, or their nongeneric equivalents. Members whose bodies include a yield return statement may not have a simple return. If the member uses the yield return statement, the C# compiler generates the necessary code to maintain the state of the iterator. In contrast, if the member uses the return statement instead of yield return, the programmer is responsible for maintaining his own state machine and returning an instance of one of the iterator interfaces. Further, just as all code paths in a method with a return type must contain a return statement accompanied by a value (assuming they don’t throw an exception), so all code paths in an iterator must contain a yield return statement if they are to return any data.

The following additional restrictions on the yield statement result in compiler errors if they are violated:

+   - The yield statement may appear only inside a method, a user-defined operator, or the get accessor of an indexer or property. The member must not take any ref or out parameter.
+   - The yield statement may not appear anywhere inside an anonymous method or lambda expression (see Chapter 12).
+   - The yield statement may not appear inside the catch and finally clauses of the try statement. Furthermore, a yield statement may appear in a try block only if there is no catch block.