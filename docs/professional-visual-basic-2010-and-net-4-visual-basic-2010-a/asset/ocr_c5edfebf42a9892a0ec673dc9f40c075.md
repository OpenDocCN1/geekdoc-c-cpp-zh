```
End If
If reader.NodeType = XmlNodeType.Whitespace Then
    Console.Out.WriteLine("Type: {0} ", reader.NodeType)
ElseIf reader.NodeType = XmlNodeType.Text Then
    Console.Out.WriteLine("Type: {0}, Value: {1} ", _
        reader.NodeType, _
        reader.Value)
Else
    Console.Out.WriteLine("Name: {0}, Type: {1}, " & _
        "AttributeCount: {2}, Value: {3} ", _
        reader.Name, _
        reader.NodeType, _
        reader.AttributeCount, _
        reader.Value)
End If
End Sub
```

Code snippet from FilmOrdersReader

Within the ShowXmlNode subroutine, each level of node depth adds two spaces to the output generated:

```
If reader.Depth > 0 Then
    For depthCount As Integer = 1 To reader.Depth
        Console.Write("  ")
    Next
End If
```

You add these spaces in order to create human-readable output (so you can easily determine the depth of each node displayed). For each type of node, ShowXmlNode displays the value of the NodeType property. The ShowXmlNode subroutine makes a distinction between nodes of type White space and other types of nodes. The reason for this is simple: A node of type White space does not contain a name or attribute count. The value of such a node is any combination of white-space characters (space, tab, carriage return, and so on). Therefore, it doesn’t make sense to display the properties if the NodeType is XmlNodeType.WhiteSpace. Nodes of type Text have no name associated with them, so for this type, subroutine ShowXmlNode only displays the properties NodeType and Value. For all other node types (including elements and attributes), the Name, AttributeCount, Value, and NodeType properties are displayed.

To finalize this module, add a Sub Main as follows:

```
Sub Main(ByVal args() As String)
    ReadMovieXml("..\MovieManage.xml")
End Sub
```

Here is an example construction of the input MovieManage.xml file:

```
<?xml version="1.0" encoding="utf-8" ?>
<MovieOrderDump>
    <FilmOrderList>
        <multiFilmOrders>
            <FilmOrder filmId="101">
                <name>Grease</name>
                <quantity>10</quantity>
            </FilmOrder>
            <FilmOrder filmId="102">
                <name>Lawrence of Arabia</name>
                <quantity>10</quantity>
            </FilmOrder>
            <FilmOrder filmId="103">
                <name>Star Wars</name>
                <quantity>10</quantity>
            </FilmOrder>
        </multiFilmOrders>
    </FilmOrderList>
</MovieOrderDump>
```