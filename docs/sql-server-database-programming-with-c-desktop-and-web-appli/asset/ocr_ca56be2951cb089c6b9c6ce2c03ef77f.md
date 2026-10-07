# Introduction to Language Integrated Query (LINQ)

```
XElement faculty = new XElement("faculty",
new XElement("faculty_name", "Patrick Tones"),
new XElement("phone",
 XAttribute("type", "home"),
"750-555-0145")
new XElement("phone",
new XAttribute("type", "work"),
"750-555-0145"));
```

FIGURE 4.53 A sample code to create an XAttribute.

will be updated. If the attribute does not exist, it will be added.

# 4.8.3.2 Get XML Attributes

The primary method for accessing an XAttribute is by using the Attribute(XName) method on XElement. For example, to use the type attribute to obtain the contact's home phone number, one can use the following piece of code that are shown in section A Figure 4.54.
Notice that the Attribute(XName) works similarly to the Element(XName) method. Also, notice that there are explicit cast operators, which lets you cast an XAttribute to a variety of simple types.

# 4.8.3.3 Delete XML Attributes

If you want to delete an attribute you can Remove() or SetAttribute(XName, object) method, passing null as the value of object. For example, to delete the type attribute from the first phone using the Remove() method, use the code that is shown in section B Figure 4.54.
Alternatively you can use the SetAttribute() method with a null argument to perform the deleting operation. An example code is shown in section C Figure 4.54.
We have provided a detailed discussion about the basic components of manipulating XML elements, and now, let's go a little deep on the query XML with LINQ to XML.

# 4.8.4 QUERY XML WITH LINQ TO XML

The major differentiator of LINQ to XML and other in-memory XML programming APIs is Language-Integrated Query (LINQ). LINQ provides a consistent query experience across different data models and the ability to mix and match data models within a single query. This section describes how to use Language-Integrated Query with XML. The following section contains a few examples of using Language-Integrated Query across data models.
Standard query operators perform a complete query for IEnumerable<T>. Standard query operators expose methods on objects that implement IEnumerable<T> and can be invoked by any other method. This approach, calling query methods, can be referred to

FIGURE 4.54 A sample code to get and delete a XAttribute.