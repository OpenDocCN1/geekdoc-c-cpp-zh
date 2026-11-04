
```
{
    return _dateCreated;
}
public string URL { get; set; }
public string Description { get; set; }
public BookMark NextURL { get; set; }
}
```

The dateCreated variable will not be serialized. Figure 11-14 shows that when the dateCreated variable is not serialized, its value is set to the default date when the object is deserialized.

![](img/a977a875c7c627b45d939729705a252e_388_0.png)

## XML Serialization

You can also serialize an object into an XML document. There are many advantages to XML serialization. For instance, XML documents are platform-agnostic because they are in plain text format and that makes cross-platform communication quite easy. XML documents are also easy to read and modify, which makes XML a very flexible format for data representation.

The following example illustrates XML serialization and shows you some of its uses.

## Defining a Sample Class

Let's define a class so that you can see how XML serialization works. For this example, you define three classes that allow you to store information about a person, such as name, address, and date of birth. Here are the class definitions:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Microsoft.VisualBasic;
using System.IO;
using System.Xml.Serialization;
using System.Xml;
```

```
namespace Serialization
{
    class Program
    {
        static void Main(string[] args)
```

## Part I: C# Fundamentals

*(continued)*

```csharp
{
}
public class Member
{
    private int age;
    public MemberName Name;
    public MemberAddress[] Addresses;
    public DateTime DOB;
    public int currentAge
    {
        get
        {
            //---add a reference to Microsoft.VisualBasic.dll---
            age = (int)DateAndTime.DateDiff(
                DateInterval.Year, DOB,
                DateTime.Now,
                FirstDayOfWeek.System,
                FirstWeekOfYear.System);
            return age;
        }
    }
}

public class MemberName
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

public class MemberAddress
{
    public string Line1;
    public string Line2;
    public string City;
    public string Country;
    public string Postal;
}
}
```

> The various classes are deliberately designed to illustrate the various aspects of XML serialization. They may not adhere to the best practices for defining classes.

Here are the specifics for the classes:

- The Member class contains both private and public members. It also contains a read-only property.
- The Member class contains a public array containing the address of a Member.
- The Member class contains a variable of Date data type.
- The MemberName class contains two properties.
- The MemberAddress class contains only public members.

## Serializing the Class

To serialize a Member object into a XML document, you can use the XMLSerializer class from the System.Xml.Serialization namespace:

```csharp
static void Main(string[] args)
{
}
```

```csharp
//=======XML.Serialization========
static void XMLSerialize(Member mem)
{
    StreamWriter sw = new StreamWriter(@"c:\Members.xml");
    try
    {
        XmlSerializer s = new XmlSerializer(typeof(Member));
        s.Serialize(sw, mem);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
    }
    finally
    {
        sw.Close();
    }
}
```

For XML serialization, you need to import the System.Xml.Serialization namespace.

In the XMLSerialize() function, you first create a new StreamWriter object so that you can save the serialized XML string to a file. The Serialize() method from the XMLSerializer class serializes the Member object into an XML string, which is then written to file by using the StreamWriter class.

## Part I: C# Fundamentals

To test the XMLSerialize() function, assume that you have the following object declarations:

```csharp
static void Main(string[] args)
{
    MemberAddress address1 = new MemberAddress()
    {
        Line1 = "One Way Street",
        Line2 = "Infinite Loop",
        Country = "SINGAPORE",
        Postal = "456123"
    };
    MemberAddress address2 = new MemberAddress()
    {
        Line1 = "Two Way Street",
        Country = "SINGAPORE",
        Postal = "456123"
    };
    Member m1 = new Member()
    {
        Name = new MemberName()
        {
            FirstName = "Wei-Meng",
            LastName = "Lee"
        },
        DOB = Convert.ToDateTime(@"5/1/1972"),
        Addresses = new MemberAddress[] { address1, address2 }
    };
}
```

To serialize the Member object, invoke the XMLSerialize() method like this:

```csharp
static void Main(string[] args)
{
    MemberAddress address1 = new MemberAddress()
    {
        Line1 = "One Way Street",
        Line2 = "Infinite Loop",
        Country = "SINGAPORE",
        Postal = "456123"
    };
    MemberAddress address2 = new MemberAddress()
    {
        Line1 = "Two Way Street",
        Country = "SINGAPORE",
        Postal = "456123"
    };
    Member m1 = new Member()
    {
        Name = new MemberName()
        {
```

```csharp
FirstName = "Wei-Meng",
LastName = "Lee"
},
DOB = Convert.ToDateTime(@"5/1/1972"),
Addresses = new MemberAddress[] { address1, address2 }
};

XMLSerialize(m1);
}
```

Figure 11-15 shows the XML document generated by the XMLSerialize() function.

![](img/a977a875c7c627b45d939729705a252e_392_0.png)

Figure 11-15

As you can see, the object is serialized into an XML document with a format corresponding to the structure of the object. Here are some important points to note:

- The City information is not persisted in the XML document (nor as the line2 in the second Address element) because it was not assigned in the objects. You will see later how to persist empty elements, even though a value is not assigned.
- All read/write properties in the object are persisted in the XML document, except the read-only currentAge property in the Member class.
- Only public variables are persisted; private variables are not persisted in XML serialization.
- The default name for each element in the XML document is drawn from the variable (or class) name. In most cases this is desirable, but sometimes the element names might not be obvious.

## Deserializing the Class

To deserialize the XML document, simply use the Deserialize() method from the XMLSerializer class. Define the XMLDeserialize() function as follows:

```csharp
static void Main(string[] args)
{
    //...
}
```

```csharp
//=======XML Serialization========
static Member XMLDeserialize(string xmlFile)
{
    Member obj;
    XmlReader xr = XmlReader.Create(xmlFile);
    try
    {
        XmlSerializer s = new XmlSerializer(typeof(Member));
        obj = (Member)s.Deserialize(xr);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
        obj = null;
    }
    finally
    {
        xr.Close();
    }

    return obj;
}
```

Here, you can use the XmlReader class's Create() method to open an XML file for reading. The XmlReader class is used to read the data from the XML file. The deserialized object is then returned to the calling function.

> Remember to import the System.Xml namespace for the XmlReader class.

To test the XMLDeserialize() function, call it directly after an object has been serialized, like this:

```csharp
static void Main(string[] args)
{
    MemberAddress address1 = new MemberAddress()
    {
        Line1 = "One Way Street",
        Line2 = "Infinite Loop",
        Country = "SINGAPORE",
        Postal = "456123"
    };
```

```csharp
};
MemberAddress address2 = new MemberAddress()
{
    Line1 = "Two Way Street",
    Country = "SINGAPORE",
    Postal = "456123"
};

Member m1 = new Member()
{
    Name = new MemberName()
    {
        FirstName = "Wei-Meng",
        LastName = "Lee"
    },
    DOB = Convert.ToDateTime("5/1/1972"),
    Addresses = new MemberAddress[] { address1, address2 }
};

XMLSerialize(m1);
```

```csharp
Member m2 = XMLDeserialize(@"c:\Members.xml");

Console.WriteLine("{0}, {1}", m2.Name.FirstName, m2.Name.LastName);
Console.WriteLine("{0}", m2.currentAge);
foreach (MemberAddress a in m2.Addresses)
{
    Console.WriteLine("{0}", a.Line1);
    Console.WriteLine("{0}", a.Line2);
    Console.WriteLine("{0}", a.Country);
    Console.WriteLine("{0}", a.Postal);
    Console.WriteLine();
}
Console.ReadLine();
}
```

The output of these statements is shown in Figure 11-16.

![](img/a977a875c7c627b45d939729705a252e_394_0.png)

Figure 11-16
