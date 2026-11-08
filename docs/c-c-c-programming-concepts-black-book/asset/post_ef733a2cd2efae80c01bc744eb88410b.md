
- If the `NodeType` property is `Text`, then the method appends the name of the text by using the member variable `Value`. Now, this text generally defines the inner text of the sub-child element. Therefore, the method writes the value of the sub-child element. If we consider our example, then the sub-child node Name of the child node Book, which has the value Database Management System, is the inner text of the child node. Therefore, the text Database Management System will be appended to the text box.
- At last, it checks for the `NodeType` property `EndElement` where it simply reads the name of the end element node by using the member method Name.

Listing 20.8 shows the code snippet to read the generated XML document by using the XmlTextReader object:

### Listing 20.8: Reading the XMLDocument by using the XmlTextReader Object

```csharp
protected void Page_Load(object sender, EventArgs e)
{
    string path = @"C:\XML\MyFirstXML.xml";

    FileStream fileStream = new FileStream
                (path, FileMode.Open, FileAccess.Read);

    XmlTextReader xmlTextReader = new XmlTextReader(fileStream);
    int startElementCount = 0, endElementCount = 0,
        startChildElementCount = 0,
        endChildElementCount = 0, childElementTextCount = 0;
    while (xmlTextReader.Read())
    {
        if(xmlTextReader.NodeType.ToString() == "XmlDeclaration")
        {
            string xmlDeclaration = xmlTextReader.Name.ToString()
                + " = " + xmlTextReader.Value.ToString();
            txtXMLText.Text += "XML Declaration: " + xmlDeclaration + "\n";
        }

        if (xmlTextReader.NodeType.ToString() == "Element")
        {
            startElementCount += 1;
            if (startElementCount == 1)
            {
                txtXMLText.Text += "Root Element: "
                    +xmlTextReader.Name.ToString() +
                    GetAttributeList(xmlTextReader) + "\n";
            }

            else if (xmlTextReader.Name.ToString() != string.Empty)
            {
                startChildElementCount += 1;

                if (startChildElementCount == 1)
                {
                    txtXMLText.Text += "    Child Element : "
                        + xmlTextReader.Name.ToString() + "\n";

                    string attributeList = GetAttributeList(xmlTextReader);

                    if (attributeList != string.Empty)
                    {
                        txtXMLText.Text += "    Child Element Attribute List: "
                            + attributeList + "\n";
                    }
                }
                else
                {
                    txtXMLText.Text += "  Sub Child Element :  "
                        + xmlTextReader.Name.ToString() + "\n";
                    string childAttributeList = GetAttributeList(xmlTextReader);

                    if (childAttributeList != String.Empty)
                    {
                        txtXMLText.Text += "  Sub Child Element Attribute List:  " + childAttributeList + "\n";
                    }
                }
            }
        }

        if (xmlTextReader.NodeType.ToString() == "Text")
        {
            childElementTextCount += 1;
            txtXMLText.Text += "  Sub Child Element Text:  "
                + xmlTextReader.Value + "\n";
        }

        if (xmlTextReader.NodeType.ToString() == "EndElement")
        {
            startElementCount -= 1;
            endElementCount = startElementCount;
            endChildElementCount = childElementTextCount;

            if (endElementCount == 0)
            {
                txtXMLText.Text += "Root End Element:  "
                    + xmlTextReader.Name.ToString() + "\n";
            }
            else if (endChildElementCount == 0)
            {
                txtXMLText.Text += "  Child End Element:  "
                    + xmlTextReader.Name.ToString() + "\n";
            }
            else
            {
                txtXMLText.Text += "  Sub Child End Element:  "
                    + xmlTextReader.Name.ToString() + "\n\n";
            }
            childElementTextCount = 0;
        }
    }
}
```

Figure 20.11 shows the content of the XML document on the Web page:

![](img/43c5f409f9b17790a628c4b4df854b61_706_0.png)

**Figure 20.11: Showing the XML Content of the Newly Created XML Document**

In Figure 20.11, we can observe the Back button provided at the bottom of the Web page. This button is used to navigate back to the main page. In other words, the parent page will be loaded again on the click of the Back button. Listing 20.9 provides the code snippet for the Back button.

### Listing 20.9: Showing the functionality of the Back button

```csharp
public void btnBack_Click(object sender, EventArgs e)
{
    Response.Redirect("MyXMLManager.aspx", true);
}
```

Figure 20.12 shows the state of the Web page after clicking the Back button:

![](img/43c5f409f9b17790a628c4b4df854b61_706_1.png)

