
It is simple to generate XSL transformations in the Java platform. Set up a transformer factory for each stylesheet. Then, get a transformer object and tell it to transform a source to a result:

```java
File styleSheet = new File(filename);
StreamSource styleSource = new StreamSource(styleSheet);
Transformer t = TransformerFactory.newInstance().newTransformer(styleSource);
t.transform(source, result);
```

The parameters of the transform method are objects of classes that implement the Source and Result interfaces. Several classes implement the Source interface:

- DOMSource
- SAXSource
- StreamSource

You can construct a StreamSource from a file, stream, reader, or URL, and a DOMSource from the node of a DOM tree. For example, in the preceding section, we invoked the identity transformation as

```java
t.transform(new DOMSource(doc), result);
```

In our example program, we do something slightly more interesting. Instead of starting out with an existing XML file, we produce a SAX XML reader that gives the illusion of parsing an XML file by emitting appropriate SAX events. Actually, our XML reader reads a flat file, as described in Chapter 2. The input file looks like this:

```
Carl Cracker|75000.0|1987|12|15
Harry Hacker|50000.0|1989|10|1
Tony Tester|40000.0|1990|3|15
```

Our XML reader generates SAX events as it processes the input. Here is a part of the parse method of the EmployeeReader class that implements the XMLReader interface:

```java
AttributesImpl attributes = new AttributesImpl();
handler.startDocument();
handler.startElement("", "staff", "staff", attributes);
while ((line = in.readLine()) != null)
{
    handler.startElement("", "employee", "employee", attributes);
    StringTokenizer t = new StringTokenizer(line, "|");
    handler.startElement("", "name", "name", attributes);
    String s = t.nextToken();
    handler.characters(s.toCharArray(), 0, s.length());
    handler.endElement("", "name", "name");
    . . .
    handler.endElement("", "employee", "employee");
}
handler.endElement("", rootElement, rootElement);
handler.endDocument();
```

The SAXSource for the transformer is constructed from the XML reader:

```java
t.transform(new SAXSource(new EmployeeReader()),
            new InputSource(new FileInputStream(filename)), result);
```

This is an ingenious trick to convert non-XML legacy data into XML. Of course, most XSLT applications will already have XML input data, and you can simply invoke the transform method on a StreamSource:

```java
t.transform(new StreamSource(file), result);
```

The transformation result is an object of a class that implements the Result interface. The Java library supplies three classes:

- DOMResult
- SAXResult
- StreamResult

To store the result in a DOM tree, use a DocumentBuilder to generate a new document node and wrap it into a DOMResult:

```java
Document doc = builder.newDocument();
t.transform(new DOMResult(doc));
```

To save the output in a file, use a StreamResult:

```java
t.transform(source, new StreamResult(file));
```

Listing 3.15 contains the complete source code.

### Listing 3.13 transform/makehtml.xsl

```xml
<?xml version="1.0" encoding="ISO-8859-1"?>

<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">

    <xsl:output method="html"/>

    <xsl:template match="/staff">
        <table border="1"><xsl:apply-templates/></table>
    </xsl:template>

    <xsl:template match="/staff/employee">
        <tr><xsl:apply-templates/></tr>
    </xsl:template>

    <xsl:template match="/staff/employee/name">
        <td><xsl:apply-templates/></td>
    </xsl:template>

    <xsl:template match="/staff/employee/salary">
        <td><xsl:apply-templates/></td>
    </xsl:template>

    <xsl:template match="/staff/employee/hiredate">
        <td><xsl:value-of select="@year"/>-<xsl:value-of
            select="@month"/>-<xsl:value-of select="@day"/></td>
    </xsl:template>

</xsl:stylesheet>
```

### Listing 3.14 transform/makereport.xsl

```xml
<?xml version="1.0"?>

<xsl:stylesheet
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    version="1.0">

    <xsl:output method="text" omit-xml-declaration="yes"/>

    <xsl:template match="/staff/employee">
        employee:<xsl:value-of select="position()"
        />/name:<xsl:value-of select="name/text()"/>
        employee:<xsl:value-of select="position()"
        />/salary:<xsl:value-of select="salary/text()"/>
        employee:<xsl:value-of select="position()"
        />/hiredate:<xsl:value-of select="hiredate/@year"
        />-<xsl:value-of select="hiredate/@month"
        />-<xsl:value-of select="hiredate/@day"/>
    </xsl:template>

</xsl:stylesheet>
```

### Listing 3.15 transform/TransformTest.java

```java
package transform;

import java.io.*;
import java.nio.file.*;
import java.util.*;
```

```java
99    public ContentHandler getContentHandler()
100   {
101       return handler;
102   }
103
104   // the following methods are just do-nothing implementations
105   public void parse(String systemId) throws IOException, SAXException {}
106   public void setErrorHandler(ErrorHandler handler) {}
107   public ErrorHandler getErrorHandler() { return null; }
108   public void setDTDHandler(DTDHandler handler) {}
109   public DTDHandler getDTDHandler() { return null; }
110   public void setEntityResolver(EntityResolver resolver) {}
111   public EntityResolver getEntityResolver() { return null; }
112   public void setProperty(String name, Object value) {}
113   public Object getProperty(String name) { return null; }
114   public void setFeature(String name, boolean value) {}
115   public boolean getFeature(String name) { return false; }
116 }
```

- **javax.xml.transform.TransformerFactory 1.4**
  - `Transformer newTransformer(Source styleSheet)`  
    returns an instance of the Transformer class that reads a stylesheet from the given source.

- **javax.xml.transform.stream.StreamSource 1.4**
  - `StreamSource(File f)`
  - `StreamSource(InputStream in)`
  - `StreamSource(Reader in)`
  - `StreamSource(String systemID)`  
    constructs a stream source from a file, stream, reader, or system ID (usually a relative or absolute URL).

- **javax.xml.transform.sax.SAXSource 1.4**
  - `SAXSource(XMLReader reader, InputSource source)`  
    constructs a SAX source that obtains data from the given input source and uses the given reader to parse the input.

| org.xml.sax.XMLReader 1.4 |  |
|---|---|
| `void setContentHandler(ContentHandler handler)` | sets the handler that is notified of parse events as the input is parsed. |
| `void parse(InputSource source)` | parses the input from the given input source and sends parse events to the content handler. |

| javax.xml.transform.dom.DOMResult 1.4 |  |
|---|---|
| `DOMResult(Node n)` | constructs a result from the given node. Usually, n is a new document node. |

| org.xml.sax.helpers.AttributesImpl 1.4 |  |
|---|---|
| `void addAttribute(String uri, String lname, String qname, String type, String value)` | adds an attribute to this attribute collection.<br><br>_Parameters:_<br>`uri` — The URI of the namespace<br>`lname` — The local name without prefix<br>`qname` — The qualified name with prefix<br>`type` — The type, one of "CDATA", "ID", "IDREF", "IDREFS", "NMTOKEN", "NMTOKENS", "ENTITY", "ENTITIES", or "NOTATION"<br>`value` — The attribute value |
| `void clear()` | removes all attributes from this attribute collection. |

This example concludes our discussion of XML support in the Java library. You should now have a good perspective on the major strengths of XML—in particular, for automated parsing and validation and as a powerful transformation mechanism. Of course, all this technology is only going to work for you if you design your XML formats well. You need to make sure that the formats are rich enough to express all your business needs, that they are stable over time, and that your business partners are willing to accept your XML documents. Those issues can be far more challenging than dealing with parsers, DTDs, or transformations.

In the next chapter, we will discuss network programming on the Java platform, starting with the basics of network sockets and moving on to higher-level protocols for e-mail and the World Wide Web.
