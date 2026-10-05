
# An XML document

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!--Product data-->
<Products>
  <Product Code="CS08">
    <Description>Murach's C# 2008</Description>
    <Price>54.50</Price>
  </Product>
</Products>
```

## Code attribute

## Description

- You can include one or more attributes in the start tag for an element. An attribute consists of an attribute name, an equal sign, and a string value in quotes.
- If an element has more than one attribute, the order in which the attributes appear doesn't matter, but the attributes must be separated by one or more spaces.

## When to use attributes instead of child elements

- When you design an XML document, you can use either child elements or attributes to represent the data for an element. The choice of whether to implement a data item as an attribute or as a separate child element is often a matter of preference.
- Two advantages of attributes are that they can appear in any order and they are more concise because they do not require end tags.
- Two advantages of child elements are that they are easier for people to read and they are more convenient for long string values.

Figure 22-3 XML attributes

## How to work with the XML Editor

You can use the XML Editor that comes with Visual Studio to create or edit an XML document. The XML Editor is similar to the Code Editor that you use for working with C# code, but it includes features that make it easier to work with XML.

Of course, since an XML file is really just a text file with XML tags, you can open or create an XML file in any text editor. As a result, if you already have a text editor that you prefer, you can use that.

In addition, since XML is a standard format that's used on the web, you can use most web browsers to view an XML document. To do that, you can enter the path for the XML file in the browser's Address bar. Or, on most systems, you can double-click on the file in Windows Explorer.

## How to create a new XML file

To create a new XML file and add it to your project, you can use the Project→Add New Item command as described in example 22-4. This adds the file to your project, adds the XML declaration to the top of the file, and opens the file in the XML Editor. In this figure, for example, the XML declaration includes both the XML version attribute and the encoding attribute that indicates which character set the document uses. Unless you're working in a language other than English, you'll want to leave this set to UTF-8.

## How to open an existing XML file

To open an existing XML file without adding it to your project, you can use the File→Open command to open the file. Then, if the file has a common XML extension (such as xml, xs, or config), or if the file contains XML markup, it is opened in the XML Editor. If this doesn't work, you can right-click on the file in the Solution Explorer, select the Open With command, and select XML Editor from the resulting dialog box.

## How to edit an XML file

When you work in the XML Editor, the task of editing XML files is simplified. For example, tags, content, attributes, values, and comments are color-coded so you can easily tell them apart. When you type a tag, the XML Editor automatically adds the end tag and positions the cursor between the start and end tags you can enter content. In addition, the XML Editor makes it easy to work with the indentation of the child elements, and it makes it easy to view data by expanding or collapsing elements. If you work with the XML Editor for a while, you'll quickly see how easy it is to use.

By the way, if you've used a version of Visual Basic .NET prior to 2008, you may remember that the XML Editor let you work with the data in an XML document in Data Grid view. Unfortunately, this view was omitted from Visual Studio 2008. So you can only work with XML data in the view here.

## An XML document in the XML Editor

![](img/3148667e42d4db35b3d08576aaa1fa01_710_0.png)

## How to add a new XML file to the project

- Choose the Project->Add New Item command. In the Add New Item dialog box, select the XML File template; type a name for the XML file in the Name text box; and click Open. This adds an XML file to your project, adds the XML declaration for the document, and opens the document in the XML Editor.

## How to open an existing XML file

- To open an existing XML file that's stored in the project, double-click on the file.
- To open an existing XML file without adding the file to your project, use the File->Open command.

## How to edit an XML file

- When you type a tag, the XML Editor automatically adds an end tag for the element and positions the insertion point between the start and end tags so you can type the element's content.
- When you type an attribute, the XML Editor automatically adds a pair of quotation marks and positions the insertion point between them so you can type the attribute value.

22-44 How to work with the XML Editor

## How to work with XML

The .NET Framework provides nearly 150 different classes for working XML documents. Frankly, you don't need to know how to use them all. In this topic, I'll get you started with XML programming by showing you how to use two classes: the Xml class and the XmlReader class. These are the classes that provide the basic services you need to write and read XML files.

Note that both of these classes reside in the System.XML namespace. As a result, you should include a using statement for the System.XML namespace at the beginning of any class that uses either of them. Otherwise, you have to qualify the class names each you refer to them.

## How to use the XmlWriter class

Figure 22-5 shows the methods of the XmlWriter class that you can use to write data to an XML file. These methods make it easy to generate the tags for the XML document. As a result, you can concentrate on the document's structure and content.

Since the XmlWriter class is an abstract class, you can't construct an object from this class. However, you can create an XmlWriter object using one of the static Create methods of the XmlWriter class. To do that, you typically use a string variable that holds the path and name of the file. If you specify a file that already exists, it's deleted.

If you want to indent your XML, you need to use XmlSettings object and set its Indent and IndentChars properties. Then, you pass this object to the Create method when you create an XmlWriter object. When you use these methods, it will make your XML easier to read. Although this class has many Write methods, you can create basic XML documents using just the Write methods in this figure.

## Description

- The XmlWriter class lets you write data to a file. If you attempt to write an invalid XML document, an XmlException will be thrown. For example, an XmlException will be thrown if you try to write two XML declarations.

## Common methods of XmlWriter

| Method | Description |
|---|---|
| Create(path) | A static method that creates an XmlWriter object using the specified path or file name. |
| Create(path, settings) | A static method that creates an XmlWriter object using the specified path or file name and the specified XmlSettings object. |
| WriteStartDocument() | Writes an XML declaration line at the beginning of a document. |
| WriteComment(comment) | Writes a comment to the XML document. |
| WriteStartElement(element) | Writes a start tag using the element name you provide. |
| WriteAttributeString(attributeName, value) | Adds an attribute to the current element. |
| WriteEndElement() | Writes an end tag for the current element. |
| WriteElementString(elementName, content) | Writes a complete element including a start tag, content, and end tag. |
| Close() | Closes the XmlWriter object. |

## Common properties of XmlWriterSettings

| Property | Description |
|---|---|
| Indent | Gets or sets a Boolean value that indicates whether to indent elements. |
| IndentChars | Gets or sets the string to use when indenting. |

![](img/3148667e42d4db35b3d08576aaa1fa01_712_0.png)
