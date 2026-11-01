```
writer.WriteElementString("title", "Case of the Missing Cookie");
writer.WriteStartElement("author");
writer.WriteElementString("name", "Cookie Monster");
writer.WriteEndElement();
writer.WriteElementString("price", "9.99");
writer.WriteEndElement();
writer.WriteEndDocument();
//clean up
writer.Flush();
writer.Close();
}
```

code download XMLReaderSample.sln

Here, you are writing to a new XML file called newbook.xml, adding the data for a new book. Note that XmlWriter will overwrite an existing file with a new one. You will look at inserting a new element or node into an existing document later in this chapter. You are instantiating the XmlWriter object by using the Create static method. In this example, a string representing a filename is passed as a parameter, along with an instance of an XmlWriterSettings class.

The XmlWriterSettings class has properties that control the way that the XML is generated. The CheckedCharacters property is a Boolean that will raise an exception if a character in the XML does not conform to the W3C XML 1.0 recommendation. The Encoding class sets the encoding used for the XML being generated; the default is Encoding.UTF8. The Indent property is a Boolean value that determines if elements should be indented. The IndentChars property is set to the character string that it is used to indent. The default is two spaces. The NewLine property is used to determine the characters for line breaks. In the preceding example, the NewLineOnAttribute is set to true. This will put each attribute in a separate line, which can make the XML generated a little easier to read.

WriteStartDocument() adds the document declaration. Now you start writing data. First comes the book element; next, you add the genre, publicationdate, and ISBN attributes. Then you write the title, author, and price elements. Note that the author element has a child element name.

When you click the button, you produce the booknew.xml file, which looks like this:

```
<?xml version="1.0" encoding="utf-8"?>
<book
  genre="Mystery"
  publicationdate="2001"
  ISBN="123456789"
  <title>Case of the Missing Cookie</title>
  <author>
    <name>Cookie Monster</name>
  </author>
  <price>9.99</price>
</book>
```

The nesting of elements is controlled by paying attention to when you start and finish writing elements and attributes. You can see this when you add the name child element to the author element. Note how the WriteStartElement() and WriteEndElement() method calls are arranged and how that arrangement produces the nested elements in the output file.

To go along with the WriteElementString() and WriteAttributeString() methods, there are several other specialized write methods. WriteCDATA() outputs a CDATA section (<![CDATA[ ]]>), writing out the text it takes as a parameter. WriteComment() writes out a comment in proper XML format. WriteChars() writes out the contents of a char buffer. This works in a similar fashion to the ReadChars() method that you looked at earlier; they both use the same type of parameters. WriteChars() needs a buffer (an array of characters), the starting position for writing (an integer), and the number of characters to write (an integer).