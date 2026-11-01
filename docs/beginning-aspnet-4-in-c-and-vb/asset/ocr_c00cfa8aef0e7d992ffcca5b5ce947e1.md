Prior to the LINQ to XML release, working with XML using System.Xml was not an easy task. With the inclusion of System.Xml.Linq, you now find a series of capabilities that make the process of working with XML in your code much easier.

Many developers previously turned to the XmlDocument object to create XML within their application code. This object allows you to create XML documents that enable you to append elements, attributes, and other items in a hierarchical fashion. With LINQ to XML and the inclusion of the new System.Xml.Linq namespace, you will now find some new objects that make the creation of XML documents a much simpler process.

# WORKING WITH DIFFERENT XML OBJECTS

In addition to the LINQ querying ability included in .NET 4, the .NET Framework includes XML objects that work so well they can stand on their own outside of LINQ. You can use these objects in place of working directly with the DOM in this release. Within the System.Xml.Linq namespace, you will find a series of LINQ to XML helper objects that make working with an XML document in memory much easier

The following sections work through the objects that are available to you within this namespace.

![](bbox=[0.2, 0.68, 0.88, 0.78])

# XDocument

The XDocument is a replacement of the XmlDocument object from the pre-.NET 3.5 world; it is easier to work with in dealing with XML documents. The XDocument object works with the other new objects in this space, such as the XNamespace, XComment, XElement, and XAttribute objects.

One of the more important members of the XDocument object is the Load() method:

```
XDocument xdoc = XDocument.Load(@"C:\Hamlet.xml");
```

This operation will load the Hamlet.xml contents as an in-memory XDocument object. You can also pass a TextReader or XmlReader object into the Load() method. From here, you are able to programmatically work with the XML:

```
XDocument xdoc = XDocument.Load(@"C:\Hamlet.xml");
Console.WriteLine(xdoc.Root.Name.ToString());
Console.WriteLine(xdoc.Root.HasAttributes.ToString());
```

code download ConsoleApplication1.sln

This produces the following results:

```
PLAY
False
```

Another important member to be aware of is the Save() method, which, like the Load() method, allows you to save to a physical disk location or to a TextWriter or XmlWriter object:

```
XDocument xdoc = XDocument.Load(@"C:\Hamlet.xml");

xdoc.Save(@"C:\CopyOfHamlet.xml");
```