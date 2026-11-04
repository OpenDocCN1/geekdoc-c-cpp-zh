The XmlReader class provides a forward-only, read-only interface for reading XML data. It is suitable for reading large XML documents where memory efficiency is crucial. Here's an example of how to use the XmlReader class to read XML data from a file:

```
```csharp
using (XmlReader reader = XmlReader.Create("data.xml"))
{
    while (reader.Read())
    {
        if (reader.NodeType == XmlNodeType.Element && reader.Name == "Employee")
        {
            string name = reader.GetAttribute("Name");
            int age = int.Parse(reader.GetAttribute("Age"));
            // Process the employee data
        }
    }
}
```
```

In this example, we're using the XmlReader class to read XML data from the "data.xml" file. We're iterating through the XML elements and extracting the "Name" and "Age" attributes of each "Employee" element.

# **Writing XML Data with XmlWriter**

The XmlWriter class provides a forward-only, write-only interface for writing XML data. It is suitable for generating XML data on-the-fly. Here's an example of how to use the XmlWriter class to write XML data to a file:

```
```csharp
using (XmlWriter writer = XmlWriter.Create("output.xml"))
{
    writer.WriteStartDocument();
    writer.WriteStartElement("Employees");
```
```