+   - RemoveAll - Removes all child nodes.
+   - RemoveChild - Removes the given child from the current node.
+   - SelectNodes - Selects a list of nodes matching the XPath expression (discussed in the following section).
+   - SelectSingleNode - Selects a single node that matches the XPath expression.

# 17.9.1.4  XMLDocument Class

The XmlDocument class, deals with the entire document, is also itself an XmlNode. The XmlDocument class, inherits from XmlNode. This fits with the DOM pattern in that the document is a node that can have child nodes. The methods in the following list show some of the additional methods available to the XmlDocument that are not part of a standard node class.

# XmlDocument Class Methods

+   - CreateAttribute - Creates an XmlAttribute with the given name.
+   - CreateDataSection - Creates a CData section with the given data.
+   - CreateComment - Creates an XmlComment.
+   - CreateDocumentFragment - Creates a document fragment.
+   - CreateElement - Creates an XmlElement, an XmlNode with element-specific functionality.
+   - CreateNode - Creates an XmlNode.
+   - CreateTextNode - Creates an XmlText node.
+   - CreateWhitespace - Creates whitespace for insertion into the document.
+   - ImportNode - Imports a node from another document.
+   - Load - Loads the XML from the given file.
+   - LoadXml - Loads the XML from the given XML string.
+   - Save - Saves the XML document.
+   - Validate - Validates the XML document against a schema.

# Program 1

```
```xml
//Add node/xml value to existing XML
string tempXml = @"<states>
<State ID='1' Name='Punjab' />
<State ID='2' Name='Rajasthan' />
<State ID='3' Name='Gujrat' />
<State ID='4' Name='Maharashtra' />
<State ID='5' Name='Tamilnadu' />
</State>";
```
```