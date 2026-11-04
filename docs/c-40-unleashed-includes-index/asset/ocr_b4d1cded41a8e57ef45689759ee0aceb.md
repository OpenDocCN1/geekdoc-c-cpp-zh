# LINQ TO XSD

LINQ to XML remained untyped without an object/XML mapping technology next to it. When dealing with schematized XML, using XSD schemas, the experience of formulating a query could be made easier as the structure of the document is known in much detail. For example, the Price attribute could be surfaced as a well-typed property on a Product class. And the Products node could be retrieved from the document directly as an IEnumerable<Product>.

For some time during the early days of LINQ, there was an attempt to leverage XSD schemas as a way to make queries over XML data using LINQ more pleasant to write. However, this LINQ to XSD project ultimately got cancelled. Although this seemed quite attractive, there are quite a few problems. For one thing, child elements and attributes can have the same name, making the use of properties for both of them infeasible in general because of potential name clashes. Besides this, it's been a general industry trend to omit XSD schemas for lots of XML documents, sometimes in favor of using other formats, such as JSON or REST (for web services without a WSDL schema).

Finally, Visual Basic 9.0 went a slightly different direction to tackle the aesthetic problem of traversing into XML data. They added language support for so-called XML literals, together with syntax to select attributes and such (.). Internally, those constructs compile into LINQ to XML API calls.

Much more complex queries can be written over XML documents, leveraging the same set of query operators as available for other data domains like SQL and objects. What should be remembered from this introductory discussion about LINQ to XML is how the technology hides lots of complexities around the use of XPath and certain XML data traversal patterns that would otherwise be written using imperative loop constructs.

Before concluding our first journey through the world of the LINQ to XML APIs, I want to point out that this API is also very well suited for creating new XML elements using constructor syntax:

```
var products = new XElement("Products",
    new XElement("Product",
        new XAttribute("Name", "Chai"),
        new XAttribute("Price", 18.00m)
    ),
    ...
);
```

You can write whole XML documents (or XML fragments) simply by calling nested constructors, ultimately resulting in an in-memory object tree representing the XML data.