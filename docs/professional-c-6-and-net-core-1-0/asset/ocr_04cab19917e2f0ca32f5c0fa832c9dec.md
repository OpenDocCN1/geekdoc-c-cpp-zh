This produces the following results:

```
root name: PLAY
has root attributes? False
```

Another important member to be aware of is the Save method, which, like the Load method, enables you to save to a physical disk location or to a TextWriter or XmlWriter object:

```
XDocument doc = XDocument.Load(HamletFileName);
doc.Save(SaveFileName);
```

# XElement

One object that you will work with frequently is the XElement object. With XElement objects, you can easily create single-element objects that are XML documents themselves, as well as fragments of XML. You can use the Load method with the XElement similarly to how you use the Load method with the XDocument. The following code snippet shows writing an XML element with its corresponding value to the console:

```
var company = new XElement("Company","Microsoft Corporation");
WriteLine(company);
```

In the creation of an XElement object, you can define the name of the element as well as the value used in the element. In this case, the name of the element is <Company>, and the value of the <Company> element is Microsoft Corporation. Running this in a console application produces the following result:

```
<Company>Microsoft Corporation</Company>
```

You can create an even more complete XML document using multiple XElement objects, as shown in the following example (code file LinqToXmlSample/Program.cs):

```
public static void CreateXml()
{
    var company =
        new XElement("Company",
            new XElement("CompanyName","Microsoft Corporation"),
            new XElement("CompanyAddress",
                new XElement("Address","One Microsoft Way"),
                new XElement("City","Redmond"),
                new XElement("Zip","WA 98052-6399"),
                new XElement("State","WA"),
                new XElement("Country","USA")));

    WriteLine(company);
}
```

What’s extremely nice with this API is that the hierarchy of the XML is represented by the API. The first instantiation of the XElement passes the string “Company” to the first parameter. This parameter is of type XName that represents the name of the XML element. The second parameter is another XElement. This second XElement defines the XML child element of the Company. This second element defines