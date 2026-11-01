```
```xml
<TITLE>The Tragedy of Hamlet, Prince of Denmark</TITLE>

<!--XML removed for clarity-->

<PERSONAE>
    <TITLE>Dramatis Personae</TITLE>
    <PERSONA>CLAUDIUS, king of Denmark.</PERSONA>
    <PERSONA>HAMLET, son to the late king, and nephew to the present king.</PERSONA>
    <PERSONA>POLONIUS, lord chamberlain.</PERSONA>
    <PERSONA>HORATIO, friend to Hamlet.</PERSONA>
    <PERSONA>LAERTES, son to Polonius.</PERSONA>
    <PERSONA>LUCIANUS, nephew to the king.</PERSONA>
    <!--XML removed for clarity-->
</PERSONAE>

</PLAY>
```
```

Now look at this C# query:

```
```csharp
XDocument xdoc = XDocument.Load(@"C:\hamlet.xml");

Console.WriteLine(
    xdoc.Element("PLAY").Element("PERSONAE").Element("PERSONA").Value);
```
```

This bit of code starts at <PLAY>, works down to the <PERSONAE> element, and then makes use of the <PERSONA> element. However, using this will produce the following results:

CLAUDIUS, king of Denmark

The reason for this is that although there is a collection of <PERSONA> elements, you are dealing only with the first one that is encountered using the Element().Value call.

# Writing to an XML Document

In addition to reading from an XML document, you can write to the document just as easily. For instance, if you wanted to change the name of the first player of the Hamlet play file, you could use the following code:

```
```csharp
using System;
using System.Linq;
using System.Xml.Linq;

namespace ConsoleApplication1
{
    class Class1
    {
        static void Main()
        {
            XDocument xdoc = XDocument.Load(@"C:\hamlet.xml");

            xdoc.Element("PLAY").Element("PERSONAE").
                Element("PERSONA").SetValue("Bill Evjen, king of Denmark");

            Console.WriteLine(xdoc.Element("PLAY").
                Element("PERSONAE").Element("PERSONA").Value);

            Console.ReadLine();
        }
    }
}
```
```