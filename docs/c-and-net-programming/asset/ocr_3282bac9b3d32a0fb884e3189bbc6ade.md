```
<LastName>Wani</LastName>
</Name>
<Name>
    <FirstName>Prakash</FirstName>
    <LastName>Deshmukh</LastName>
</Name>
</Names>
```

+   - To get all `<Name>` nodes use **XPath expression** `/Names/Name`.

The first slash means that the `<Names>` node must be a root node.

SelectNodes method returns collection `XmlNodeList` which will contain the `<Name>` nodes.

To **get value** of sub node `<FirstName>` one can simply index `XmlNode` with the node name: xmlNode["FirstName"].InnerText.

# Example

```
XmlDocument xml = new XmlDocument();
xml.LoadXml(myXmlString); // suppose that myXmlString contains
                         <Names>... </Names>"

XmlNodeList xnList = xml.SelectNodes("/Names/Name");
foreach (XmlNode xn in xnList)
{
    string firstName = xn["FirstName"].InnerText;
    string lastName = xn["LastName"].InnerText;
    Console.WriteLine("Name: {0} {1}", firstName, lastName);
}
```

# Output

```
Name: Ravindra Wani
Name: Prakash Deshmukh
```

# 2. Select XML Nodes by Attribute Value

+   - XML nodes can be selected from XML document **by attribute value**. For this, use method **XmlNode.SelectNodes** to get list of nodes selected by the XPath expression.

Consider XML file below.

```
[XML]
<Names>
    <Name type="M">Ravindra</Name>
    <Name type="F">Anu</Name>
    <Name type="M">Prakash</Name>
</Names>
```

To **get all name nodes** use XPath expression `/Names/Name`.