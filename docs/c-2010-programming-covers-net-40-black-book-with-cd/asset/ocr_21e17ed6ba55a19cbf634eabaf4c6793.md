6. Double-click the button1 and add the following code snippet:

```
private void button1_Click(object sender, EventArgs e) {
    listBox1.Items.Clear();
    XPathDocument pd = new XPathDocument("authors.xml");
    XPathNavigator pn = ((IXPathNavigable)pd).CreateNavigator();
    XPathNodeIterator ni = pn.Select("/authorslist/authors[@au_id='409-56-7008']");
    while(ni.MoveNext())
    {
        XPathNodeIterator newni = ni.Current.SelectDescendants(XPathNodeType.Element, false);
        while(newni.MoveNext())
        {
            listBox1.Items.Add(newni.Current.Name + ": " + newni.Current.Value);
        }
    }
}
```

In the preceding code snippet, we have created a blank list box. Then, we have created an object of the XPathDocument class by passing it the name of the XML file (authors.xml) as a parameter. Note that the authors.xml file is already placed in the bin\Debug folder of the project, so the location of the XML file will be detected by the application automatically. Next, we have created an object of the XPathNavigator class by first casting the XPathDocument object to the IXPathNavigable interface and then calling the CreateNavigator() method of the IXPathNavigable interface.

After that, we have created an object of the XPathNodeIterator class by calling the Select() method of the XPathNavigator object. The Select() method returns all the authors elements for which the value of the attribute au_id is 409-56-7008. The nodes of the XML document are then traversed using the MoveNext() method of the XPathNodeIterator object in a while loop. Inside the loop, we have created an object of the XPathNavigator class, which is the child element of the current element. We have again traversed the nodes of the XML document by using the MoveNext() method of the XPathNodeIterator object in another while loop. Inside the loop, the text value for the element is added to the list box.

7. Press the F5 key to run the XMLElementsNavigation application. In the output, when you click the Find Elements button, all elements with the specified attribute value are added to the list box, as shown in Figure 30.7:

![](bbox=[0.33, 0.64, 0.71, 0.89])

Figure 30.7: Displaying the Output of the XMLElementsNavigation Application