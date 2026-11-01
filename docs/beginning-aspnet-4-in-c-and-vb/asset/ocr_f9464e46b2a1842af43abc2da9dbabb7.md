```
```csharp
connection.Open();
var reader = command.ExecuteReader(CommandBehavior.CloseConnection);
while (reader.Read())
{
    SqlXml xml = reader.GetSqlXml(2);
    var doc = new XmlDocument();
    doc.LoadXml(xml.Value);

    XmlNode examNode = doc.SelectSingleNode("//Exam");
    Console.WriteLine("Exam: {0}", examNode.Attributes["Number"].Value);
    XmlNode titleNode = examNode.SelectSingleNode("./Title");
    Console.WriteLine("Title: {0}", titleNode.InnerText);
    Console.Write("Course(s): ");

    foreach (XmlNode courseNode in examNode.SelectNodes("./Course"))
    {
        Console.Write("{0} ", courseNode.InnerText);
    }
    Console.WriteLine();
}
reader.Close();
```
```

code snippet XmlSamples/Program.cs

> > The XmlReader and XmlDocument classes are discussed in Chapter 33, "Manipulating XML."

With .NET 4 there’s another option to access the XML column from the database. You can combine LINQ to SQL and LINQ to XML, which makes the programming code smaller.

You can use the ADO.NET Entity Framework designer by selecting the ADO.NET Entity Data Model template from the Data templates category. Name the file ExamsModel.edmx to create a mapping for the database SqlServerSample. Select the Exams table and select the option to singularize object names. After you create the model with the wizard, a design surface, as shown in Figure 34-4, opens.

The data context class that is created by the designer has the name ExamsEntities and defines a property Exams to return all exam rows. Here a foreach statement is used to iterate through all records. Of course you can also define a LINQ query with a where expression if not all records are required. The Exam class defines the properties Id, Number, and Info according to the columns in the database table. The Info property is of type string. With the XElement class the string can be parsed and accessed by the LINQ to XML classes from the namespace System.Xml.Linq. Invoking the method Element() passing the name of the XML element Exam returns an XElement object that is then used to access the values of the attribute Number and the elements Title and Course in a much simpler way, as was done earlier with the XmlDocument class:

![](bbox=[0.68, 0.6, 0.92, 0.85])

FIGURE 34-4

```
```csharp
using System;
using System.Xml.Linq;

namespace Wrox.ProcSharp.SqlServer
{
```
```