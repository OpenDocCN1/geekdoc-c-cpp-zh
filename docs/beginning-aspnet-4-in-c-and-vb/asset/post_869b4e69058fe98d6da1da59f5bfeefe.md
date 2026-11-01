
SelectNodes() returns a NodeList, or a collection of XmlNodes. The list contains only nodes that match the XPath statement passed in as the parameter SelectNodes. In this example, all you want to see are the title nodes. If you had made the call to SelectSingleNode, then you would have received a single node object that contained the first node in the XmlDocument that matched the XPath criteria.

A quick comment regarding the SelectSingleNode() method: This is an XPath implementation in the XmlDocument class. Both the SelectSingleNode() and SelectNodes() methods are defined in XmlNode, which XmlDocument is based on. SelectSingleNode() returns an XmlNode and SelectNodes() returns an XmlNodeList. However, the System.Xml.XPath namespace contains a richer XPath implementation, which you will look at in a later section.

## Inserting Nodes

Earlier, you looked at an example using XmlTextWriter that created a new document. The limitation was that it would not insert a node into a current document. With the XmlDocument class, you can do just that. Change the button1_Click() event handler from the last example to the following:

```
private void button4_Click(object sender, System.EventArgs e)
{
    //change path to match your structure
    _doc.Load("books.xml");
    //create a new 'book' element
    XmlElement newBook = _doc.CreateElement("book");
    //set some attributes
    newBook.SetAttribute("genre", "Mystery");
    newBook.SetAttribute("publicationDate", "2001");
    newBook.SetAttribute("ISBN", "123456789");
    //create a new 'title' element
    XmlElement newTitle = _doc.CreateElement("title");
    newTitle.InnerText = "Case of the Missing Cookie";
    newBook.AppendChild(newTitle);
    //create new author element
    XmlElement newAuthor = _doc.CreateElement("author");
    newBook.AppendChild(newAuthor);
    //create new name element
    XmlElement newName = _doc.CreateElement("name");
    newName.InnerText = "Cookie Monster";
    newAuthor.AppendChild(newName);
    //create new price element
    XmlElement newPrice = _doc.CreateElement("price");
    newPrice.InnerText = "9.95";
    newBook.AppendChild(newPrice);
    //add to the current document
    _doc.DocumentElement.AppendChild(newBook);
    //write out the doc to disk
    XmlTextWriter tr = new XmlTextWriter("booksEdit.xml", null);
    tr.Formatting = Formatting.Indented;
    _doc.WriteContentTo(tr);
    tr.Close();
    //load listBox1 with all of the titles, including new one
    XmlNodeList nodeList = _doc.GetElementsByTagName("title");
    textBox1.Text = "*";
    foreach (XmlNode node in nodeList)
    {
        textBox1.Text += node.OuterXml + "\r\n";
    }
}
```

After executing this code, you end up with the same functionality as in the previous example, but there is one additional book in the text box, The Case of the Missing Cookie (a soon-to-be classic). If you look closely at the code, you can see that this is actually a fairly simple process. The first thing that you do is create a new book element:

```
XmlElement newBook = doc.CreateElement("book");
```

CreateElement() has three overloads that allow you to specify the following:

- The element name
- The name and namespace URI
- The prefix, localname, and namespace

Once the element is created, you need to add attributes:

```
newBook.SetAttribute("genre", "Mystery");
newBook.SetAttribute("publicationdate", "2001");
newBook.SetAttribute("ISBN", "123456789");
```

Now that you have the attributes created, you need to add the other elements of a book:

```
XmlElement newTitle = doc.CreateElement("title");
newTitle.InnerText = "The Case of the Missing Cookie";
newBook.AppendChild(newTitle);
```

Once again, you create a new XmlElement-based object (newTitle). Then you set the InnerText property to the title of our new classic and append the element as a child to the book element. You repeat this for the rest of the elements in this book element. Note that you add the name element as a child to the author element. This will give you the proper nesting relationship, as in the other book elements.

Finally, you append the newBook element to the doc.DocumentElement node. This is the same level as all of the other book elements. You now have an updated an existing document with a new element.

The last thing to do is to write the new XML document to disk. In this example, you create a new XmlTextWriter and pass it to the WriteContentTo() method. WriteContentTo() and WriteTo() both take an XmlTextWriter as a parameter. WriteContentTo() saves the current node and all of its children to the XmlTextWriter, whereas WriteTo() just saves the current node. Because doc is an XmlDocument-based object, it represents the entire document and so that is what is saved. You could also use the Save() method. It will always save the entire document.

Save() has four overloads. You can specify a string with the filename and path, a Stream-based object, a TextWriter-based object, or an XmlWriter-based object.

You also call the Close() method on XmlTextWriter to flush the internal buffers and close the file.

![](img/d7d2ffa0a76feaab821930e95daace93_977_0.png)

Figure 33-1 shows what you get when you run this example. Notice the new entry at the bottom of the list.

## FIGURE 33-1

Earlier in the chapter, you saw how to create a document using the XmlTextWriter class. You can also use XmlDocument. Why would you use one in preference to the other? If the data that you want streamed to XML is available and ready to write, then the XmlTextWriter class is the best choice. However, if you need to build the XML document a little at a time, inserting nodes into various places, then creating the document with XmlDocument might be the better choice. You can accomplish this by changing the following line:

```
doc.Load("books.xml");
```

to this:

```
//create the declaration section
XmlDeclaration newDec = doc.CreateXmlDeclaration("1.0",null,null);
doc.AppendChild(newDec);
//create the new root element
XmlElement newRoot = doc.CreateElement("newBookstore");
doc.AppendChild(newRoot);
```

First, you create a new XmlDeclaration. The parameters are the version (always 1.0 for now), the encoding, and the standalone flag. The encoding parameter should be set to a string that is part of the System.Text.Encoding class if null is not used (null defaults to UTF-8). The standalone flag can be either yes, no, or null. If it is null, the attribute is not used and will not be included in the document.

The next element that is created will become the DocumentElement. In this case, it is called newBookstore so that you can see the difference. The rest of the code is the same as in the previous example and works in the same way.

This is booksEdit.xml, which is generated from the following code:

```
<?xml version="1.0"?>
<newBookstore>
  <book genre="Mystery" publicationDate="2001" ISBN="123456789">
    <title>The Case of the Missing Cookie</title>
    <author>
      <name>C. Monster</name>
    </author>
    <price>9.95</price>
  </book>
</newBookstore>
```

You will want to use the XmlDocument class when you want to have random access to the document, or the XmlReader-based classes when you want a streaming-type model instead. Remember that there is a cost for the flexibility of the XmlNode-based XmlDocument class — memory requirements are higher and the performance of reading the document is not as good as when using XmlReader. There is another way to traverse an XML document: the XPathNavigator.

## USING XPATHNAVIGATORS

An XPathNavigator is used to select, iterate through, and sometimes edit data from an XML document. An XPathNavigator can be created from an XmlDocument to allow editing capabilities or from an XPathDocument for read-only use. Because the XPathDocument is read-only, it performs very well.

Unlike the XmlReader, the XPathNavigator is not a streaming model, so the same document can be used without having to re-read and parse.

The XPathNavigator is part of the System.Xml.XPath namespace. XPath is a query language used to select specific nodes or elements from an XML document for processing.

### The System.Xml.XPath Namespace

The System.Xml.XPath namespace is built for speed. It provides a read-only view of your XML documents, so there are no editing capabilities. Classes in this namespace are built to do fast iteration and selections on the XML document in a cursory fashion.

The following table lists the key classes in System.Xml.XPath and gives a short description of the purpose of each class.
