```
```scala
{years.map(yearToXML)}
{rideInfo.map(rideDataToXML)}
{employeeInfo.map(employeeToXML)}
</themeParkData>)
```
```

There is completely new code at the bottom to allow for data entry that is added to the main variables. There is also a do-while loop that handles the menu functionality. The script ends by saving the main data elements back out to the same XML file.

# 14.4  End of Chapter Material

# 14.4.1  Summary of Concepts

+   - XML is a text markup language that can be used to encode arbitrary data. Being text means that it is as easy to work with as flat text files, but it allow you to attach meaning to the values in the file and the flexibility of the parsing makes it easier to extend XML files than flat text files.
+   
+   - An XML file is composed of markup and content. The content is plain text. Markup has a number of options as must follow a certain format.
+     - The primary markup is tags. A tag starts with `<` and ends with `>`. Each tag has a name.
+     - The combination of a matching start and end tag defines an element. An element can contain content and other elements.
+     - Start tags can be given attributes to store basic information.
+     - Special characters that can not appear as plain text can be specified by markup tokens that begin with a `&` and end with a `;`.
+     - You can put comments into an XML file by starting them with `<!--` and ending them with `-->`.
+     - The entire contents of an XML file must be held inside of a single element.
+   
+   - The Scala language has native support for XML. This makes it significantly easier to work with XML in Scala than in most other languages. XML elements can be written directly into Scala source code.
+     - An XML file can be loaded using `XML.loadFile(fileName:String):Elem`.
+     - The `\` and `\\` operators can be used to pull things out of XML.
+     - You can build XML by typing in XML literals. You can put Scala code into the XML by surrounding it with curly braces.
+     - XML can be written back out to file using `XML.save(fileName:String,node:Node)`.
+     - Patterns can be made using XML with the limitation that attributes can not be part of the match. Values can be bound by including names in curly braces.