**Figure 20.12: Showing the State of the Web Page after Clicking the Back Button**

Let’s now create an XML document using the XmlDocument class.

## The Create XML using XML Document Button

When we click the Create XML using XML Document button, it creates another XML document but with the help of XmlDocument object. This functionality follows the same steps that we have discussed in the previous section to create an XMLDocument using the XmlTextWriter object. However, in this case, we need to take care of the insertion of XML nodes in the document.

Perform the following steps to create an XML document:

- 1. Create an object of `XmlDeclaration` and assign it the XML declaration text using the `CreateXmlDeclaration()` method. Then, create an object of `XmlElement` and assign it the root element (LIBRARY) by using the `CreateElement()` method. After that, insert the `XmlDeclaration` object before the `XmlElement` object and the `XmlElement` object after the `XmlDeclaration` object by using the `InsertBefore()` and `InsertAfter()` methods, respectively. This is important as it keeps the XML document in the correct format.
- 2. Add the child element by using the `CreateElement()` method, which returns an object of `XmlElement`. Then, append the child element to the root element by using the `AppendChild()` method.
- 3. Add the attributes to the child element. For this, create an object of `XmlAttribute` by using the `CreateAttribute()` method and specify the name of an attribute. Next, assign the value to that attribute and set it as the attribute of the child element by using the `SetAttributeNode()` method. Depending on the number of attributes provided by an user, the same procedure is repeated each time.
- 4. Add the sub-child elements. For this, create an object of `XmlElement` by using the `CreateElement()` method, where we specify the name of the sub-child element. Next, we set the `InnerText` of the sub-child element by assigning its value. At the end, append this sub-child element as the sub-child of the child element by using the `AppendChild()` method.
- 5. Save the XML document to the specified path by using the `Save()` method.

Listing 20.10 provides the code snippet to create an XML Document by using the XmlDocument object:

### Listing 20.10: Creating an XMLDocument by using the XmlDocument Object

```csharp
protected void btnCreateXML_Click(object sender, EventArgs e)
{
    //Creating an XmlDocument object
    XmlDocument doc = new XmlDocument();

    //Declaring the xml declaration object that are going to use to build the xml
    XmlDeclaration declaration;

    //Declaring the Xml elements that are going to use to build the xml
    XmlElement rootElement, childElement;

    //declaring the XmlElements that refers to the sub-child
    XmlElement subChild1, subChild2, subChild3;

    //Declaring the attributes of the element
    XmlAttribute attr1, attr2, attr3;

    try
    {
        //Adding the Xml declaration
        declaration = doc.CreateXmlDeclaration("1.0", "utf-8", "yes");
        doc.InsertBefore(declaration, doc.DocumentElement);
```

![](img/43c5f409f9b17790a628c4b4df854b61_710_0.png)

Figure 20.14: Showing the XML Document

In the next section, let's now learn about XSD.

## XSD

Similar to the database schema definition, XSD defines a schema structure for an XML document. XSD also defines a set of allowable elements and their types that can be incorporated in a valid XML document.

XSD has evolved as a replacement to DTD, which is W3C's first attempt to data validation. The need for such a replacement arose due to the following problems:

- It uses the syntax known as Extended Backus-Naur Form, which is not similar to XML syntax.
- It does not use a human reader approach. We need to have profound knowledge before using DTD.
- Its metadata is programmatically difficult to consume.
- It cannot be inherited.

These drawbacks of DTD led the W3C developers to design a schema definition language whose syntaxes are familiar to the XML syntax and use a human readable format. This new validating mechanism provides the same feature of DTDs but offers much more flexibilities.

In this section, let's create and save an XSD file with an extension .xsd. This XSD file can be used to validate the XML document for Library Management System; however, the full description of XSD is out of scope of this chapter. Listing 20.11 shows the MyFirstXML.xsd file:

### Listing 20.11: Showing the Code of the MyFirstXML.xsd File

```xml
<?xml version="1.0" encoding="utf-8"?>
<xs:schema id ="MyFirstXML" attributeFormDefault="unqualified"
   elementFormDefault="qualified" xmlns:xs="http://www.w3.org/2001/XMLSchema">
   <xs:element name="LIBRARY">
      <xs:complexType>
         <xs:sequence>
            <xs:element name="BOOK">
               <xs:complexType>
                  <xs:sequence>
                     <xs:element name="NAME" type="xs:string" />
                     <xs:element name="AUTHOR" type="xs:string" />
                  </xs:sequence>
```
