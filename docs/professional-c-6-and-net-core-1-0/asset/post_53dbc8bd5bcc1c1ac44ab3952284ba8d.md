
```
var overrides = new XmlAttributeOverrides();

overrides.Add(typeof(Inventory),"InventoryItems",
inventoryAttributes);

overrides.Add(typeof(BookProduct),"ISBN", bookIsbnAttributes);
overrides.Add(typeof(Product),"Discount",
productDiscountAttributes);
    return overrides;
}
```

When you run the application, the same XML content is created as before:

```
<?xml version="1.0"?>
<Inventory xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <InventoryItems>
        <Product Discount="0">
            <ProductID>100</ProductID>
            <ProductName>Product Thing</ProductName>
            <SupplierID>10</SupplierID>
            <CategoryID>0</CategoryID>
            <UnitPrice>0</UnitPrice>
            <UnitsInStock>0</UnitsInStock>
            <UnitsOnOrder>0</UnitsOnOrder>
            <ReorderLevel>0</ReorderLevel>
            <Discontinued>false</Discontinued>
        </Product>
        <Book Discount="0" Isbn="1234567890">
            <ProductID>101</ProductID>
            <ProductName>How To Use Your New Product Thing</ProductName>
            <SupplierID>10</SupplierID>
            <CategoryID>0</CategoryID>
            <UnitPrice>0</UnitPrice>
            <UnitsInStock>0</UnitsInStock>
            <UnitsOnOrder>0</UnitsOnOrder>
            <ReorderLevel>0</ReorderLevel>
            <Discontinued>false</Discontinued>
        </Book>
    </InventoryItems>
</Inventory>
```

methods offered by LINQ to Objects, LINQ to XML adds some XML specifics to this query in the `System.Xml.Linq` namespace. LINQ to XML also offers easier creating of XML content than the standards-based `XmlDocument` XML creation.

The following sections describe the objects that are available with LINQ to XML.

> **NOTE** *Many of the examples in this section use a file called `Hamlet.xml`, which you can find at http://metalab.unc.edu/bosak/xml/eg/shaks200.zip. It includes all of Shakespeare’s plays as XML files.*

The sample code makes use of the following dependencies and namespaces:

## Dependencies

- `NETStandard.Library`
- `System.Xml.XDocument`

## Namespaces

- `System`
- `System.Collections.Generic`
- `System.Linq`
- `System.Xml.Linq`
- `static System.Console`

## XDocument

The `XDocument` represents an XML document like the `XmlDocument` class, but it is easier to work with. The `XDocument` object works with the other new objects in this space, such as the `XNamespace`, `XComment`, `XElement`, and `XAttribute` objects.

One of the more important members of the `XDocument` object is the `Load` method. Here it loads the file `hamlet.xml` that is defined by the constant `HamletFileName` into memory:

```
XDocument doc = XDocument.Load(HamletFileName);
```

You can also pass a `TextReader` or `XmlReader` object into the `Load` method. From here, you can programmatically work with the XML code as shown in the following code snippet to access the name of the root element and check whether the root element has attributes (code file `LinqToXmlSample/Program.cs`):

```
XDocument doc = XDocument.Load(HamletFileName);
WriteLine($"root name: {doc.Root.Name}");
WriteLine($"has root attributes? {doc.Root.HasAttributes}");
```

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

## XElement

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

"CompanyName" as XName, and "Microsoft Corporation" as its value. The XElement specifying the company address is another child of the Company element. All the other XElement objects that follow are direct child objects of CompanyAddress. The constructor allows passing any number of objects as defined by the type params object[]. All these objects are treated as children.

Running this application produces this result:

```
<Company>
    <CompanyName>Microsoft Corporation</CompanyName>
    <CompanyAddress>
        <Address>One Microsoft Way</Address>
        <City>Redmond</City>
        <Zip>WA 98052-6399</Zip>
        <State>WA</State>
        <Country>USA</Country>
    </CompanyAddress>
</Company>
```

> NOTE The constructor syntax of XElement allows easy creation of hierarchical XML. This makes it easy to create XML out of LINQ queries (transforming object trees to XML), as is shown later in this section, and you can also transform one XML syntax to another XML syntax.

## XNamespace

XNamespace is an object that represents an XML namespace, and it is easily applied to elements within your document. For instance, you can take the previous example and easily apply a namespace to the root element by creating an XNamespace object (code file LinqToXmlSample/Program.cs):

```
public static void WithNamespace()
{
    XNamespace ns ="http://www.cninnovation.com/samples/2015";

    var company =
        new XElement(ns +"Company",
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

In this case, an XNamespace object is created by assigning it a value of http://www.cninnovation.com/samples/2015. From there, it is actually used in the root element <Company> with the instantiation of the XElement object.

This produces the following result:

```
<Company>
    <CompanyName>Microsoft Corporation</CompanyName>
    <CompanyAddress>
        <Address>One Microsoft Way</Address>
        <City>Redmond</City>
        <Zip>WA 98052-6399</Zip>
        <State>WA</State>
        <Country>USA</Country>
    </CompanyAddress>
</Company>
```

> NOTE The XNamespace allows creation by assigning a string to the XNamespace instead of using the new operator because this class implements an implicit cast operator from string. It’s also possible to use the + operator with the XNamespace object by having a string on the right side because of an implementation of the + operator that returns an XName. Operator overloading is explained in Chapter 8, “Operators and Casts.”

In addition to dealing with only the root element, you can also apply namespaces to all your elements, as shown in the following example (code file LinqToXmlSample/Program.cs):

```
public static void With2Namespace()
{
    XNamespace ns1 ="http://www.cninnovation.com/samples/2015";
    XNamespace ns2
    ="http://www.cninnovation.com/samples/2015/address";

    var company =
        new XElement(ns1 +"Company",
            new XElement(ns2 +"CompanyName","Microsoft Corporation"),
            new XElement(ns2 +"CompanyAddress",
                new XElement(ns2 +"Address","One Microsoft Way"),
                new XElement(ns2 +"City","Redmond"),
                new XElement(ns2 +"Zip","WA 98052-6399"),
                new XElement(ns2 +"State","WA"),
                new XElement(ns2 +"Country","USA")));

    WriteLine(company);
}
```

which produces the following result:

```
<Company xmlns="http://www.cninnovation.com/samples/2015">
    <CompanyName
xmlns="http://www.cninnovation.com/samples/2015/address">
        Microsoft Corporation</CompanyName>
    <CompanyAddress
xmlns="http://www.cninnovation.com/samples/2015/address">
        <Address>One Microsoft Way</Address>
        <City>Redmond</City>
        <Zip>WA 98052-6399</Zip>
        <State>WA</State>
        <Country>USA</Country>
    </CompanyAddress>
</Company>
```
