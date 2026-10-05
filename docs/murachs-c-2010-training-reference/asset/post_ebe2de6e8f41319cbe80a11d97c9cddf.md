
# Code that writes an XML document

Figure 22-6 shows the code that creates an XML document like the one that's in figure 22-1. This code gets its data from a List<> collection of objects where each product has three properties: Code, Description, and Price.

To start, this code defines a string variable that points to the Products.xml file that is stored in the C:\2010\Files directory. Then, it creates an XmlWriterSettings object and sets the Indent and IndentChars properties to the XmlWriter object four spaces to indent each level of child elements.

Finally, this code creates an XmlWriter object, it uses the WriteStartDocument method to write the XML declaration for the document. In addition, it uses the WriteStartElement method to write the start tag for the root element of the document, which is the Products.

The heart of this code is the foreach loop that writes a Product element for each Product object in the List<> collection. To write a Product element, the method uses the WriteStartElement method to write the start tag for the Product element, and then uses the WriteAttributeString method to write the Attribute. Next, two WriteElementString methods are used to write the Description and Price elements. Finally, the WriteEndElement method is used to write the end tag for the Product element.

Since the foreach loop is preceded by a WriteStartElement method that writes the start tag for the document's root element, the loop must be followed by a WriteEndElement method that writes the end tag for the root element. After that, the Close method is used to close the XmlWriter object. In this case, the path of the XML document is coded as an absolute path

```c
string path = @
```

In this case, the XML file is stored in a directory other than the one where the rest of the files for the ProductMaintenance project are stored. However, if you want to use an XML file that's part of the project, you can specify a relative path like this:

This works because for the application runs from the bin\Debug subdirectory of the project directory. As a result, you need to navigate back two directories to get to the directory that stores the files for the project.

# Code that writes an XML document

```csharp
// create the path variable
string path = "C:\C# 210\Files\Products.xml";

// create the XmlWriterSettings object
XmlWriterSettings settings = new XmlWriterSettings();
settings.Indent = true;
settings.IndentChars = ("  ");

// create the XmlWriter object
XmlWriter xmlOut = XmlWriter.Create(path, settings);

// write the start of the document
xmlOut.WriteStartDocument();
xmlOut.WriteStartElement("Products");

// write each Product object to the xml file
foreach (Product product in products)
{
xmlOut.WriteStartElement("Product");
xmlOut.WriteAttributeString("Code",
product.Code);
xmlOut.WriteElementString("Description",
product.Description);
xmlOut.WriteElementString("Price",
Convert.ToString(product.Price));
xmlOut.WriteEndElement();
}

// write the end tag for the root element
xmlOut.WriteEndElement();

// close the XmlWriter object
xmlOut.Close();
```

# Description

- This example saves a List<> collection of Product objects as an XML document. The resulting XML document will be the one in figure 22-1.
- To set the path for an XML file in the current project, you can use two dots to refer to the parent directory as in:
  "@..\.\Products.xml"
This works because the current project is run from the bin\Debug subdirectory of the project directory.

![](img/3148667e42d4db35b3d08576aaa1fa01_714_0.png)

Figure 22-6 Code that writes an XML document

# How to use the XmlReader class

To read an XML document, you can use the XmlReader class that's summarized in figure 22-7. Like the XmlWriter class, the XmlReader is an abstract class. As a result, to create an object from this class, you must use the Static method that is available from the class. When you do that, you must supply the path of the XML file as a string. In addition, you can optionally supply an XmlReaderSettings object that contains any settings that you want to set for the XmlReader object.

For example, you typically want to set the IgnoreWhitespace property of the XmlReaderSettings to indicate how you handle white space. White space refers to spaces, tabs, and return characters that affect the appearance but not the meaning of an XML document. To simplify the task of processing XML data, you typically set the IgnoreWhitespace to true. That, the XmlReader object will automatically skip white space in the XML document, and you won't have to write code to handle it.

Similarly, you typically want to set the IgnoreComments property of the XmlReaderSettings to true. That, the XmlReader object will automatically skip any comments in the XML document, and you won't have to write code to handle them.

To read data from an XML document, you can use the various methods of the XmlReader class. This class treats an XML document as a series of nodes, and you can use the Read method to read the next node from the file. Because the concept of nodes is important to reading XML data, the next figure describes them in detail and walks you through the process of reading a simple XML document node by node. For now, you just need to know that every tag in an XML document is treated as a separate node, and each element's content is also treated as a separate node. Attributes, however, are not treated as nodes. Instead, an attribute is treated as part of a tag node.

When you invoke the Read method, the XmlReader gets the next node from the XML document and makes it the current node. Then, you can use the XmlReader's NodeType, Name, or Value property to retrieve the node's type, name, or value. If you read the last node in the document, the EOF property is set to true. As a result, you can use this property to tell you when have reached the end of the file.

In fact, you can process an entire document by just using the Read method to read the nodes one at a time, by using the NodeType property to determine what kind of node has been read, and by taking appropriate action based on the node type.

However, the XmlReader has several other methods that simplify the task of parsing an XML document. For example, you can use the ReadToDescendant and ReadNextSibling elements to read the element that you want to process. In addition, you can use the ReadElementContentAsString and ReadElementContentAsDecimal methods to read content from an element that contains content.

# Common members of the XmlReader class

| Type | Description |
| :--- | :--- |
| Indexer | Gets the value of the specified attribute. If the current element doesn't have the attribute, an empty string is returned. |
| NodeType | Returns a member of the XmlNodeType enumeration that indicates the type of the current node. |
| Name | Gets the name of the current node, if the node has a name. |
| Value | Gets the value of the current node, if the node has a value. |
| EOF | Returns a true value if the reader has reached the end of the stream. |
| Create (path) | A static method that creates an XmlReader object using the specified path or name. |
| Create (path, settings) | A static method that creates an XmlReader object using the specified path or name and the XmlReaderSettings object. |
| Read() | Reads the next node. |
| ReadStartElement (name) | Checks that the current node is a start tag with the specified name, then advances to the next node. |
| ReadEndElement () | Checks that the current node is an end tag, then advances to the next node. |
| ReadToDescendant (name) | If the specified descendant is found, this method advances to it and returns a true value. Otherwise, it advances to the end of the current element and returns a false value. |
| ReadNextSibling (name) | If the specified sibling is found, this method advances to it and returns a true value. Otherwise, it advances to the end tag of the current element and returns a false value. |
| ReadElementAsString() | Reads the current element, returns the content as a string, and moves the element's end tag. |
| ReadElementAsDecimal() | Reads the current element, returns the content as a decimal value, and moves the element's end tag. |
| Close () | Closes the XmlReader and releases any resources. |

# Common properties of the XmlReaderSettings class

| Property | Description |
| :--- | :--- |
| IgnoreWhitespace | Gets or sets a Boolean value that indicates whether to ignore white space. If set to false, white space is treated as a node. |
| IgnoreComments | Gets or sets a Boolean value indicating whether to ignore comments. |

# Description

- Some of these methods throw an XmlException if they encounter an unexpected situation such as when the next element does not match the specified name.

![](img/3148667e42d4db35b3d08576aaa1fa01_716_0.png)
