
```java
if (lname.equals("a") && attrs != null)
{
    for (int i = 0; i < attrs.getLength(); i++)
    {
        String aname = attrs.getLocalName(i);
        if (aname.equals("href")) System.out.println(attrs.getValue(i));
    }
}
}
};
SAXParserFactory factory = SAXParserFactory.newInstance();
factory.setNamespaceAware(true);
factory.setFeature("http://apache.org/xml/features/nonvalidating/load-external-dtd", false);
SAXParser saxParser = factory.newSAXParser();
InputStream in = new URL(url).openStream();
saxParser.parse(in, handler);
}
}
```

### javax.xml.parsers.SAXParserFactory 1.4

- `static SAXParserFactory newInstance()`  
  returns an instance of the SAXParserFactory class.
- `SAXParser newSAXParser()`  
  returns an instance of the SAXParser class.
- `boolean isNamespaceAware()`
- `void setNamespaceAware(boolean value)`  
  gets or sets the namespace-aware property of the factory. If set to true, the parsers that this factory generates are namespace-aware.
- `boolean isValidating()`
- `void setValidating(boolean value)`  
  gets or sets the validating property of the factory. If set to true, the parsers that this factory generates validate their input.

### javax.xml.parsers.SAXParser 1.4

- `void parse(File f, DefaultHandler handler)`
- `void parse(String url, DefaultHandler handler)`
- `void parse(InputStream in, DefaultHandler handler)`  
  parses an XML document from the given file, URL, or input stream and reports parse events to the given handler.

### org.xml.sax.ContentHandler 1.4

- `void startDocument()`
- `void endDocument()`

  is called at the start or the end of the document.

- `void startElement(String uri, String lname, String qname, Attributes attr)`
- `void endElement(String uri, String lname, String qname)`

  is called at the start or the end of an element.

  **Parameters:**

  | Name | Description |
  |---|---|
  | `uri` | The URI of the namespace (if the parser is namespace-aware) |
  | `lname` | The local name without prefix (if the parser is namespace-aware) |
  | `qname` | The element name if the parser is not namespace-aware, or the qualified name with prefix if the parser reports qualified names in addition to local names |

- `void characters(char[] data, int start, int length)`

  is called when the parser reports character data.

  **Parameters:**

  | Name | Description |
  |---|---|
  | `data` | An array of character data |
  | `start` | The index of the first character in the data array that is a part of the reported characters |
  | `length` | The length of the reported character string |

### org.xml.sax.Attributes 1.4

- `int getLength()`

  returns the number of attributes stored in this attribute collection.

- `String getLocalName(int index)`

  returns the local name (without prefix) of the attribute with the given index, or the empty string if the parser is not namespace-aware.

- `String getURI(int index)`

  returns the namespace URI of the attribute with the given index, or the empty string if the node is not part of a namespace or if the parser is not namespace-aware.

- `String getQName(int index)`

  returns the qualified name (with prefix) of the attribute with the given index, or the empty string if the qualified name is not reported by the parser.

## AI in Healthcare

This is the opening paragraph of the document. Artificial Intelligence is transforming the healthcare sector by improving diagnostics, personalizing treatment plans, and streamlining administrative workflows.

- Improved medical imaging analysis with faster and more accurate reads.
- Predictive analytics for patient deterioration and early intervention.
- Automated transcription and clinical documentation for providers.
- Personalized medicine based on genetic profiles and history.

> "The integration of AI is not just about technology, but about creating more time for human connection in healthcare."

Despite the promising benefits, the adoption of AI in clinical settings faces challenges including regulatory hurdles, data privacy concerns, and the need for robust validation workflows.

Figure 1 shows the projected growth of AI adoption in healthcare over the next five years.

To analyze the attribute values, call the appropriate methods of the XMLStreamReader class. For example,

```java
String units = parser.getAttributeValue(null, "units");
```

gets the units attribute of the current element.

By default, namespace processing is enabled. You can deactivate it by modifying the factory:

```java
XMLInputFactory factory = XMLInputFactory.newInstance();
factory.setProperty(XMLInputFactory.IS_NAMESPACE_AWARE, false);
```

Listing 3.9 contains the code for the web crawler program implemented with the StAX parser. As you can see, the code is simpler than the equivalent SAX code because you don't have to worry about event handling.

### Listing 3.9 stax/StAXTest.java

