
# An introduction to XML

This topic introduces you to the basics of XML. Here, you'll learn what XML is, how it is used, and the rules you must follow to create a simple XML document.

# An XML document

XML (Extensible Markup Language) is a standard way to structure data by tags that identify each data element. In some ways, XML is similar to HTML, the markup language that's used to format HTML documents on the World Wide Web. As a result, if you're familiar with HTML, you'll have no trouble learning how to create XML documents.

Figure 22-1 shows a simple XML document that contains data for three products. Each product has a code, description, and price. In the next two figures, you'll learn how the tags in this XML document work. But even without knowing those details, you can pick out the code, description, and price for each of the three products represented by this XML document.

XML was designed as a way to structure data that's sent over the World Wide Web. When you use .NET to develop web applications, though, you don't have to deal directly with XML. Instead, the .NET Framework classes handle the XML details for.

Besides its use for web applications, XML is used internally throughout the .NET Framework to store data and exchange data between various components of the Framework. In particular, the database features described in section 4 rely on XML. When you retrieve data from a database, for example, the .NET Framework converts the data to XML. However, since this is automatic, the programmer doesn't have to deal with XML directly.

You can also use XML files as an alternative to the text and binary files described in chapter 21. Later in this chapter, for example, you'll learn how to create a ProductDB class for the Product Maintenance application that uses an XML file.

# Data for three products

| Code | Description | Price |
| --- | --- | --- |
| A3CS | Murach's ASP.NET 4 with C# 2008 | 54.50 |
| JSE6 | Murach's Java SE 6 | 52.50 |
| CS08 | Murach's C# 2008 | 54.50 |

# An XML document that contains the data shown above

# Description

- XML, which stands for Extensible Markup Language, provides a method of structuring data using special tags.
- The XML document in this figure contains data for three products. Each product has an attribute Code and elements named Description and Price, which you'll learn more about in the next figures.
- XML can be used to exchange data between different systems, especially via the Internet.
- Many .NET classes, particularly the database and web classes, use XML internally to store or exchange data.
- XML documents that are stored in a file can be used as an alternative to binary files, text files, or other databases for storing data.
- When XML is stored in a file, the file name usually has an extension of xml.
- The .NET Framework includes several classes that let you read and write XML data. These classes are in the System.Xml namespace.

Figure 22-1 An XML document

# XML tags, declarations, and comments

Figure 22-2 shows how XML uses tags to structure the data in an XML document. Here, each XML tag begins with the < character and ends with the > character. As a result, the first line in the XML document contains a complete XML tag. Similarly, the next three lines also contain complete tags. In contrast, the fifth line contains two tags, <Description> and </Description>, with a text value between.

The first tag in any XML document is an XML declaration. This declaration identifies the document as an XML document and indicates which XML version the document conforms to. In this example, the document conforms to XML version 1.0. In addition, the declaration usually identifies the character set that's being used for the document. In this example, the character set is UTF-8, the most common one used for XML documents in English-speaking countries.

An XML document can also contain contents. These are tags with <!-- and end with ->. Between the tags, you can type anything you want. For instance, the second line in this figure is a comment that indicates what type of data is contained in the XML document. It's often a good idea to include similar comments in your own XML documents.

# XML elements

Elements are the building blocks of XML. Each element in an XML document represents a single data item and is identified by two tags: a start tag and an end tag. The start tag marks the beginning of the element and provides the element's name. The end tag marks the end of the element and repeats the name, prefixed by a slash. For example, <Description> is the start tag for an element named Description, and </Description> is the corresponding end tag. It's important to realize that XML does not provide a pre-defined set of elements names like HTML does. Instead, you create your own elements to describe the content of each element. Since XML names are case-sensitive, <product> and <Product> are not the same.

A complete element contains the element's start tag, its end tag, and the content. For example, <Price>54.50</Price> indicates that the content of the element is 54.50. <Description>Murach's C# 2008</Description> indicates that the content of the element is Murach's C# 2008.

Besides content, elements can contain other elements, known as child elements. This lets you add structure to a parent element. For example, a Product element can have child elements that provide details about each product, such as the product's description and price. In this figure, for example, you can see that the start tag, end tag, and values for the Description and Price elements are contained between the start and end tags for the Product element. As a result, Description and Price are children of the Product element, and the Product element is the parent of both the Description and Price elements.

# An XML document

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!--Product data-->
<Products>
  <Product Code="CS008">
    <Description>Murach's C# 2008</Description>
    <Price>54.50</Price>
  </Product>
</Products>
```

# Tags, XML declarations, and comments

- Each XML tag begins with < and ends with >.
- The first line in an XML document is an XML declaration that indicates which version of the XML standard is being used for the document. In addition, the declaration usually identifies the standard character set that's used. For documents in English-speaking countries, UTF-8 is the character set that's commonly used.
- You can use the <!-- and --> tags to include comments in an XML document.

# Elements

- An element is a unit of XML data that begins with a start tag and ends with an end tag. The start tag provides the name of the element and contains any attributes assigned to the element (see figure 22-3 for details on attributes). The end tag repeats the name, prefixed with a slash (/). You can use any name you want for an XML element.
- The text between an element's start and end tags is called the element's content. For example, <Description>Murach's C# 2008</Description> indicates the content of the Description element is the string Murach's C# 2008.
- Elements can contain other elements. An element that's contained within another element is known as a child element. The element that contains a child is known as the parent element.
- Child elements can repeat within a parent element. For instance, in the example above, the Products element can contain more than one Product element. Similarly, each Product element could contain repeating child elements.
- The highest-level parent element in an XML document is known as the root element. An XML document can have only one root element.

Figure 22-2 XML tags, declarations, comments, and elements

Section 5 Other skills for C# developers

The XML document in figure 22-1 shows, an element can occur more than once within an XML document. In this case, the document has three Product elements, each representing a product. Since each of these Product elements contains Description and Price elements, these elements also appear three times in the document.

Although this example doesn't show it, a given child element can occur more than once within a parent. For example, suppose you want to provide for products that have more than one category. You could do this by using a Category child element to indicate the category of a product. Then, for a product that belongs to multiple categories, you simply include multiple Category child elements within the Product element for that.

The highest-level parent element in an XML document is known as the root element, and an XML document can have only one root element. In the examples in figures 22-1 and 22-2, the root element is Products. For XML documents that contain repeating data, it is common to use a plural name for the root element to indicate it contains multiple child elements.

# XML attributes

As shown in figure 22-3, attributes are a concise way to provide data for XML elements. In the XML document, for example, each Product element has a Code attribute that provides an identifying code for the product. Thus, <Code="CS08"> contains an attribute named Code whose value is CS08.

Here again, XML doesn't provide a set of pre-defined attributes. Instead, you create attributes as you need them, using names that describe the content of the attributes. If an element has more than one attribute, you can list the attributes in any order you wish. However, you must separate the attributes from each other with one or more spaces. In addition, each attribute can appear only once within an element.

When you plan the layout of an XML document, you will often need to decide whether to use elements or attributes to represent each data item. In many cases, either will work. In the products document, for example, I could have used a child element Code rather than an attribute to represent each product's code. Likewise, I could have used an attribute named Description rather than a child element for the product's description.

Because attributes are more concise than child elements, it's often tempting to use attributes rather than child elements. Keep in mind, though, that an element with more than a few attributes becomes unwieldy. As a result, most designers limit their use of attributes to certain types of data, such as identifiers like product codes or customer numbers.
