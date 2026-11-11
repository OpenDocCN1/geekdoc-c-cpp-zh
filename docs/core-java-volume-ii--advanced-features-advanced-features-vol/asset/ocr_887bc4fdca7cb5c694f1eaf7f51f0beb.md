+   1. START_ELEMENT, element name: font
+   2. CHARACTERS, content: white space
+   3. START_ELEMENT, element name: name
+   4. CHARACTERS, content: Helvetica
+   5. END_ELEMENT, element name: name
+   6. CHARACTERS, content: white space
+   7. START_ELEMENT, element name: size
+   8. CHARACTERS, content: 36
+   9. END_ELEMENT, element name: size
+   10. CHARACTERS, content: white space
+   11. END_ELEMENT, element name: font

To analyze the attribute values, call the appropriate methods of the XMLStreamReader class. For example,

```
```java
String units = parser.getAttributeValue(null, "units");
```
```

gets the units attribute of the current element.

By default, namespace processing is enabled. You can deactivate it by modifying the factory:

```
```java
XMLInputFactory factory = XMLInputFactory.newInstance();
factory.setProperty(XMLInputFactory.IS_NAMESPACE_AWARE, false);
```
```

Listing 3.8 contains the code for the web crawler program implemented with the StAX parser. As you can see, the code is simpler than the equivalent SAX code because you don't have to worry about event handling.

# **Listing 3.8** stax/StAXTest.java

```
```java
1 package stax;
2
3 import java.io.*;
4 import java.net.*;
5 import javax.xml.stream.*;
6
7 /**
8  * This program demonstrates how to use a StAX parser. The program prints all
9  * hyperlinks of an HTML web page. <br>
10 * Usage: java stax.StAXTest URL
11 * @author Cay Horstmann
12 * @version 1.1 2018-05-01
13 */
```
```