
| CLASS NAME | DESCRIPTION |
|---|---|
| XPathDocument | Provides a view of the entire XML document. Read-only. |
| XPathNavigator | Provides the navigational capabilities to an XPathDocument. |
| XPathNodeIterator | Provides iteration capabilities to a node set. |
| XPathExpression | Represents a compiled XPath expression. Used by SelectNodes, SelectSingleNode, Evaluate, and Matches. |
| XPathException | An XPath exception class. |

## XPathDocument

XPathDocument does not offer any of the functionality of the XmlDocument class. Its sole purpose is to create XPathNavigator. In fact, that is the only method available on the XPathDocument class (other than those provided by Object).

An XPathDocument can be created in a number of different ways. You can pass in an XmlReader, a filename of an XML document, or a Stream-based object to the constructor. This allows a great deal of flexibility. For example, you can use the XmlValidatingReader to validate the XML and then use that same object to create the XPathDocument.

## XPathNavigator

XPathNavigator contains all of the methods for moving and selecting elements that you need. The following table lists some of the "move" methods defined in this class.

| METHOD NAME | DESCRIPTION |
|---|---|
| MoveTo() | Takes XPathNavigator as a parameter. Moves the current position to be the same as that passed in to XPathNavigator. |
| MoveToAttribute() | Moves to the named attribute. Takes the attribute name and namespace as parameters. |
| MoveToFirstAttribute() | Moves to the first attribute in the current element. Returns true if successful. |
| MoveToNextAttribute() | Moves to the next attribute in the current element. Returns true if successful. |
| MoveToFirst() | Moves to the first sibling in the current node. Returns true if successful. |
| MoveToLast() | Moves to the last sibling in the current node. Returns true if successful. |
| MoveToNext() | Moves to the next sibling in the current node. Returns true if successful. |
| MoveToPrevious() | Moves to the previous sibling in the current node. Returns true if successful. |
| MoveToFirstChild() | Moves to the first child of the current element. Returns true if successful. |
| MoveToId() | Moves to the element with the ID supplied as a parameter. There needs to be a schema for the document, and the data type for the element must be of type ID. |
| MoveToParent() | Moves to the parent of the current node. Returns true if successful. |
| MoveToRoot() | Moves to the root node of the document. |

To select a subset of the document, you can use one of the Select methods listed in the following table.

| METHOD NAME | DESCRIPTION |
|---|---|
| Select() | Selects a node set using an XPath expression. |
| SelectAncestors() | Selects all the ancestors of the current node based on an XPath expression. |
| SelectChildren() | Selects all the children of the current node based on an XPath expression. |
| SelectDescendants() | Selects all of the descendants of the current node based on an XPath expression. |
| SelectSingleNode() | Selects one node based on an XPath expression. |

If the XPathNavigator was created from an XPathDocument, it is read-only. If it is created from an XmlDocument, the XPathNavigator can be used to edit the document. This can be verified by checking the CanEdit property. If it is true, you can use one of the Insert methods. InsertBefore and InsertAfter will create a new node either before or after the current node. The source of the new node can be from an XmlReader or a string. Optionally, an XmlWriter can be returned and used to write the new node information.

Strongly typed values can be read from the nodes by using the ValueAs properties. Notice that this is different from XmlReader, which used ReadValue methods.

## XPathNodeIterator

XPathNodeIterator can be thought of as the equivalent of a NodeList or a NodeSet in XPath. This object has two properties and three methods:

- Clone() — Creates a new copy of itself
- Count — Number of nodes in the XPathNodeIterator object
- Current — Returns an XPathNavigator pointing to the current node
- CurrentPosition() — Returns an integer with the current position
- MoveNext() — Moves to the next node that matches the XPath expression that created the XPathNodeIterator

The XPathNodeIterator is returned by the XPathNavigator Select methods. You use it to iterate over the set of nodes returned by a Select method of the XPathNavigator. Using the MoveNext method of the XPathNodeIterator does not change the location of the XPathNavigator that created it.

## Using Classes from the XPath Namespace

The best way to see how these classes are used is to look at some code that iterates through the books.xml document. This will allow you to see how the navigation works. In order to use the examples, you first add a reference to the System.Xml.Xsl and System.Xml.XPath namespaces:

using System.Xml.XPath;
using System.Xml.Xsl;

For this example, you use the file bookxpath.xml. It is similar to the books.xml file that you have been using, except that there are a couple of extra books added. Here's the form code, which is part of the XmlSample project:

```
private void button1_Click(object sender, EventArgs e)
{
    //modify to match your path structure
    XPathDocument doc = new XPathDocument("books.xml");
    //create the XPath navigator
    XPathNavigator nav = ((IXPathNavigable)doc).CreateNavigator();
    //create the XPathNodeIterator of book nodes
    //that have genre attribute value of novel
    XPathNodeIterator iter = nav.Select("/bookstore/book[@genre='novel']");
    textBox1.Text = "";
    while (iter.MoveNext())
    {
        XPathNodeIterator newIter =
            iter.Current.SelectDescendants(XPathNodeType.Element, false);
        while (newIter.MoveNext())
        {
            textBox1.Text += newIter.Current.Name + ": " +
                newIter.Current.Value + "\r\n";
        }
    }
}
```

The first thing you do in the button1_Click() method is create the XPathDocument (called doc), passing in the file and path string of the document you want opened. The next line is where the XPathNavigator is created:

```
XPathNavigator nav = doc.CreateNavigator();
```

In the example, you can see that you use the Select() method to retrieve a set of nodes that all have novel as the value of the genre attribute. You then use the MoveNext() method to iterate through all of the novels in the book list.

To load the data into the list box, you use the XPathNodeIterator.Current property. This creates a new XPathNavigator object based on just the node that the XPathNodeIterator is pointing to. In this case, you are creating an XPathNavigator for one book node in the document.

The next loop takes this XPathNavigator and creates another XPathNodeIterator by issuing another type of select method, the SelectDescendants() method. This gives you an XPathNodeIterator of all of the child nodes and children of the child nodes of the book node.

Then, you do another MoveNext() loop on the XPathNodeIterator and load the text box with the element names and element values.

Figure 33-2 shows what the screen looks like after running the code. Note that novels are the only books listed now.

![](img/d7d2ffa0a76feaab821930e95daace93_981_0.png)

FIGURE 33-2

What if you wanted to add up the cost of these books? XPathNavigator includes the Evaluate() method for just this reason. Evaluate() has three overloads. The first one contains a string that is the XPath function call. The second overload uses the XPathExpression object as a parameter, and the third uses XPathExpression and an XPathNodeIterator as parameters. The following code is similar to the previous example, except that this time all of the nodes in the document are iterated through. The Evaluate method call at the end totals up the cost of all of the books:

```
private void button2_Click(object sender, EventArgs e)
{
    //modify to match your path structure
    XPathDocument doc = new XPathDocument("books.xml");
    //create the XPath navigator
    XPathNavigator nav = ((IXPathNavigable)doc).CreateNavigator();
    //create the XPathNodeIterator of book nodes
    XPathNodeIterator iter = nav.Select("/bookstore/book");
    textBox1.Text = "";
    while (iter.MoveNext())
    {
        XPathNodeIterator newIter =
            iter.Current.SelectDescendants(XPathNodeType.Element, false);
        while (newIter.MoveNext())
        {
            textBox1.Text += newIter.Current.Name + ": " + newIter.Current.Value +
                "\r\n";
        }
    }
    textBox1.Text += "=================" + "\r\n";
    textBox1.Text += "Total Cost = " +
        nav.Evaluate("sum(/bookstore/book/price)");
}
```
