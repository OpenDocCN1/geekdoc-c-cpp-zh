# SQL Server Database Programming with C#

```
A faculty.Element("phone").Remove();
 faculty.Elements("phone").Remove();
 faculties.Element("faculty").Element("office").RemoveNodes();\ faculty.SetElement("phone", null);
```

FIGURE 4.51 Some sample codes of using LINQ to XML to delete XML.

Attributes have a symmetric method call SetAttribute(), which has the similar functionality as SetElement().

# 4.8.2. Delete XML

To delete elements, navigate to the content where you want to delete and call the Remove()method. For example, if you want to delete the first phone number for a faculty, entering the following code that is shown in section A in Figure 4.51.

The Remove()method also works over an Xumerable, you could delete all of the phone numbers for a faculty in one call that is shown in section B in Figure 4.51.

You can also remove the content of an XElement by using the RemoveNodes() method. For example, you could remove the content of the faculty's first office with the statement that is shown in section C in Figure 4.51.

Another way to remove an element is to set it to null using the SetElement() method, which we talked about in the last section, Update XML. An example is shown in section D in Figure 4.51.

# 4.8.3 MANIPULATE XML ATTRIBUTES

There is substantial symmetry between working with XElement and XAttribute classes. However, in the LINQ to XML hierarchy, XElement and XAttribute are distinct and do not derive from a common base class. This is because X attributes are not nodes in the XML tree; they are unordered name/value pairs associated with an X element. LINQ to XML makes this distinction; in practice, working with XAttribute is quite similar to working with XElement due to the nature of an XML attribute, where they diverge understandable.

# 4.8.3.1 Add XML Attributes

Adding an XAttribute is very similar to adding a simple XElement. In the XML that is shown in Figure 4.52, notice that each phone number has a type attribute that states this is a home, work, or mobile phone number.

You can create X using functional construction the same way you would create an XElement with a simple type. To create a faculty using functional construction, enter the following code that are shown in Figure 4.53.

Just as you use the SetElement() method to update, add, or delete elements with simple types, you can do the same using the SetAttribute(XName, object) method on XElement. If the attribute exists,

```
<faculties>
<faculty>
  <faculty_name>Patrick Tones</faculty_name>
  <phone type="home">750-555-0144</phone>
  <phone type="work">750-555-0145</phone>
</faculty>
```

FIGURE 4.52 A sample XML attributes.