# XNamespace

The XNamespace is an object that represents an XML namespace and is easily applied to elements within your document. For instance, you can take the previous example and easily apply a namespace to the root element:

```
using System;
using System.Linq;
using System.Xml.Linq;

namespace ConsoleApplication1
{
    class Class1
    {
        static void Main()
        {
            XNamespace ns = "http://www.lipperweb.com/ns/1";

            XElement xe = new XElement(ns + "Company",
                new XElement("CompanyName", "Lipper"),
                new XElement("CompanyAddress",
                    new XElement("Address", "123 Main Street"),
                    new XElement("City", "St. Louis"),
                    new XElement("State", "MO"),
                    new XElement("Country", "USA")));

            Console.WriteLine(xe.ToString());
            Console.ReadLine();
        }
    }
}
```

code download ConsoleApplication1.sln

In this case, an XNamespace object is created by assigning it a value of http://www.lipperweb.com/ns/1. From there, it is actually used in the root element <Company> with the instantiation of the XElement object:

```
XElement xe = new XElement(ns + "Company", // .
```

This produces the results illustrated in Figure 33-8.

![](bbox=[0.15, 0.7, 0.7, 0.88])

FIGURE 33-8

In addition to dealing with only the root element, you can also apply namespaces to all your elements, as shown in the following example:

```
using System;
using System.Linq;
using System.Xml.Linq;

namespace ConsoleApplication1
```