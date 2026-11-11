```
```java
InputStream in = new FileInputStream(fileName);
Doc doc = new SimpleDoc(in, flavor, null);
```
```

Finally, you are ready to print:

```
```java
job.print(doc, null);
```
```

As before, the null parameter can be replaced by an attribute set.

Note that this printing process is quite different from that of the preceding section. There is no user interaction through print dialog boxes. For example, you can implement a server-side printing mechanism in which users submit print jobs through a web form.

The program in Listing 11.16 demonstrates how to use a print service to print an image file.

# Listing 11.16 `printService/PrintServiceTest.java`

```
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
```