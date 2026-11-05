By default, elements in the XML output are named after the properties or fields that they are based on.

The root node can be renamed using the XmlRoot attribute, and change the name of child nodes by using the XmlElement attribute and setting its ElementName.

Multiple properties can be specified for an attribute by separating them with commas within the parenthesis. This usually takes the form [atributename(property1=value1, property2=value2...)]

```
[XmlRoot("XTest")]
public class Test
{
    [XmlElement(ElementName="V1")]
    public String value1;

    [XmlElement("V2")]
    public String value2;
}
```

Note that when specifying the element name, the property name can be omitted.

# 17.5 XML Schema

+   1. While an XML file might conform to the XML specification, it might not be a valid form of a particular dialect. An XML schema help to verify that certain elements are present, while making sure that the values presented are of the correct type.
+   2. There are a few different specifications of schemas: XSD, DTD, and X SX. Though DTD (Document Type Definition) is the most common schema used today, XSD (XML Schema Definition) is a newer standard that's gaining acceptance, as it provides the finest grained control for XML validation.
+   3. XML Schema is commonly known as XML Schema Definition (XSD) which is used to describe and validate the structure and the content of XML data.
+   4. XML schema defines the elements, attributes and data types.
+   5. Schema element supports Namespaces. It is similar to a database schema that describes the data in a database.
+   6. The basic idea behind XML Schemas is that they describe the legitimate format that an XML document can take.
+   7. Syntax
+      - Declare a schema in XML document as,

```
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
```