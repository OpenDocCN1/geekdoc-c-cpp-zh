# 6. XML Namespaces

A XML namespace allows to qualify an element. XML namespaces uses URI, which is associated with a prefix for the namespace. A namespace is defined using an xmlns declaration, followed by the prefix, which is equal to a URI that uniquely identifies the namespace.

```
```
xmlns:movie="http://www.enjoypoint.com/movies">
```
```

By adding this namespace definition as an attribute to a tag, one can use the prefix movie in that tag, and any tags it contains, to fully qualify elements:

```
```
<movie:film-types xmlns:movie="http://www.enjoypoint.com/movies">

<movie:film-type>Drama</movie:film-type>

<movie:film-type>Romance</movie:film-type>

</movie:film-types>
```
```

Parsers can now recognise both meanings of "film type" and handle them accordingly.

# 17.3 Reading and Writing XML Files

# .NET classes for reading and writing XML files

+   1. **XmlTextReader** : The XmlTextReader class is just one of the methods of reading XML files. It approaches an XML file in a similar way to a DataReader, in that the document is read element by element, making decisions as reading proceeds. It's by far the easiest class to use to parse an XML file quickly.
+   2. **XmlTextWriter** : Similarly, the XmlTextWriter class provides a means of writing XML files line by line.
+   3. **XmlValidatingReader** : XmlValidatingReader is used to validate an XML file against a schema file.

+   - **Reading an XML File In .NET**

**XmlTextReader.** XmlTextReader is based upon the XmlReader class, specially designed to read byte streams, making it suitable for XML files that are to be located on disk, on a network, or in a stream.

First create a new instance of the class.

The **constructor takes the** location of the XML file that it will read.

```
```
// file

XmlTextReader reader = new XmlTextReader("first.xml");

// url
```
```