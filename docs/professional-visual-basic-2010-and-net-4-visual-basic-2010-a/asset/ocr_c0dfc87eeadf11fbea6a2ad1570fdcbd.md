# Writing to an XML Document

In addition to reading from an XML document, you can also write to the document just as easily. For instance, if you wanted to change the name of the first player of the hamlet file, you could make use of the code here to accomplish that task:

```
Module Module1
    Sub Main()
        Dim xdoc As XDocument = XDocument.Load("hamlet.xml")
        xdoc.Element("PLAY").Element("PERSONAE")._
            Element("PERSONA").SetValue("Foo deBar, King of Denmark")
        Console.WriteLine(xdoc.Element("PLAY")._
            Element("PERSONAE").Element("PERSONA").Value)
        Console.ReadLine()
    End Sub
End Module
```

Code snippet from LinqWrite

In this case, the first instance of the <PERSONA> element is overwritten with the value of Foo deBar, King of Denmark using the SetValue method of the Element object. After the SetValue is called and the value is applied to the XML document, the value is then retrieved using the same approach as before. Running this bit of code, you can indeed see that the value of the first <PERSONA> element has been changed.

Another way to change the document (by adding items to it in this example) is to create the element you want as XElement objects and then add them to the document:

```
Module Module1
    Sub Main()
        Dim xdoc As XDocument = XDocument.Load("hamlet.xml")
        Dim xe As XElement = New XElement("PERSONA", _
            "Foo deBar, King of Denmark")
        xdoc.Element("PLAY").Element("PERSONAE").Add(xe)
        Dim query = From people In xdoc.Descendants("PERSONA") _
            Select people.Value
        Console.WriteLine("{0} Players Found", query.Count())
        Console.WriteLine()
        For Each item In query
            Console.WriteLine(item)
        Next
        Console.ReadLine()
    End Sub
End Module
```

Code snippet from LinqAdd

In this case, an XElement document called xe is created. The construction of xe gives you the following XML output:

```
<PERSONA>Foo deBar, King of Denmark</PERSONA>
```

Then, using the Element().Add method from the XDocument object, you are able to add the created element:

```
xdoc.Element("PLAY").Element("PERSONAE").Add(xe)
```

Next, querying all the players, you will now find that instead of 26, as before, you now have 27, with the new one at the bottom of the list. Besides Add, you can also use AddFirst, which does just that — adds the player to the beginning of the list instead of the end, which is the default.