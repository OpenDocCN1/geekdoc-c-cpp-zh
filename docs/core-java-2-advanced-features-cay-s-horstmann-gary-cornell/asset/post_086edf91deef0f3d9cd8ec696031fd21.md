
A better approach is to build up a DOM tree with the contents of the document and then write out the tree contents. The following sections discuss the details.

## 3.7.1 Documents without Namespaces

To build a DOM tree, you start out with an empty document. You can get an empty document by calling the `newDocument` method of the `DocumentBuilder` class:

```
Document doc = builder.newDocument();
```

Use the `createElement` method of the Document class to construct the elements of your document:

```
Element rootElement = doc.createElement(rootName);
Element childElement = doc.createElement(childName);
```

Use the createTextNode method to construct text nodes:

```
Text textNode = doc.createTextNode(textContents);
```

Add the root element to the document, and add the child nodes to their parents:

```
doc.appendChild(rootElement);
rootElement.appendChild(childElement);
childElement.appendChild(textNode);
```

As you build up the DOM tree, you may also need to set element attributes. Simply call the setAttribute method of the Element class:

```
rootElement.setAttribute(name, value);
```

## 3.7.2 Documents with Namespaces

If you use namespaces, the procedure for creating a document is slightly different.

First, set the builder factory to be namespace-aware, then create the builder:

```
DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
factory.setNamespaceAware(true);
builder = factory.newDocumentBuilder();
```

Then use the `createElementNS` instead of `createElement` to create any nodes:

```
String namespace = "http://www.w3.org/2000/svg";
Element rootElement = doc.createElementNS(namespace, "svg");
```

If your node has a qualified name with a namespace prefix, then any necessary xml-ns-prefixed attributes are created automatically. For example, if you need SVG inside XHTML, you can construct an element like this:

```
Element svgElement = doc.createElementNS(namespace, "svg:svg");
```

When the element is written, it turns into

```xml
<svg:svg xmlns:svg="http://www.w3.org/2000/svg">
```

If you need to set element attributes whose names are in a namespace, use the setAttributeNS method of the Element class:

```java
rootElement.setAttributeNS(namespace, qualifiedName, value);
```

## 3.7.3 Writing Documents

Somewhat curiously, it is not so easy to write a DOM tree to an output stream. The easiest approach is to use the Extensible Stylesheet Language Transformations (XSLT) API. For more information about XSLT, turn to Section 3.8, “XSL Transformations,” on p. 222. Right now, consider the code that follows a magic incantation to produce XML output.

We apply the do-nothing transformation to the document and capture its output. To include a DOCTYPE node in the output, we also need to set the SYSTEM and PUBLIC identifiers as output properties.

```java
// construct the do-nothing transformation
Transformer t = TransformerFactory.newInstance().newTransformer();
// set output properties to get a DOCTYPE node
t.setOutputProperty(OutputKeys.DOCTYPE_SYSTEM, systemIdentifier);
t.setOutputProperty(OutputKeys.DOCTYPE_PUBLIC, publicIdentifier);
// set indentation
t.setOutputProperty(OutputKeys.INDENT, "yes");
t.setOutputProperty(OutputKeys.METHOD, "xml");
t.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "2");
// apply the do-nothing transformation and send the output to a file
t.transform(new DOMSource(doc), new StreamResult(new FileOutputStream(file)));
```

Another approach is to use the LSSerializer interface. To get an instance, you have to use the following magic incantation:

```java
DOMImplementation impl = doc.getImplementation();
DOMImplementationLS implLS = (DOMImplementationLS) impl.getFeature("LS", "3.0");
LSSerializer ser = implLS.createLSSerializer();
```

If you want spaces and line breaks, set this flag:

```java
ser.getDomConfig().setParameter("format-pretty-print", true);
```

Then it’s simple enough to convert a document to a string:

```java
String str = ser.writeToString(doc);
```

If you want to write the output directly to a file, you need an LSOutput:

