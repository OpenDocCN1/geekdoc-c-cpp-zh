# nodes:

The Autobiography of Benjamin Franklin
Benjamin
Franklin
8.99
The Confidence Man
Herman
Melville
11.99
The Gorgias
Plato
9.99

# Using Read Methods

Several ways exist to move through the document. As shown in the previous example, Read takes you to the next node. You can then verify whether the node has a value (HasValue) or, as you see later, whether the node has any attributes (HasAttributes). You can also use the ReadStartElement method, which verifies whether the current node is the start element and then positions you on the next node. If you are not on the start element, an XmlException is raised. Calling this method is the same as calling the IsStartElement method followed by a Read method.

ReadElementString is similar to ReadString except that you can optionally pass in the name of an element. If the next content node is not a start tag, or if the Name parameter does not match the current node Name, an exception is raised.

Here is an example showing how you can use ReadElementString. Notice that it uses FileStreams, so you need to ensure that you import the System.IO namespace (code file XMLReaderAndWriterSample/Program.cs):

```
public static void ReadElementContent()
{
    using (XmlReader reader = XmlReader.Create(BooksFileName))
    {
        while (!reader.EOF)
        {
            if (reader.MoveToContent() == XmlNodeType.Element &&
                reader.Name =="title")
            {
                WriteLine(reader.ReadElementContentAsString());
            }
            else
            {
                // move on
                reader.Read();
            }
        }
    }
}
```

In the while loop, the MoveToContent method is used to find each node of type XmlNodeType.Element with the name title. The EOF property of the XmlTextReader checks the end of the loop condition. If the node is