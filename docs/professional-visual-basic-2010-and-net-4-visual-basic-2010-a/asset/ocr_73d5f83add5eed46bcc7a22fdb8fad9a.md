Before exploring the System.Xml.Serialization namespace, take a moment to consider the various uses of the term attribute.

# Source Code Style Attributes

Thus far, you have seen attributes applied to a specific portion of an XML document. Visual Basic has its own flavor of attributes, as does C# and each of the other .NET languages. These attributes refer to annotations to the source code that specify information, or metadata, that can be used by other applications without the need for the original source code. We will call such attributes Source Code Style attributes.

In the context of the System.Xml.Serialization namespace, Source Code Style attributes can be used to change the names of the elements generated for the data members of a class or to generate XML attributes instead of XML elements for the data members of a class. To demonstrate this, we will change the FilmOrder class using these attributes to change the outputted XML.

To rename the XML generated for a data member, a Source Code Style attribute will be used. This Source Code Style attribute specifies that when FilmOrder is serialized, the name data member is represented as an XML element, <Title>. The actual Source Code Style attribute that specifies this is as follows:

```
<XmlElementAttribute("Title")> Public Name As String
```

The updated FilmOrder (contained in the FilmOrderAttributes project) also contains other Source Code Style attributes:

+   > <XmlAttributeAttribute("ID")> specifies that FilmId is to be serialized as an XML attribute named ID.

+   > <XmlAttributeAttribute("Qty")> specifies that Quantity is to be serialized as an XML attribute named Qty.

The complete modified FilmOrder is defined as follows:

```
Imports System.Xml.Serialization
Public Class FilmOrder
    <XmlElementAttribute("Title")> Public Name As String
    <XmlAttributeAttribute("ID")> Public FilmId As Integer
    <XmlAttributeAttribute("Qty")> Public Quantity As Integer
    Public Sub New()
    End Sub
    Public Sub New(ByVal name As String, _
                   ByVal filmId As Integer, _
                   ByVal quantity As Integer)
        Me.Name = name
        Me.FilmId = filmId
        Me.Quantity = quantity
    End Sub
End Class
```

Note that you needed to include the System.Xml.Serialization namespace to bring in the Source Code Style attributes used.

The serialization code in Sub Main() doesn't change:

```
Dim serialize As XmlSerializer = _
    New XmlSerializer(GetType(FilmOrder))
Dim MyMovieOrder As FilmOrder = _
    New FilmOrder("Grease", 101, 10)
serialize.Serialize(Console.Out, MyMovieOrder)
Console.Readline()
```