```java
package stax;

import java.io.*;
import java.net.*;
import javax.xml.stream.*;

/**
 * This program demonstrates how to use a StAX parser. The program prints all hyperlinks of
 * an XHTML web page. <br>
 * Usage: java stax.StAXTest URL
 * @author Cay Horstmann
 * @version 1.0 2007-06-23
 */
public class StAXTest
{
   public static void main(String[] args) throws Exception
   {
      String urlString;
      if (args.length == 0)
      {
         urlString = "http://www.w3c.org";
         System.out.println("Using " + urlString);
      }
      else urlString = args[0];
      URL url = new URL(urlString);
      InputStream in = url.openStream();
      XMLInputFactory factory = XMLInputFactory.newInstance();
      XMLStreamReader parser = factory.createXMLStreamReader(in);
      while (parser.hasNext())
      {
         int event = parser.next();
         if (event == XMLStreamConstants.START_ELEMENT)
         {
            if (parser.getLocalName().equals("a"))
            {
               String href = parser.getAttributeValue(null, "href");
               if (href != null)
                  System.out.println(href);
            }
         }
      }
   }
}
```

### javax.xml.stream.XMLInputFactory

- `static XMLInputFactory newInstance()`  
  returns an instance of the XMLInputFactory class.

- `void setProperty(String name, Object value)`  
  sets a property for this factory, or throws an `IllegalArgumentException` if the property is not supported or cannot be set to the given value. The Java SE implementation supports the following Boolean-valued properties:

| Property | Description |
|---|---|
| `"javax.xml.stream.isValidating"` | When false (the default), the document is not validated. Not required by the specification. |
| `"javax.xml.stream.isNamespaceAware"` | When true (the default), namespaces are processed. Not required by the specification. |
| `"javax.xml.stream.isCoalescing"` | When false (the default), adjacent character data are not coalesced. |
| `"javax.xml.stream.isReplacingEntityReferences"` | When true (the default), entity references are replaced and reported as character data. |
| `"javax.xml.stream.isSupportingExternalEntities"` | When true (the default), external entities are resolved. The specification gives no default for this property. |
| `"javax.xml.stream.supportDTD"` | When true (the default), DTDs are reported as events. |

- `XMLStreamReader createXMLStreamReader(InputStream in)`
- `XMLStreamReader createXMLStreamReader(InputStream in, String characterEncoding)`
- `XMLStreamReader createXMLStreamReader(Reader in)`
- `XMLStreamReader createXMLStreamReader(Source in)`  
  creates a parser that reads from the given stream, reader, or JAXP source.

| `javax.xml.stream.XMLStreamReader` |
|---|
| • `boolean hasNext()`<br>returns true if there is another parse event.<br><br>• `int next()`<br>sets the parser state to the next parse event and returns one of the following constants: `START_ELEMENT`, `END_ELEMENT`, `CHARACTERS`, `START_DOCUMENT`, `END_DOCUMENT`, `CDATA`, `COMMENT`, `SPACE` (ignorable whitespace), `PROCESSING_INSTRUCTION`, `ENTITY_REFERENCE`, `DTD`.<br><br>• `boolean isStartElement()`<br>• `boolean isEndElement()`<br>• `boolean isCharacters()`<br>• `boolean isWhiteSpace()`<br>returns true if the current event is a start element, end element, character data, or whitespace.<br><br>• `QName getName()`<br>• `String getLocalName()`<br>gets the name of the element in a `START_ELEMENT` or `END_ELEMENT` event.<br><br>• `String getText()`<br>returns the characters of a `CHARACTERS`, `COMMENT`, or `CDATA` event, the replacement value for an `ENTITY_REFERENCE`, or the internal subset of a DTD.<br><br>• `int getAttributeCount()`<br>• `QName getAttributeName(int index)`<br>• `String getAttributeLocalName(int index)`<br>• `String getAttributeValue(int index)`<br>gets the attribute count and the names and values of the attributes, provided the current event is `START_ELEMENT`.<br><br>• `String getAttributeValue(String namespaceURI, String name)`<br>gets the value of the attribute with the given name, provided the current event is `START_ELEMENT`. If namespaceURI is null, the namespace is not checked. |

## 3.7 Generating XML Documents

You now know how to write Java programs that read XML. Let us now turn to the opposite process: producing XML output. Of course, you could write an XML file simply by making a sequence of print calls, printing the elements, attributes, and text content, but that would not be a good idea. The code is rather tedious, and you can easily make mistakes if you don’t pay attention to special symbols (such as " or <) in the attribute values and text content.
