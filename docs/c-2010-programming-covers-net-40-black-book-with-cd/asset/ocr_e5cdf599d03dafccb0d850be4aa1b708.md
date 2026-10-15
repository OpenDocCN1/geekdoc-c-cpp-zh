# In Depth

Extensible Markup Language (XML) is a simple and flexible text format widely used to exchange different type of data on the Web. XML plays a very significant role with respect to .NET Framework, as it provides a namespace, System.Xml, which includes classes required to work with XML. You can import this namespace to use XML in the .NET applications. XML also stores data used in the .NET applications. ActiveX Data Objects (ADO) .NET is a primary tool used for data access and data manipulation in many programming languages supported by .NET Framework 4.0. ADO.NET uses XML as a medium of transferring data between applications and provides some powerful features to read and write XML documents.

Document Object Model (DOM) is a platform and language independent interface, which allows programs and scripts to access and update the content and structure of documents dynamically. You implement DOM with the help of the XmlDocument class. In addition, you can serialize and deserialize objects using the System.Xml.Serialization namespace.

In this chapter, you learn about the support for XML provided by .NET Framework 4.0. You learn about the System.Xml namespace, and how to work with streamed XML. In addition, you learn to implement DOM in .NET. You also learn about working with XPath and XSLT in .NET Framework 4.0. Finally, you learn how to use XML with ADO.NET, and how to work with object serialization in XML.

Now, let’s start our discussion by describing the support for XML provided by .NET Framework 4.0.

# Support for XML in .NET Framework 4.0

XML is a Data Description Language (DDL), which is developed by World Wide Web Consortium (W3C). It is used by ADO.NET as a format to store and transfer data. W3C has developed some standards for XML. The set of W3C standards supported by .NET Framework 4.0 are as follows:

+   - XML 1.0 (www.w3.org/TR/1998/REC-xml-19980210) with Document Type Definition (DTD) support
+   - XML Namespaces (www.w3.org/TR/REC-xml-names) for both stream-level and DOM
+   - XML Schemas (www.w3.org/2001/XMLSchema)
+   - XPath expressions (www.w3.org/TR/xpath)
+   - XSLT transformations (www.w3.org/TR/xslt)
+   - DOM Level 1 Core (www.w3.org/TR/REC-DOM-Level-1/)
+   - SOAP 1.1 (www.w3.org/TR/SOAP)

After exploring the different standards developed by W3C, let’s now look at the namespace to support XML in .NET Framework 4.0.

# The System.Xml Namespace

.NET Framework provides a namespace known as System.Xml, which contains classes to process XML. Table 30.1 describes some important classes contained in the System.Xml namespace:

Table 30.1: Important Classes in the System.Xml Namespace

| Class Name | Description |
|---|---|
| XmlReader | Specifies an abstract reader class that provides fast and forward-only non-cached XML data. |
| XmlWriter | Specifies an abstract writer class that provides fast non-cached XML data in the form of stream or file format. |
| XmlTextReader | Extends the XmlReader class and provides fast and forward-only stream access to XML data. |
| XmlTextWriter | Extends the XmlWriter class and provides fast and forward-only generation of XML streams. |
| XmlNode | Specifies an abstract class that represents a single node in an XML document. It is a base class for many classes in the XML namespace. |