
![](img/43c5f409f9b17790a628c4b4df854b61_684_0.png)

## 20 XML in C#

| If you need information on: | See page: |
|---|---:|
| Introduction to XML | 644 |
| Creating XML Files using Visual Studio 2008 | 647 |
| XML Namespaces | 648 |
| XML Classes | 649 |
| XmlTextReader | 649 |
| XmlTextWriter | 652 |
| XmlDocument | 654 |
| Application of XML Classes | 657 |
| The OnLoad Event | 657 |
| The Create XML using XmlTextWriter Button | 659 |
| The Create XML using XmlDocument Button | 666 |
| XSD | 669 |
| XSLT | 672 |
| XPath | 674 |
| ADO.NET and XML | 675 |

### Introduction to XML

A markup language is used to tell Web browsers how to display a document. Every markup language consists of certain semantics, which decide how the text in a document should be structured. Two widely used markup languages are HyperText Markup Language (HTML) and Extensible Markup Language (XML), which are derived from Standard Generalized Markup Language (SGML). HTML is a language that uses predefined tags to define the structure of a document. On the other hand, XML is a language that is used to create custom tags to describe data. XML can also be used as an exchange format to transfer data between similar applications.

Due to a well-formed structural representation of data as well as user-friendly tags and attributes, XML is an integral part of .NET Framework. Microsoft has introduced a new suite of XML application programming interfaces that are built on industry standards, such as XPath, XML Schema Definition (XSD), and Extensible Stylesheet Language Transformations (XSLT). XML is a core part in .NET because it is used to represent data in technologies, such as ASP.NET and Web Services.

To work with an XML document (or file), .NET provides five namespaces, namely System.Xml, System.Xml.Schema, System.Xml.Serialization, System.Xml.XPath, and System.Xml.Xsl. The System.Xml namespace contains major XML classes, such as XmlTextReader, XmlTextWriter, and XmlDocument, to read and write XML documents.

In this chapter, we learn about the XML language and its structural representation. We also learn how to create XML files using Visual Studio 2008. Next, we explore the XmlTextReader, XmlTextWriter, and XmlDocument classes that help in creating and reading an XML document. In addition, we develop the My XML Manager application by using these classes. After that, the chapter discusses XSD, XSLT, and XPath with the help of some programs. Towards the end, we learn how to convert an ADO.NET dataset to XML by using the XmlDataDocument class.

Let's start the chapter with the introduction to XML.

When we save enterprise data in a document, we always try to structure the data in a certain way that can be understood later by another user. Therefore, we choose a format that is reliable and easily understood by other users. In this scenario, XML is used to provide a structured way to format the content of the document using user-friendly tags. Each XML document starts with an XML tag that holds the version of XML along with the encoding type it provides. Similar to SGML, XML also has the starting tag and the ending tag. Consider an example of Library Management System to understand the structure of an XML document. Listing 20.1 shows the format of library data using XML:

**Listing 20.1: Showing the XML Format of a Library Data**

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Library>
    <Book>
        <ID>12341</ID>
        <ISBN>100-000-X</ISBN>
        <Title>TCP/IP Protocol Suite</Title>
        <Author>Behrouz A. Forouzan</Author>
    </Book>
    <Book>
        <ID>12342</ID>
        <ISBN>200-000-X</ISBN>
        <Title>Data Communications and Networking</Title>
        <Author>Behrouz A. Forouzan, Sophia Chung Fegan</Author>
    </Book>
