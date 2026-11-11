
### Table 11.3 Document Flavors for Print Services

| Data Source | Data Type | MIME Type |
| --- | --- | --- |
| INPUT_STREAM | GIF | image/gif |
| URL | JPEG | image/jpeg |
| BYTE_ARRAY | PNG | image/png |
|  | POSTSCRIPT | application/postscript |
|  | PDF | application/pdf |
|  | TEXT_HTML_HOST | text/html (using host encoding) |
|  | TEXT_HTML_US_ASCII | text/html; charset=us-ascii |
|  | TEXT_HTML_UTF_8 | text/html; charset=utf-8 |
|  | TEXT_HTML_UTF_16 | text/html; charset=utf-16 |
|  | TEXT_HTML_UTF_16LE | text/html; charset=utf-16le (little-endian) |
|  | TEXT_HTML_UTF_16BE | text/html; charset=utf-16be (big-endian) |
|  | TEXT_PLAIN_HOST | text/plain (using host encoding) |
|  | TEXT_PLAIN_US_ASCII | text/plain; charset=us-ascii |
|  | TEXT_PLAIN_UTF_8 | text/plain; charset=utf-8 |
|  | TEXT_PLAIN_UTF_16 | text/plain; charset=utf-16 |
|  | TEXT_PLAIN_UTF_16LE | text/plain; charset=utf-16le (little-endian) |
|  | TEXT_PLAIN_UTF_16BE | text/plain; charset=utf-16be (big-endian) |
|  | PCL | application/vnd.hp-PCL (Hewlett Packard Printer Control Language) |
|  | AUTOSENSE | application/octet-stream (raw printer data) |
| READER | TEXT_HTML | text/html; charset=utf-16 |
| STRING | TEXT_PLAIN | text/plain; charset=utf-16 |
| CHAR_ARRAY |  |  |
| SERVICE_FORMATTED | PRINTABLE | N/A |
|  | PAGEABLE | N/A |
|  | RENDERABLE_IMAGE | N/A |

```java
InputStream in = new FileInputStream(fileName);
Doc doc = new SimpleDoc(in, flavor, null);
```

Finally, you are ready to print:

```java
job.print(doc, null);
```

As before, the null parameter can be replaced by an attribute set.

Note that this printing process is quite different from that of the preceding section. There is no user interaction through print dialog boxes. For example, you can implement a server-side printing mechanism in which users submit print jobs through a web form.

The program in Listing 11.16 demonstrates how to use a print service to print an image file.

### Listing 11.16 `printService/PrintServiceTest.java`

```java
package printService;

import java.io.*;
import java.nio.file.*;
import javax.print.*;

/**
 * This program demonstrates the use of print services. The program lets you print a GIF image to
 * any of the print services that support the GIF document flavor.
 * @version 1.0 2007-08-16
 * @author Cay Horstmann
 */
public class PrintServiceTest
{
   public static void main(String[] args)
   {
      DocFlavor flavor = DocFlavor.URL.GIF;
      PrintService[] services = PrintServiceLookup.lookupPrintServices(flavor, null);
      if (args.length == 0)
      {
         if (services.length == 0) System.out.println("No printer for flavor " + flavor);
         else
         {
            System.out.println("Specify a file of flavor " + flavor
                  + "\nand optionally the number of the desired printer.");
            for (int i = 0; i < services.length; i++)
               System.out.println((i + 1) + ": " + services[i].getName());
         }
         System.exit(0);
      }
   }
}
```

| `javax.print.SimpleDoc 1.4` |
|---|
| • `SimpleDoc(Object data, DocFlavor flavor, DocAttributeSet attributes)` — constructs a SimpleDoc object that can be printed with a DocPrintJob. |

**Parameters:**

| Parameter | Description |
|---|---|
| `data` | The object with the print data, such as an input stream or a Printable |
| `flavor` | The document flavor of the print data |
| `attributes` | Document attributes, or null if attributes are not required |

## 11.12.5 Stream Print Services