```java
LSOutput out = implLS.createLSOutput();
out.setEncoding("UTF-8");
out.setByteStream(Files.newOutputStream(path));
ser.write(doc, out);
```

## 3.7.4 An Example: Generating an SVG File

Listing 3.10 on p. 215 is a typical program that produces XML output. The program draws a modernist painting—a random set of colored rectangles (see Figure 3.6). To save a masterpiece, we use the Scalable Vector Graphics (SVG) format. SVG is an XML format to describe complex graphics in a device-independent fashion. You can find more information about SVG at www.w3.org/Graphics/SVG. To view SVG files, simply use any modern browser.

![](img/7dd923a566750151a3aab0dacd0cdaa5_231_0.png)

*Figure 3.6 Generating modern art*

We don’t need to go into details about SVG; for our purposes, we just need to know how to express a set of colored rectangles. Here is a sample:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 20000802//EN"
   "http://www.w3.org/TR/2000/CR-SVG-20000802/DTD/svg-20000802.dtd">
<svg xmlns="http://www.w3.org/2000/svg" width="300" height="150">
  <rect x="231" y="61" width="9" height="12" fill="#6e4a13"/>
  <rect x="107" y="106" width="56" height="5" fill="#4006e"/>

</svg>
```

As you can see, each rectangle is described as a rect node. The position, width, height, and fill color are attributes. The fill color is an RGB value in hexadecimal.

**NOTE:** SVG uses attributes heavily. In fact, some attributes are quite complex. For example, here is a path element:

```
<path d="M 100 100 L 300 100 L 200 300 z">
```

The M denotes a "moveto" command, L is "lineto," and z is "closepath" (!). Apparently, the designers of this data format didn't have much confidence in using XML for structured data. In your own XML formats, you might want to use elements instead of complex attributes.

### javax.xml.parsers.DocumentBuilder 1.4

- `Document newDocument()`
  returns an empty document.

### org.w3c.dom.Document 1.4

- `Element createElement(String name)`
- `Element createElementNS(String uri, String qname)`
  creates an element with the given name.
- `Text createTextNode(String data)`
  creates a text node with the given data.

### org.w3c.dom.Node 1.4

- `Node appendChild(Node child)`
  appends a node to the list of children of this node. Returns the appended node.

### org.w3c.dom.Element 1.4

- `void setAttribute(String name, String value)`
- `void setAttributeNS(String uri, String qname, String value)`
  sets the attribute with the given name to the given value.

Parameters:

| Parameter | Description |
| --- | --- |
| uri | The URI of the namespace, or null |
| qname | The qualified name. If it has an alias prefix, then uri must not be null. |
| value | The attribute value |

### javax.xml.transform.TransformerFactory 1.4

- `static TransformerFactory newInstance()`
  returns an instance of the TransformerFactory class.
- `Transformer newTransformer()`
  returns an instance of the Transformer class that carries out an identity (do-nothing) transformation.

### javax.xml.transform.Transformer 1.4

- `void setOutputProperty(String name, String value)`
  sets an output property. See www.w3.org/TR/xsl#output for a listing of the standard output properties. The most useful ones are shown here:
  - `doctype-public` The public ID to be used in the DOCTYPE declaration
  - `doctype-system` The system ID to be used in the DOCTYPE declaration
  - `indent` "yes" or "no"
  - `method` "xml", "html", "text", or a custom string
- `void transform(Source from, Result to)`
  transforms an XML document.

### javax.xml.transform.dom.DOMSource 1.4

- `DOMSource(Node n)`
  constructs a source from the given node. Usually, n is a document node.

### javax.xml.transform.stream.StreamResult 1.4

- `StreamResult(File f)`
- `StreamResult(OutputStream out)`
- `StreamResult(Writer out)`
- `StreamResult(String systemID)`
  constructs a stream result from a file, stream, writer, or system ID (usually a relative or absolute URL).
