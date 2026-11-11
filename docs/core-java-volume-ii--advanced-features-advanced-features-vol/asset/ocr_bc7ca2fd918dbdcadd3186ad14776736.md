+   **org.xml.sax.Attributes** 1.4
+   
+   - `int getLength()`
+     returns the number of attributes stored in this attribute collection.
+   - `String getLocalName(int index)`
+     returns the local name (without prefix) of the attribute with the given index,
+     or the empty string if the parser is not namespace-aware.
+   - `String getURI(int index)`
+     returns the namespace URI of the attribute with the given index, or the empty
+     string if the node is not part of a namespace or if the parser is not namespace-
+     aware.
+   - `String getQName(int index)`
+     returns the qualified name (with prefix) of the attribute with the given index,
+     or the empty string if the qualified name is not reported by the parser.
+   - `String getValue(int index)`
+   - `String getValue(String qname)`
+   - `String getValue(String uri, String lname)`
+     returns the attribute value from a given index, qualified name, or namespace
+     URI + local name. Returns null if the value doesn't exist.

# 3.7.2 Using the StAX Parser

The StAX parser is a “pull parser.” Instead of installing an event handler, you simply iterate through the events, using this basic loop:

```
~~~
InputStream in = url.openStream();
XMLInputFactory factory = XMLInputFactory.newInstance();
XMLStreamReader parser = factory.createXMLStreamReader(in);
while (parser.hasNext())
{
    int event = parser.next();
    Call parser methods to obtain event details
}
~~~
```

For example, when parsing the fragment

```
~~~
<font>
    <name>Helvetica</name>
    <size units="pt">36</size>
</font>
~~~
```

the parser yields the following events: