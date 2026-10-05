# Common members of the XmlReader class

| Indexer | Description |
| --- | --- |
| [name] | Gets the value of the specified attribute. If the current element doesn't have the attribute, an empty string is returned. |
| Property | Description |
| NodeType | Returns a member of the XmlNodeType enumeration that indicates the type of the current node. |
| Name | Gets the name of the current node, if the node has a name. |
| Value | Gets the value of the current node, if the node has a value. |
| EOF | Returns a true value if the reader has reached the end of the stream. |
| Method | Description |
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
| --- | --- |
| IgnoreWhitespace | Gets or sets a Boolean value that indicates whether to ignore white space. If set to false, white space is treated as a node. |
| IgnoreComments | Gets or sets a Boolean value indicating whether to ignore comments. |

# Description

+   * Some of these methods throw an XmlException if they encounter an unexpected situation such as when the next element does not match the specified name.

![](bbox=[0.051, 0.946, 0.866, 0.966])