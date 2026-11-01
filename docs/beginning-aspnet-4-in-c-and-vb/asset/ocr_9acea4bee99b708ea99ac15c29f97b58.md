```
class Class1
{
    static void Main()
    {
        XNamespace ns1 = "http://www.lipperweb.com/ns/root";
        XNamespace ns2 = "http://www.lipperweb.com/ns/sub";

        XElement xe = new XElement(ns1 + "Company",
            new XElement(ns2 + "CompanyName", "Lipper"),
            new XElement(ns2 + "CompanyAddress",
                new XElement(ns2 + "Address", "123 Main Street"),
                new XElement(ns2 + "City", "St. Louis"),
                new XElement(ns2 + "State", "MO"),
                new XElement(ns2 + "Country", "USA")));

        Console.WriteLine(xe.ToString());
        Console.ReadLine();
    }
}
```

code download ConsoleApplication1.sln

This produces the results shown in Figure 33-9.

![](bbox=[0.15, 0.57, 0.65, 0.78])

# FIGURE 33-9

In this case, you can see that the subnamespace was applied to everything you specified except for the <Address>, <City>, <State>, and the <Country> elements because they inherit from their parent, <CompanyAddress>, which has the namespace declaration.

# XComment

The XComment object allows you to easily add XML comments to your XML documents. The following example shows the addition of a comment to the top of the document:

```
using System;
using System.Linq;
using System.Xml.Linq;

namespace ConsoleApplication1
{
    class Class1
    {
        static void Main(string[] args)
        {
            XDocument xdoc = new XDocument();
            XComment xc = new XComment("Here is a comment.");
```