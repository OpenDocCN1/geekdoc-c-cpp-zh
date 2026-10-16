standards that give XML its power and potential. Without these standards, XML would not have the impact on the development world that it does. The W3C website (www.w3.org) is a valuable source for all things XML.

The .NET Framework supports the following W3C standards:

+   - XML 1.0 (www.w3.org/TR/REC-xml), including DTD support
+   - XML namespaces (www.w3.org/TR/REC-xml-names), both stream level and DOM
+   - XML schemas (www.w3.org/XML/Schema)
+   - XPath expressions (www.w3.org/TR/xpath)
+   - XSLT transformations (www.w3.org/TR/xslt)
+   - DOM Level 1 Core (www.w3.org/TR/REC-DOM-Level-1)
+   - DOM Level 2 Core (www.w3.org/TR/DOM-Level-2-Core)
+   - SOAP 1.2 (www.w3.org/TR/SOAP)

The level of standards support changes as the W3C updates the recommended standards and as Microsoft and the community update .NET Core. Therefore, you need to make sure that you stay up to date with the standards and the level of support provided.

# Working with XML in the Framework

The .NET Framework gives you many different options for reading and writing XML. You can directly use the DOM tree to work with XmlDocument and classes from the System.Xml namespace and the System.Xml.XmlDocument NuGet package. This works well and is easy to do with files that fit into the memory.

For fast reading and writing XML, you can use the XmlReader and XmlWriter classes. These classes allow streaming and make it possible to work with large XML files. These classes are in the System.Xml namespace as well, but they’re in a different NuGet package: System.Xml.ReaderWriter.

For using the XPath standard to navigate and query XML, you can use the XPathNavigator class. This is defined in the System.Xml.XPath namespace in the NuGet package System.Xml.XmlDocument.

Since .NET 3.5, .NET has offered another syntax to query XML: LINQ. Although LINQ to XML doesn’t support the W3C DOM standard, it provides an easier option to navigate within the XML tree, and also allows easier creating of XML documents or fragments. The namespace needed here is System.Xml.Linq, and the NuGet package System.Xml.XDocument.