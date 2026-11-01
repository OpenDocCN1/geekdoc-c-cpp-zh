SelectNodes() returns a NodeList, or a collection of XmlNodes. The list contains only nodes that match the XPath statement passed in as the parameter SelectNodes. In this example, all you want to see are the title nodes. If you had made the call to SelectSingleNode, then you would have received a single node object that contained the first node in the XmlDocument that matched the XPath criteria.

A quick comment regarding the SelectSingleNode() method: This is an XPath implementation in the XmlDocument class. Both the SelectSingleNode() and SelectNodes() methods are defined in XmlNode, which XmlDocument is based on. SelectSingleNode() returns an XmlNode and SelectNodes() returns an XmlNodeList. However, the System.Xml.XPath namespace contains a richer XPath implementation, which you will look at in a later section.

# Inserting Nodes

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