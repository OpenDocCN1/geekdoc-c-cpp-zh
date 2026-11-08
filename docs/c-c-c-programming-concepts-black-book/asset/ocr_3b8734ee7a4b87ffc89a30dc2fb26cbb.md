```
```xml
<Author>Behrouz A. Farhouzen, Sophia Chung Fegan</Author>
</Book>
</Library>
```
```

Adding attributes in a tag is relatively easy in markup languages, such as HTML and Extensible Hypertext Markup Language (XHTML). However, adding attributes in an element is much more stringent in case of XML. Therefore, to add attributes in an element, we need to maintain the following syntactical rules:

+   - Attribute always comes in a name/value pair, where value cannot be blank.
+   - Value must always be embraced with the quotes.
+   - If an element is empty, then the element can be closed by using a forward slash (/). For example, if the Book element is empty, then we can write `<Book ID ="12341"/>`.

# Document Type Definition

Document Type Definition (DTD) is a well-defined standard in SGML that helps in creating a protocol following which an XML document is structured. As XML is the only meta-language that the system understands for exchanging two XML documents, we must have a standard protocol that the XML document should support. Therefore, DTD provides a standard protocol to exchange data between two XML documents. An XML document containing the DTD is considered as a valid document and is called well defined only if the start and end tags of the root element in the document does not reside inside other elements. In addition to this, all the other tags are nested within each other in a correct manner. We use the DOCTYPE keyword to define a DTD. The DOCTYPE declaration is placed underneath the XML declaration tag.

We can define DTD either in an XML document or in some text file and then save it with an extension .dtd. The former approach is known as an inline definition or internal DTD and the later approach is known as external definition or external DTD. Internal DTD is helpful where an XML needs to deal with a restricted number of elements. Listing 20.3 shows the definition of an internal DTD:

**Listing 20.3:** Showing the Definition of an Internal DTD

```
```xml
<?xml version="1.0"?>
<!DOCTYPE documentelement [definition]>
```
```

External DTD is helpful where it is required to make a communication between two XML documents or to transmit one XML document to other systems. In this case, external DTD minimizes the communication overhead by providing a separate file for DTD that two communicating systems can refer. Listing 20.4 shows the definition of an external DTD:

**Listing 20.4:** Showing the Definition of an External DTD

```
```xml
<?xml version="1.0"?>
<!DOCTYPE documentElement SYSTEM "documentelement.dtd">
```
```

Let’s modify the XML document for Library Management System (Listing 20.2) to implement the internal DTD for its elements. Listing 20.5 shows the XML document after implementing internal DTD.

**Listing 20.5:** Implementing Internal DTD in the XML Document

```
```xml
<?xml version="1.0"?>
<!DOCTYPE LIBRARY [
<!ELEMENT LIBRARY (BOOK)+>
<!ELEMENT book (title,author)>
<!ELEMENT title (#CDATA)>
<!ELEMENT author (#CDATA)>
]>
```
```

In Listing 20.5, the + sign refers to the minimum of one occurrence of the element BOOK.

In the next section, let’s learn how to create XML files using Visual Studio 2008.