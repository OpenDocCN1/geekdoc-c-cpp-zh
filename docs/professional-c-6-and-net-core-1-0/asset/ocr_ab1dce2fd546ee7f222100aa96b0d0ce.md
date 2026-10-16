# 27
# XML and JSON

# ## What’s In This Chapter?

+   - XML standards
+   - XmlReader and XmlWriter
+   - XmlDocument
+   - XPathNavigator
+   - LINQ to XML
+   - Working with objects in the System.Xml.Linq namespace
+   - Querying XML documents using LINQ
+   - Creating JSON
+   - Converting Objects to and from JSON

# ## Wrox.com Code Downloads for This Chapter

The wrox.com code downloads for this chapter are found at [www.wrox.com/go/professionalcsharp6](http://www.wrox.com/go/professionalcsharp6) on the Download Code tab. The code for this chapter is divided into the following major examples:

+   - XmlReaderAndWriter
+   - XmlDocument
+   - XPathNavigator
+   - ObjectToXmlSerialization
+   - ObjectToXmlSerializationWOAttributes
+   - LinqToXmlSample
+   - JsonSample

# # Data Formats

The Extensible Markup Language (XML) has been playing an important part in information technology since 1996. The language is used to describe data, and it’s used with configuration files, source code documentation, web services that make use of SOAP, and more. In recent years, it has been replaced in some ways (for example, configuration files and data transfer from REST-based web services) by JavaScript Object Notation (JSON) because this technology has less overhead and can be used easily from JavaScript. However, JSON cannot replace XML in all the scenarios where XML is used today. Both of these data formats can be used with .NET applications, as covered in this chapter.