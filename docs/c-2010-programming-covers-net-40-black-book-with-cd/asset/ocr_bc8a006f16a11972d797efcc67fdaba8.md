# The XPathExpression Class

The XPathExpression class encapsulates a compiled XPath query expression, which contains the syntax for confirming the W3C XPath Query Language specification. Therefore, you should have to compile an XPath query expression before executing the query expression of the code. The XPathExpression class is used to supply a precompiled XPath query expression in case of calling the Select() method of the XPathNavigator class. You can also invoke the Compile() method of the XPathNavigator class to return an object of the XPathExpression class.

# The XPathException Class

XPathException is an exception class, which generates the exception when an error occurs during the execution of XPath query expression. The Select() and Compile() methods of the XPathNavigator class can raise the XPathException exception.

# The System.Xml.Xsl Namespace

The classes contained in the System.Xml.Xsl namespace are used to perform XSL transformations in .NET Framework. The contents of this namespace are available to the classes that implement the IXPathNavigable interface. In .NET Framework, the XmlDocument, XmlDataDocument, and XPathDocument classes implement the IXPathNavigable interface. If you want to create a custom store with a set of classes, you need to implement the IXPathNavigable interface in your class. For instance, a class is using a file system and performs XSLT transformations. XSLT uses a streaming pull model to pull data into the application. Therefore, you can perform several transformations together. A custom reader can be applied between transformations, if required.

Let’s learn how XML is used with ADO.NET.

# Using XML with ADO.NET

XML is a medium of exchanging data from the data stores and applications. ADO.NET is primarily designed to work in the XML environment. It provides some powerful features that are used to read and write XML documents. Some classes contained in the System.Xml namespace, such as XmlDataDocument, are also used to work with ADO.NET relational data.

You can create an XML file with the data from an ADO.NET data source by first filling a DataSet object with the data from an ADO.NET data source and then calling the WriteXml() method of the DataSet object. The WriteXml() method has two overloaded forms, one of which takes a string with the file path and name, and the other takes one more parameter to specify the mode, which takes the value from an XmlWriteMode enumeration. The XmlWriteMode enumeration has three values, which are as follows:

+   - IgnoreSchema – Ignores or does not provide an inline schema at the start of an XML file.
+   - WriteSchema – Provides an inline schema at the start of an XML file.
+   - DiffGram – Specifies an XML document that contains data related to pre- and post-edit sessions. A DiffGram may include any type of changes made in data, such as addition and deletion of some data elements. The DiffGram is useful in audit trail for a commit/rollback process. A DiffGram comes as a built-in feature in most of the Database Management Systems (DBMSs) these days.

Let’s learn how objects are serialized in XML.

# Object Serialization with XML

Retaining an object’s data into the memory disk is called object serialization. In object serialization, public properties and fields of an object are converted into XML elements or attributes, or both. The data that you can serialize may be a primitive type, field, array, or embedded XML in the form of the XmlElement and XmlAttribute objects.

In .NET Framework, you can serialize objects with the help of a class, named XmlSerializer, contained in the System.Xml.Serialization namespace. For this, you first create an object of the XmlSerializer class by specifying the type of object that you want to serialize. Next, you create a stream/writer object to write the file to