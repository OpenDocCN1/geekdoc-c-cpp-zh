# XML

meaning to the values in the file, and the flexibility of the parsing makes it easier to
end XML files flat text files.

+   An XML file is composed of markup and content. The content is plain text. Markup
h a number of options that must follow a certain format.
- The primary markup is tags. A tag starts with < and ends with. Each tag has
a name.
- The combination of a matching start and end tag defines an element. An element
 contain content and other elements.
- Start tags can be given attributes to store basic information.
- Special characters that cannot appear as plain text can be specified by markup
tokens that begin with a & and ends with a ;
- You can put comments into an XML file by starting them with <!-- and ending
them with -->.
- The entire contents of an XML file must be held inside of a single element.

+   The Scala language has native support for XML. This makes it significantly easier to
work with XML in Scala in most other languages. Scala elements can be written
directly into Scala source code.

+   An XML file is loaded using XML.loadFile(fileName:String): Elem.
- The \ and \ operators can be used to pull things out of XML.
- You can build XML by typing in Scala literals. You can put Scala code into the
XML by surrounding it with curly braces.
- XML can be written to file using XML.save(fileName:String,node:Node).
- Patterns can be made using XML with the limitation that attributes cannot be
part the match. Values can be bound by including names in curly braces.

# 14.4.2 Self-Directed Study

Enter the following statements in the REPL and see what they do. Some will produce
errors. You try to figure out why. Try some variations to make sure you understand
what is going on.

```
scala val xml1 = <tag>contents</tag>
scala xml1.text
scala val <tag>{str}</tag> = xml1
scala val xml2 = <data type="simple">
| <language>Scala</language>
| <lesson>Programming is an art./lesson>
| <lesson>Software runs the world</lesson>
| </data>
scala val xml2 = "language"
scala xml12 = "lesson"
scala val xml3 = <randPoints>
| {(i <- 1 to 20).map(i => <point x={math.random.toString}
  y={math.random.toString}>})
| </randPoints>
scala val (xml3 = "point").map(p) => {
```