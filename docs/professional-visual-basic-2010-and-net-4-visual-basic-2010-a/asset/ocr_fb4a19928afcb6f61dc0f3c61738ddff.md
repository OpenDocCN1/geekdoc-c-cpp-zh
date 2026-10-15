Where do lambda expressions fit in with XML? The LINQ expressions you have been using are written internally as lambda expressions (LINQ is actually why lambda expressions were added to .NET).

In addition, you can use your own lambdas to simplify complex queries by replacing the queries with lambda expressions. For example, the following code prints off a subset of the lines from the hamlet.xml file that you've been using:

```
Dim doc As XElement = XElement.Load("..\..\hamlet.xml")
Dim speakers = {"OPHELIA", "LORD POLONIUS" }

Dim lines As List(Of String) =
    (From line In doc.Descendants("SPEECH") _
        .Where(Function(item As XElement)
            Return speakers.Contains(item.Descendants("SPEAKER").Value)
        End Function) _
        .Select(Function(item As XElement)
            Return String.Format("{0} said, {1}{2}{3}",
                item.Descendants("SPEAKER").Value,
                ControlChars.Quote,
                item.Descendants("LINE").Value,
                ControlChars.Quote)
        End Function)).ToList()

lines.ForEach(Sub(line)
    Console.WriteLine(line)
End Sub)
```

Code snippet from Lambdas

The XML file is loaded into an XElement for processing, and an array of speakers is initialized. This uses the new syntax for initializing an array. You want to return the lines spoken by any of the people listed in the array. You could do this in regular LINQ syntax, but using a lambda reduces the where clause to a few lines. Notice that in this case, you still need to use statement completion characters to break up the long query.

In the previous examples, the lambda expression was written first, then used. However, in this example, the expressions are actually written where they will execute. Which form you should use depends on what you are attempting to accomplish, and the needs of the application, just as when you are trying to decide if a function should be written as a standalone function, or inline. For example, if you only need to access the lambda once or twice, writing it first is probably a good idea. In this case, the lambda is only used once, therefore putting it inline is a better choice. In addition, by having the lambda within the LINQ query, you get a better view of just what the lambda is doing (i.e. in the Where clause, the lambda returns the records desired, while in the Select clause, it formats the output)

A second lambda expression is used in the select clause to concatenate some of the child nodes of the <SPEECH> element in the XML. Finally, the entire result set is converted into a List(Of String). Each element in the list is a string containing the speaker and the line:

LORD POLONIUS said, "By the mass, and 'tis like a camel, indeed."

Next, the code prints off the selected lines (see Figure 9-13). In this case it uses the new Sub version of a lambda. This works exactly like the lambdas you've used earlier, except that it doesn't return any value.