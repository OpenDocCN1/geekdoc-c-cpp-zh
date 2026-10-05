# Code that reads an XML document

22-90 shows code that loads the contents of the Products.xml file into a List<> collection of Product objects. The first statement creates a new List<> collection to store the Product objects. The second statement specifies the path for the Products.xml file, which is in C:\2010Files directory. The next three statements create an XmlReaderSettings object and set its IgnoreWhitespace and IgnoreComments properties so the reader will ignore any nodes for white space or comments. Then, this code creates an XmlReader object by passing the specified path and settings to the static Create method of the XmlReader class.

After the XmlReader object has been created, the ReadToDescendant method is used to read any nodes in the XML file before the first Product element. If this method returns a true value, it indicates that a Product element was found. The do-while loop runs and processes the data for each Product element in the file. This loop begins by using the indexer to retrieve the value of the Code attribute. This works because the do-while loop always begins with the reader positioned at the start tag for the Product element.

After the Code attribute has been retrieved and stored in the Product object, the loop uses the ReadStartElement method to advance to the next node, which is the Description element's start tag. Although it's also possible to use a Read method here, the ReadStartElement ensures that the reader is on the Product element.

After the reader has been positioned at the Description element, the next two statements use the ReadElementContentAsString and ReadElementAsAs methods to retrieve the contents of the Description and Price elements. Then, the last line adds the Product object to the List<> collection.

Note that the ReadNextSibling method is used as the condition at the end of the do-while loop. As a result, if the XML document contains another Product element, this method advances to the start tag for the next Product element and returns a true value so the loop will repeat. However, if the XML document doesn't contain another Product element, this method will return a false value and the loop won't repeat. In that case, the Close method is called to close the reader.

If the Products.xml file doesn't contain an XML document like the one that's expected, one of the Read methods will throw an exception of the XmlException. To catch this type of exception, you can code a try-catch statement just as you would for any other type of exception.

# A class that works with an XML file

22-10 presents the code for a ProductDB class that works with the data in an XML file. This shows how the code presented in this chapter can be used to implement the database class that's used by the Product Maintenance application that was presented in chapter 12. If you understand the earlier versions of this application, you shouldn't have any trouble understanding how this class works.