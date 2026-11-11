# org.xml.sax.XMLReader 1.4

+   - `void setContentHandler(ContentHandler handler)`  
+     sets the handler that is notified of parse events as the input is parsed.
+   - `void parse(InputSource source)`  
+     parses the input from the given input source and sends parse events to the content handler.

# javax.xml.transform.dom.DOMResult 1.4

+   - `DOMResult(Node n)`  
+     constructs a source from the given node. Usually, n is a new document node.

# org.xml.sax.helpers.AttributesImpl 1.4

+   - `void addAttribute(String uri, String lname, String qname, String type, String value)`  
+     adds an attribute to this attribute collection. The lname parameter is the local name without prefix, and qname is the qualified name with prefix. The type parameter is one of "CDATA", "ID", "IDREF", "IDREFS", "NMTOKEN", "NMTOKENS", "ENTITY", "ENTITIES", or "NOTATION".
+   - `void clear()`  
+     removes all attributes from this attribute collection.

This example concludes our discussion of XML support in the Java library. You should now have a good perspective on the major strengths of XML—in particular, its automated parsing and validation as well as its powerful transformation mechanism. Of course, all this technology is only going to work for you if you design your XML formats well. You need to make sure that the formats are rich enough to express all your business needs, that they are stable over time, and that your business partners are willing to accept your XML documents. Those issues can be far more challenging than dealing with parsers, DTDs, or transformations.

In the next chapter, we will discuss network programming on the Java platform, starting with the basics of network sockets and moving on to higher-level protocols for e-mail and the World Wide Web.