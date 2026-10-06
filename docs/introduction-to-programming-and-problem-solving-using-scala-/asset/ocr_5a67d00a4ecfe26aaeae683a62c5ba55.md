# 14.2.4 Writing XML to File

Once you have the Node you want to write, the writing process is as easy as a call to the save method of the XML object.

```
xml.save("grades.xml",node);
```

The first argument is the name of the file you want to write to. The second is the Node you want to write.

# Validating XML (Advanced)

XML is used for large applications, it is important to be able to verify that the contents of a file match the format that is required by the applications. This process is called validation. When the XML standard was first released, validation was done with Document Type Definitions (DTDs). A DTD is a text file that has a fairly simple format that allows you to specify what types of elements should be in a file. For each element you can say what needs to be in or what could be in it. This ability includes attributes as well as sub-elements.

DTDs were generally considered to have two problems. First, they were a bit limited and simplistic. For example, you could say that an element must contain an attribute, but could not put any constraints on the nature of that attribute. For example, you could not say that it had to be a number or a date. In addition, DTDs had their own syntax. The goal of XML was to be a general data storage format and some unifying that by use some other format to specify what goes into an XML

For these reasons, XML schema created. An XML schema is an XML document that uses tags to specify what and cannot go into other XML files. XML schema needs to be large and complex, but they provide great control over the format of an XML file.

There are tools for both DTDs and XML schema that will run through XML files and tell you whether or not they adhere to a given specification. There is also a package in the Scala standard libraries called scala.xml.dtd that can help with validation using DTDs.

# 14.2.5 XML Patterns

We have seen patterns in a number of places so. With XML we can add another. Not only can XML be written directly into the Scala language, it can be used to build patterns. The patterns look like what you would like to build XML, except that what you put into curly braces are names you want bound as. There is one significant limitation, you cannot put attributes into your patterns. This usage can be seen with the following example in REPL:

```
scala val personXML = <person>Kyle</name><gender>M</gender></person>
personXML: scala.xml.Elem = <person>Kyle</name><gender>M</gender></person>
```

```
scala val <person>{name}</name><gender>{sex}</gender></person> = personXML
name: scala.xml.Node = Kyle
sex: scala.xml.Node = M
```