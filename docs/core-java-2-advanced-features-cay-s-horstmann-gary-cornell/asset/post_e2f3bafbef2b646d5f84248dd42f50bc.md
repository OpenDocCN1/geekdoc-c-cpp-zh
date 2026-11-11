
The header can be followed by a *document type definition* (DTD), such as

```xml
<!DOCTYPE web-app PUBLIC
    "-//Sun Microsystems, Inc.//DTD Web Application 2.2//EN"
    "http://java.sun.com/j2ee/dtds/web-app_2.2.dtd">
```

DTDs are an important mechanism to ensure the correctness of a document, but they are not required. We will discuss them later in this chapter.

Finally, the body of the XML document contains the *root element*, which can contain other elements. For example,

```xml
<?xml version="1.0"?>
<!DOCTYPE configuration . . . >
<configuration>
    <title>
        <font>
            <name>Helvetica</name>
            <size>36</size>
        </font>
    </title>
    . . .
</configuration>
```

An element can contain child elements, text, or both. In the preceding example, the font element has two child elements, name and size. The name element contains the text "Helvetica".

![](img/7dd923a566750151a3aab0dacd0cdaa5_167_0.png)

> **TIP:** It is best to structure your XML documents so that an element contains *either* child elements or text. In other words, you should avoid situations such as
>
> ```xml
> <font>
>     Helvetica
>     <size>36</size>
> </font>
> ```
>
> This is called *mixed content* in the XML specification. As you will see later in this chapter, you can simplify parsing if you avoid mixed content.

XML elements can contain attributes, such as

```xml
<size unit="pt">36</size>
```

There is some disagreement among XML designers about when to use elements and when to use attributes. For example, it would seem easier to describe a font as

```xml
<font name="Helvetica" size="36"/>
```

than

```xml
<font>
    <name>Helvetica</name>
    <size>36</size>
</font>
```

However, attributes are much less flexible. Suppose you want to add units to the size value. If you use attributes, you will have to add the unit to the attribute value:

```xml
<font name="Helvetica" size="36 pt"/>
```

Ugh! Now you have to parse the string “36 pt”, just the kind of hassle that XML was designed to avoid. Adding an attribute to the size element is much cleaner:

```xml
<font>
    <name>Helvetica</name>
    <size unit="pt">36</size>
</font>
```

A commonly used rule of thumb is that attributes should be used only to modify the interpretation of a value, not to specify values. If you find yourself engaged in metaphysical discussions about whether a particular setting is a modification of the interpretation of a value or not, just say “no” to attributes and use elements throughout. Many useful XML documents don’t use attributes at all.

> **NOTE:** In HTML, the rule for attribute usage is simple: If it isn’t displayed on the web page, it’s an attribute. For example, consider the hyperlink
>
> ```html
> <a href="http://java.sun.com">Java Technology</a>
> ```
>
> The string Java Technology is displayed on the web page, but the URL of the link is not a part of the displayed page. However, the rule isn’t all that helpful for most XML files because the data in an XML file aren’t normally meant to be viewed by humans.

Elements and text are the “bread and butter” of XML documents. Here are a few other markup instructions that you might encounter:

- *Character references* have the form `&#decimalValue;` or `&#xhexValue;`. For example, the é character can be denoted with either of the following:

  ```text
  &#233; &#xE9;
  ```

- *Entity references* have the form `&name;`. The entity references

  ```text
  &lt; &gt; &amp; &quot; &apos;
  ```

  have predefined meanings: the less-than, greater-than, ampersand, quotation mark, and apostrophe characters. You can define other entity references in a DTD.

- *CDATA sections* are delimited by `<![CDATA[ ... ]]>`. They are a special form of character data. You can use them to include strings that contain characters such as `<` and `&` without having them interpreted as markup, for example:

  ```text
  <![CDATA[ & are my favorite delimiters]]>
  ```

  CDATA sections cannot contain the string `]]>`. Use this feature with caution! It is too often used as a back door for smuggling legacy data into XML documents.

- *Processing instructions* are instructions for applications that process XML documents. They are delimited by `<?` and `?>`, for example

  ```xml
  <?xml-stylesheet href="mystyle.css" type="text/css"?>
  ```

  Every XML document starts with a processing instruction

  ```xml
  <?xml version="1.0"?>
  ```

- *Comments* are delimited by `<!--` and `-->`, for example

  ```xml
  <!-- This is a comment. -->
  ```

  Comments should not contain the string `--`. Comments should only be information for human readers. They should never contain hidden commands; use processing instructions for commands.

## 3.2 Parsing an XML Document

To process an XML document, you need to *parse* it. A parser is a program that reads a file, confirms that the file has the correct format, breaks it up into the constituent elements, and lets a programmer access those elements. The Java library supplies two kinds of XML parsers:

- Tree parsers, such as the Document Object Model (DOM) parser, that read an XML document into a tree structure.
- Streaming parsers, such as the Simple API for XML (SAX) parser, that generate events as they read an XML document.

The DOM parser is easier to use for most purposes, and we explain it first. You may consider a streaming parser if you process very long documents whose tree structures would use up a lot of memory, or if you are only interested in a few elements and don’t care about their context. For more information, see Section 3.6, “Streaming Parsers,” on p. 199.

The DOM parser interface is standardized by the World Wide Web Consortium (W3C). The `org.w3c.dom` package contains the definitions of interface types such as `Document` and `Element`. Different suppliers, such as the Apache Organization and IBM, have written DOM parsers whose classes implement these interfaces. The Java API for XML Processing (JAXP) library actually makes it possible to plug in any of these parsers. But the JDK also comes with a DOM parser that is derived from the Apache parser.

To read an XML document, you need a `DocumentBuilder` object that you get from a `DocumentBuilderFactory` like this:

```java
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
```

You can now read a document from a file:

```java
File f = ...;
Document doc = builder.parse(f);
```

Alternatively, you can use a URL:

```java
URL u = ...;
Document doc = builder.parse(u);
```

You can even specify an arbitrary input stream:

```java
InputStream in = ...;
Document doc = builder.parse(in);
```

> **NOTE:** If you use an input stream as an input source, the parser will not be able to locate other files that are referenced relative to the location of the document, such as a DTD in the same directory. You can install an “entity resolver” to overcome that problem. See `www.xml.com/pub/a/2004/03/03/catalogs.html` or `www.ibiblio.org/developer/xml/1/library/x-nxd3.html` for more information.

The Document object is an in-memory representation of the tree structure of the XML document. It is composed of objects whose classes implement the Node interface and its various subinterfaces. Figure 3.1 shows the inheritance hierarchy of the subinterfaces.

Start analyzing the contents of a document by calling the `getDocumentElement` method. It returns the root element.

```java
Element root = doc.getDocumentElement();
```

![](img/7dd923a566750151a3aab0dacd0cdaa5_171_0.png)

Figure 3.1 The Node interface and its subinterfaces

For example, if you are processing a document

```xml
<?xml version="1.0"?>
<font>
   . . .
</font>
```

then calling `getDocumentElement` returns the font element.

The `getTagName` method returns the tag name of an element. In the preceding example, `root.getTagName()` returns the string "font".

To get the element's children (which may be subelements, text, comments, or other nodes), use the `getChildNodes` method. That method returns a collection of type `NodeList`. That type was standardized before the standard Java collections, so it has a different access protocol. The `item` method gets the item with a given index, and the `getLength` method gives the total count of the items. Therefore, you can enumerate all children like this:

```java
NodeList children = root.getChildNodes();
for (int i = 0; i < children.getLength(); i++)
{
    Node child = children.item(i);
    . . .
}
```
