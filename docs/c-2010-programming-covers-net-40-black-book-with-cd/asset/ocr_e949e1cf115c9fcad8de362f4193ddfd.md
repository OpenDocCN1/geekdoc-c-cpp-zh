The System.Xml.Linq namespace contains classes for LINQ to XML. The following are some of the variety of functions that can be performed by using LINQ to XML:

+   - Loading XML from files or streams
+   - Serializing XML to files and streams
+   - Creating XML trees using functional construction
+   - Querying XML trees using LINQ queries
+   - Controlling the in-memory XML trees
+   - Validating the XML trees using XML Schema Definition (XSD)

Let’s now learn about the difference between LINQ to XML and the DOM method and how to work with XML trees in LINQ.

# Difference Between LINQ to XML and DOM Method

XML Document Object Model (DOM) is the current predominant XML programming API. In XML DOM, you build an XML tree in the bottom up direction. The typical way to create an XML tree using DOM is to use the XmlDocument class. LINQ to XML also supports the XmlDocument class approach for constructing an XML tree. It also supports an alternative approach, called the functional construction, which uses the XElement and XAttribute constructors to build an XML tree.

In LINQ to XML, you can directly work with XML elements and attributes. You can create XML elements without using a document object. It also loads the T:System.Xml.Linq.XElement object directly from an XML file. It also serializes the T:System.Xml.Linq.XElement object to a file or a stream. When you compare this with XML DOM, the XML document is used as a logical container for the XML tree. In XML DOM, the nodes, which also include the elements and attributes, are created in the context of an XML document. The use of XML DOM is also complex. For example, if you want to use an element across multiple documents, you must import the nodes across the documents. This kind of complexity is not included in LINQ to XML.

The use of LINQ to XML also simplifies the names and namespaces by eliminating the prerequisite to deal with namespace prefix completely. The use of XML DOM does not let you change the name of node. As a substitute, you have to create a new node and copy all the child nodes to it, which leads to losing the original child identity. LINQ to XML supports whitespace more simply than XML DOM.

# Working with XML Trees in LINQ

LINQ to XML provides a powerful way to create XML elements called functional construction, which has the ability to create an XML tree in a single statement. You need to use the XElement constructor that takes various types of argument for the content to create an XML tree in LINQ. The XElement constructor takes params array type of Object, so that you can pass any number of objects to the constructor. This helps you in using an element that has a complex content. The XAttribute object becomes the attribute of an element.

When you actually create an XML tree, the XElement and XAttribute constructors let you pass the content of the attribute or element as an argument to the constructor. You can pass any number of child elements in them as one of the constructors take a variable number of arguments. It supports any type of object that is a valid child element of an XElement constructor. You should keep in mind the following rules while creating an XML tree in LINQ:

+   - The string is added as a text content
+   - An XElement class is added as an attribute
+   - An XAttribute class is added as an attribute
+   - You should call the ToString() method for any other type than string

You learn more about working with XML tree in the Immediate Solutions section of this chapter.

# The LinqDataSource Control

The LinqDataSource control enables you to use LINQ in an ASP.NET Web page by setting the properties in the markup text. You can use the LinqDataSource control to create a Web page that retrieves or modifies the