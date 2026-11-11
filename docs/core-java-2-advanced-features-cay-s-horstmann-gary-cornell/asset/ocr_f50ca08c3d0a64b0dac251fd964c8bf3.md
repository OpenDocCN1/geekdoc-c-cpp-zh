# 3.7.5 Writing an XML Document with StAX

In the preceding section, you saw how to produce an XML document by writing a DOM tree. If you have no other use for the DOM tree, that approach is not very efficient.

The StAX API lets you write an XML tree directly. Construct an `XMLStreamWriter` from an `OutputStream`:

```
```java
XMLOutputFactory factory = XMLOutputFactory.newInstance();
XMLStreamWriter writer = factory.createXMLStreamWriter(out);
```
```

To produce the XML header, call

```
```java
writer.writeStartDocument()
```
```

Then call

```
```java
writer.writeStartElement(name);
```
```

Add attributes by calling

```
```java
writer.writeAttribute(name, value);
```
```

Now you can add child elements by calling `writeStartElement` again, or write characters with

```
```java
writer.writeCharacters(text);
```
```

When you have written all child nodes, call

```
```java
writer.writeEndElement();
```
```

This causes the current element to be closed.

To write an element without children (such as `<img ... />`), use the call

```
```java
writer.writeEmptyElement(name);
```
```

Finally, at the end of the document, call

```
```java
writer.writeEndDocument();
```
```

This call closes any open elements.

You still need to close the `XMLStreamWriter`, and you need to do it manually since the `XMLStreamWriter` interface does not extend the `AutoCloseable` interface.

As with the DOM/XSLT approach, you don't have to worry about escaping characters in attribute values and character data. However, it is possible to produce malformed XML, such as a document with multiple root nodes. Also, the current version of StAX has no support for producing indented output.