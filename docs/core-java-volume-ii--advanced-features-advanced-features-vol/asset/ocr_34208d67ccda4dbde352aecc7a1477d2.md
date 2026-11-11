Then the first child and the grandchildren are part of the second namespace. This simple mechanism works well if you need only a single namespace or if the namespaces are naturally nested. Otherwise, you will want to use a second mechanism that has no analog in Java. You can have a prefix for a namespace—a short identifier that you choose for a particular document. Here is a typical example—the xsd prefix in an XML Schema file:

```
```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <xsd:element name="config"/>
  . . .
</xsd:schema>
```
```

The attribute

```
```
xmlns:prefix="namespaceURI"
```
```

defines a namespace and a prefix. In our example, the prefix is the string xsd. Thus, xsd:schema really means schema in the namespace http://www.w3.org/2001/XMLSchema.

> > **NOTE:** Only child elements inherit the namespace of their parent. Attributes without an explicit prefix are never part of a namespace. Consider this contrived example:
> >
> > ```xml
> > <configuration xmlns="http://www.horstmann.com/corejava"
> >     xmlns:si="http://www.bipm.fr/enus/3_SI/si.html">
> >   <size value="210" si:unit="mm"/>
> >   . . .
> > </configuration>
> > ```
> >
> > In this example, the elements configuration and size are part of the namespace with URI http://www.horstmann.com/corejava. The attribute si:unit is part of the namespace with URI http://www.bipm.fr/enus/3_SI/si.html. However, the attribute value is not part of any namespace.

You can control how the parser deals with namespaces. By default, the DOM parser of the Java XML library is not namespace-aware.

To turn on namespace handling, call the setNamespaceAware method of the DocumentBuilderFactory:

```
```java
factory.setNamespaceAware(true);
```
```

Now, all builders the factory produces support namespaces. Each node has three properties:

+   - The *qualified name*, with a prefix, returned by `getNodeName`, `getTagName`, and so on
+   - The namespace URI, returned by the `getNamespaceURI` method