To write an element without children (such as `<img .../>`), use the call

```
writer.writeEmptyElement(name);
```

Finally, at the end of the document, call

```
writer.writeEndDocument();
```

This call closes any open elements.

You still need to close the XMLStreamWriter, and you need to do it manually since the XMLStreamWriter interface does not extend the AutoCloseable interface.

As with the DOM/XSLT approach, you don’t have to worry about escaping characters in attribute values and character data. However, it is possible to produce malformed XML, such as a document with multiple root nodes. Also, the current version of StAX has no support for producing indented output.

The program in Listing 3.9 shows you both approaches for writing XML.

# **Listing 3.9** `write/XMLWriteTest.java`

```
package write;

import java.io.*;
import java.nio.file.*;
import java.util.*;
import javax.xml.parsers.*;
import javax.xml.stream.*;
import javax.xml.transform.*;
import javax.xml.transform.dom.*;
import javax.xml.transform.stream.*;

import org.w3c.dom.*;
/**
 * This program shows how to write an XML file. It produces modern art in SVG
 * format.
 * @version 1.12 2016-04-27
 * @author Cay Horstmann
 */
public class XMLWriteTest
{
   public static void main(String[] args) throws Exception
   {
      Document doc = new Drawing(600, 400);
      writeDocument(doc, "drawing1.svg");
      writeNewDrawing(600, 400, "drawing2.svg");
   }

   private static Random generator = new Random();
```