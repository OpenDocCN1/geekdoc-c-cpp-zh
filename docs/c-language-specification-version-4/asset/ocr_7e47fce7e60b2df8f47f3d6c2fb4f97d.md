```
```
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```
```

The example below creates a file named `log.txt` and writes two lines of text to the file. The example then opens that same file for reading and copies the contained lines of text to the console.

```
```csharp
using System;
using System.IO;

class Test
{
    static void Main() {
        using (TextWriter w = File.CreateText("log.txt")) {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }
        using (TextReader r = File.OpenText("log.txt")) {
            string s;
            while ((s = r.ReadLine()) != null) {
                Console.WriteLine(s);
            }
        }
    }
}
```
```

Since the `TextWriter` and `TextReader` classes implement the `IDisposable` interface, the example can use `using` statements to ensure that the underlying file is properly closed following the write or read operations.

# ## 8.14 The yield statement

The `yield` statement is used in an iterator block (§8.2) to yield a value to the enumerator object (§10.14.4) or enumerable object (§10.14.5) of an iterator or to signal the end of the iteration.

```
```
yield-statement:
    yield return expression ;
    yield break ;
```
```

`yield` is not a reserved word; it has special meaning only when used immediately before a `return` or `break` keyword. In other contexts, `yield` can be used as an identifier.

There are several restrictions on where a `yield` statement can appear, as described in the following.

+   - It is a compile-time error for a `yield` statement (of either form) to appear outside a *method-body*, *operator-body* or *accessor-body*
+   - It is a compile-time error for a `yield` statement (of either form) to appear inside an anonymous function.
+   - It is a compile-time error for a `yield` statement (of either form) to appear in the *finally* clause of a *try* statement.
+   - It is a compile-time error for a `yield return` statement to appear anywhere in a *try* statement that contains any *catch* clauses.

The following example shows some valid and invalid uses of `yield` statements.

```
```csharp
delegate IEnumerable<int> D();
```
```