> **NOTE:** Only child elements inherit the namespace of their parent. Attributes without an explicit prefix are never part of a namespace. Consider this contrived example:

```
```xml
<configuration xmlns="http://www.horstmann.com/corejava"
    xmlns:si="http://www.bipm.fr/enus/3/SI/si.html">
    <size value="210" si:unit="mm"/>
    ...
</configuration>
```
```

In this example, the elements `configuration` and `size` are part of the namespace with URI `http://www.horstmann.com/corejava`. The attribute `si:unit` is part of the namespace with URI `http://www.bipm.fr/enus/3/SI/si.html`. However, the attribute `value` is not part of any namespace.

You can control how the parser deals with namespaces. By default, the DOM parser of the Java XML library is not namespace-aware.

To turn on namespace handling, call the `setNamespacesAware` method of the `DocumentBuilderFactory`:

`factory.setNamespacesAware(true);`

Now, all builders the factory produces support namespaces. Each node has three properties:

+   - The *qualified name*, with a prefix, returned by `getNodeName`, `getTagName`, and so on
+   - The namespace URI, returned by the `getNamespaceURI` method
+   - The *local name*, without a prefix or a namespace, returned by the `getLocalName` method

Here is an example. Suppose the parser sees the following element:

```
```xml
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema">
```
```

It then reports the following:

+   - Qualified name = `xsd:schema`
+   - Namespace URI = `http://www.w3.org/2001/XMLSchema`
+   - Local name = `schema`

> **NOTE:** If namespace awareness is turned off, `getNamespaceURI` and `getLocalName` return null.