A print service sends print data to a printer. A stream print service generates the same print data but instead sends them to a stream, perhaps for delayed printing or because the print data format can be interpreted by other programs. In particular, if the print data format is PostScript, it may be useful to save the print data to a file because many programs can process PostScript files. The Java platform includes a stream print service that can produce PostScript output from images and 2D graphics. You can use that service on all systems, even if there are no local printers.

Enumerating stream print services is a bit more tedious than locating regular print services. You need both the DocFlavor of the object to be printed and the MIME type of the stream output. You then get a StreamPrintServiceFactory array of factories.

```java
DocFlavor flavor = DocFlavor.SERVICE_FORMATTED.PRINTABLE;
String mimeType = "application/postscript";
StreamPrintServiceFactory[] factories
    = StreamPrintServiceFactory.lookupStreamPrintServiceFactories(flavor, mimeType);
```

The StreamPrintServiceFactory class has no methods that would help us distinguish any one factory from another, so we just take factories[0]. We call the getPrintService method with an output stream parameter to get a StreamPrintService object.

```java
OutputStream out = new FileOutputStream(fileName);
StreamPrintService service = factories[0].getPrintService(out);
```

The StreamPrintService class is a subclass of PrintService. To produce a printout, simply follow the steps of the preceding section.

| `javax.print.StreamPrintServiceFactory` | `1.4` |
|---|---|
| `StreamPrintServiceFactory[] lookupStreamPrintServiceFactories(DocFlavor flavor, String mimeType)` | Looks up the stream print service factories that can print the given document flavor and produce an output stream of the given MIME type. |
| `StreamPrintService getPrintService(OutputStream out)` | Gets a print service that sends the printing output to the given output stream. |

## 11.12.6 Printing Attributes

The print service API contains a complex set of interfaces and classes to specify various kinds of attributes. There are four important groups of attributes. The first two specify requests to the printer.

- *Print request attributes* request particular features for all doc objects in a print job, such as two-sided printing or the paper size.
- *Doc attributes* are request attributes that apply only to a single doc object.

The other two attributes contain information about the printer and job status.

- *Print service attributes* give information about the print service, such as the printer make and model or whether the printer is currently accepting jobs.
- *Print job attributes* give information about the status of a particular print job, such as when the job is already completed.

To describe the various attributes, there is an interface Attribute with subinterfaces:

```
PrintRequestAttribute
DocAttribute
PrintServiceAttribute
PrintJobAttribute
SupportedValuesAttribute
```

Individual attribute classes implement one or more of these interfaces. For example, objects of the Copies class describe the number of copies of a printout. That class implements both the `PrintRequestAttribute` and the `PrintJobAttribute` interfaces. Clearly, a print request can contain a request for multiple copies. Conversely, an attribute of the print job might be how many of these copies were actually printed. That number might be lower, perhaps because of printer limitations or because the printer ran out of paper.

The `SupportedValuesAttribute` interface indicates that an attribute value does not reflect actual request or status data but rather the capability of a service. For example, the CopiesSupported class implements the SupportedValuesAttribute interface. An object of that class might describe that a printer supports 1 through 99 copies of a printout.

Figure 11.38 shows a class diagram of the attribute hierarchy.

![](img/7dd923a566750151a3aab0dacd0cdaa5_900_0.png)

Figure 11.38 The attribute hierarchy

In addition to the interfaces and classes for individual attributes, the print service API defines interfaces and classes for attribute sets. A superinterface, AttributeSet, has four subinterfaces:

- PrintRequestAttributeSet
- DocAttributeSet
- PrintServiceAttributeSet
- PrintJobAttributeSet

Each of these interfaces has an implementing class, yielding the five classes:

- HashAttributeSet
- HashPrintRequestAttributeSet
- HashDocAttributeSet
- HashPrintServiceAttributeSet
- HashPrintJobAttributeSet

Figure 11.39 shows a class diagram of the attribute set hierarchy.

For example, you can construct a print request attribute set like this:

```
PrintRequestAttributeSet attributes = new HashPrintRequestAttributeSet();
```
