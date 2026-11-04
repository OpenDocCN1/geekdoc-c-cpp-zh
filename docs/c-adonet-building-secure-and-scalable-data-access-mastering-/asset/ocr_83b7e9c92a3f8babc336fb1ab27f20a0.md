```
{
    Console.WriteLine($"Name: {employee.Name}, Age: {employee.Age}");
}
```

In this example, we're using LINQ to XML to query XML data from the "data.xml" file. We're selecting all "Employee" elements, extracting the "Name" and "Age" attributes, and projecting them into an anonymous type.

# Manipulating XML Data with LINQ to XML

LINQ to XML also allows you to manipulate XML data using a fluent API. Here's an example of how to use LINQ to XML to create and modify XML data:

```
XDocument doc = new XDocument(
    new XElement("Employees",
        new XElement("Employee",
            new XAttribute("Name", "John Doe"),
            new XAttribute("Age", "30")
        ),
        // Add more employees...
    )
);

// Modify existing employee data
XElement employee = doc.Descendants("Employee").FirstOrDefault();
if (employee != null)
{
    employee.SetAttributeValue("Age", "31");
}

doc.Save("modified_data.xml");
```