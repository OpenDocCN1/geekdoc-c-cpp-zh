# 154 SQL Server Database Programming with C#

![](bbox=[0.109, 0.093, 0.891, 0.303])

FIGURE 4.45 The LINQ to XML class hierarchy.

# 4.8.1 LINQ to XML Class HIERARCHY

First let's have a global picture about the LINQ to XML Class Hierarchy that is shown in Figure 4.45. The following important points should be noticed when watching this class hierarchy:

+   1. XElement is low in the class hierarchy, it is the fundamental class in LINQ to XML. XML trees are generally made up of a tree of XElements. XAttributes are name/value pairs associated with an XElement. XDocuments are created only if necessary, such to hold a DFT or top-level XML processing instruction (ProcessingInstruction). All other XNodes can be leaf nodes under an XElement, or possibly an XDocument (if they exist at the root).
2. XAttribute and XNode are derived from a common base class XObject. XAttributes are not XNodes because XML attributes are really name value pairs associated with an XML element not nodes in the XML tree. This contrast with W3C DOM.
3. Text and XData are exposed in this version of LINQ to XML, but as discussed above, it is best to think of them as a semi-hidden implementation except when exposing text is necessary. As a user, you can get back the value of the text within an element or attribute as a string or other simple value.
4. The only Node that can have children is XContainer, meaning either an XDocument or XElement. An XDocument can contain an XElement (the root element), an XDeclaration, or an ProcessingInstruction. An XElement can contain another XElement, an Attribute, and text (which can be passed in a variety of formats, but will be represented in the XML tree as text)

In addition to this class hierarchy, other important components aligned in XML also play key roles in LINQ to XML. One of them is the XML names.

XML names, often a complex subject in XML programming APIs, are represented simply in LINQ to XML. An XML name is represented by an XNamespace object (which encapsulates the XML namespace URI) and a local name. An XML namespace serves the same purpose that a namespace does in your .NET Framework-based programs, allowing you to uniquely qualify the names of your classes. This ensures that you don't run into a name conflict with other users or built-in names. When you have identified an XML namespace, you can choose a local name that needs to be unique only within your identified namespace.