</Library>
```

In Listing 20.1, the main starting and ending tags are `<Library>` and `</Library>`, respectively. The preceding XML document also holds the information regarding the books in Library Management System. The information about each book is enclosed in the `<Book>` and `</Book>` tags.

Therefore, the structured representation of data in an XML document helps in understanding what information the document holds. Next, let’s learn about elements, tags, and attributes in XML.

### Elements

An element is the main building block of an XML document. It refers to a structural component, which is used to store data. In Listing 20.1, Library, Book, ID, ISBN, Title, and Author are the elements of the XML document. These elements are enclosed within the two angular brackets (`<` and `>`) that represent tags. Therefore, we can say that an element is a user-defined entity that can be repeated multiple times and has a meaning specific to the document.

### Tags

XML allows us to design our own tags for writing a structured document. Tags are nothing but the elements enclosed by the angular brackets. However, tags have certain restrictions, which are given as follows:

- XML tags are case sensitive. Therefore, we cannot use `<Book>` and `<book>` to refer to the same portion of the text. In this case, both have different meanings to the XML parser, which is used by the programming languages that support XML.
- We cannot add whitespace in the name of a tag. For example, if we declare a tag, such as `<Book Name>`, then Book will be considered as the name of the tag and Name will be considered as an attribute.
- Each document must have a root tag and all the other tags must be nested in the root tag. In Listing 20.1, `<Library>` represents the root tag and all the `<Book>` tags are nested in the root tag `<Library>`.
- Each start tag must have an end tag; otherwise, the document will throw an error during parsing.
- The XML parser does not understand some of the special characters, such as angular brackets (`<` and `>`) and ampersand (`&`), in the text part. Therefore, if we want to use the special characters in the text part, then we should use the equivalent forms of those special characters, which will be converted by the XML parser. For instance, we can use `&amp;` for ampersand, `&lt;` for `<`, and `&gt;` for `>`.

### Attributes

Attributes provide some extra information about an element. They are defined inside the start tag of an element. An attribute has a name/value format, which means that each name of the attribute is assigned a relative value. For example, we can add the ID sub-tag as an attribute in the `<Book>` tag. Therefore, in this case, the name-value pair would be as follows:

```xml
<Book ID="12341"></Book>
```

In this way, the whole XML document can be reframed, as shown in Listing 20.2:

**Listing 20.2: Showing the Modified XML Format after Introducing Attributes**

```xml
<Library>
    <Book ID="12341">
        <ISBN>100-000-X</ISBN>
        <Title>TCP/IP Protocol Suite</Title>
        <Author>Behrouz A. Forouzan</Author>
    </Book>
    <Book ID="12342">
        <ISBN>200-000-X</ISBN>
        <Title>Data Communications and Networking</Title>
        <Author>Behrouz A. Forouzan, Sophia Chung Fegan</Author>
    </Book>
</Library>
```

Adding attributes in a tag is relatively easy in markup languages, such as HTML and Extensible Hypertext Markup Language (XHTML). However, adding attributes in an element is much more stringent in case of XML. Therefore, to add attributes in an element, we need to maintain the following syntactical rules:

- Attribute always comes in a name/value pair, where value cannot be blank.
- Value must always be enclosed in quotes.
- If an element is empty, then the element can be closed by using a forward slash (/). For example, if the Book element is empty, then we can write `<Book ID="12341"/>`.

### Document Type Definition

Document Type Definition (DTD) is a well-defined standard in SGML that helps in creating a protocol following which an XML document is structured. As XML is the only meta-language that the system understands for exchanging two XML documents, we must have a standard protocol that the XML document should support. Therefore, DTD provides a standard protocol to exchange data between two XML documents. An XML document containing the DTD is considered as a valid document and is called well-defined only if the start and end tags of the root element in the document do not reside inside other elements. In addition to this, all the other tags are nested within each other in a correct manner. We use the DOCTYPE keyword to define a DTD. The DOCTYPE declaration is placed underneath the XML declaration tag.

We can define DTD either in an XML document or in some text file and then save it with an extension .dtd. The former approach is known as an inline definition or internal DTD and the latter approach is known as external definition or external DTD. Internal DTD is helpful where an XML needs to deal with a restricted number of elements. Listing 20.3 shows the definition of an internal DTD:

**Listing 20.3: Showing the Definition of an Internal DTD**

```xml
<?xml version="1.0"?>
<!DOCTYPE documentelement [definition]>
```

External DTD is helpful where it is required to make a communication between two XML documents or to transmit one XML document to other systems. In this case, external DTD minimizes the communication overhead by providing a separate file for DTD that two communicating systems can refer to. Listing 20.4 shows the definition of an external DTD:

**Listing 20.4: Showing the Definition of an External DTD**

```xml
<?xml version="1.0"?>
<!DOCTYPE documentElement SYSTEM "documentelement.dtd">
```

Let’s modify the XML document for Library Management System (Listing 20.2) to implement the internal DTD for its elements. Listing 20.5 shows the XML document after implementing internal DTD.

**Listing 20.5: Implementing Internal DTD in the XML Document**

```xml
<?xml version="1.0"?>
<!DOCTYPE LIBRARY [
<!ELEMENT LIBRARY (BOOK)+>
<!ELEMENT book (title,author)>
<!ELEMENT title (#PCDATA)>
<!ELEMENT author (#PCDATA)>
]>
```

In Listing 20.5, the + sign refers to the minimum of one occurrence of the element BOOK.

In the next section, let’s learn how to create XML files using Visual Studio 2008.
