```
```xml
<author>
    <name>Plato</name>
</author>
<price>$9.99</price>
</book>
</bookstore>
```
```

*code snippet books.xml*

# READING AND WRITING STREAMED XML

The XmlReader and XmlWriter classes will feel familiar if you have ever used SAX. XmlReader-based classes provide a very fast, forward-only, read-only cursor that streams the XML data for processing. Because it is a streaming model, the memory requirements are not very demanding. However, you don't have the navigation flexibility and the read or write capabilities that would be available from a DOM-based model. XmlWriter-based classes produce an XML document that conforms to the W3C's XML 1.0 Namespace Recommendations.

XmlReader and XmlWriter are both abstract classes. The following classes are derived from XmlReader:

+   - XmlNodeReader
+   - XmlTextReader
+   - XmlValidatingReader

The following classes are derived from XmlWriter:

+   - XmlTextWriter
+   - XmlQueryOutput

XmlTextReader and XmlTextWriter work with either a stream-based object from the System.IO namespace or TextReader/TextWriter objects. XmlNodeReader uses an XmlNode as its source instead of a stream. The XmlValidatingReader adds DTD and schema validation and therefore offers data validation. You look at these a bit more closely later in this chapter.

# Using the XmlReader Class

XmlReader is a lot like SAX in the MSXML SDK. One of the biggest differences, however, is that whereas SAX is a push type of model (that is, it pushes data out to the application, and the developer has to be ready to accept it), the XmlReader is a pull model, where data is pulled into an application requesting it. This provides an easier and more intuitive programming model. Another advantage to this is that a pull model can be selective about the data that is sent to the application: if you don't want all of the data, you don't need to process it. In a push model, all of the XML data has to be processed by the application, whether it is needed or not.

The following is a very simple example of reading XML data, and later you will take a closer look at the XmlReader class. You'll find the code in the XmlReaderSample folder. Here is the code for reading in the books.xml document. As each node is read, the NodeType property is checked. If the node is a text node, the value is appended to the text box:

```
```csharp
using System.Xml;

private void button3_Click(object sender, EventArgs e)
{
    richTextBox1.Clear();
    XmlReader rdr = XmlReader.Create("books.xml");
    while (rdr.Read())
    {
        if (rdr.NodeType == XmlNodeType.Text)
```
```