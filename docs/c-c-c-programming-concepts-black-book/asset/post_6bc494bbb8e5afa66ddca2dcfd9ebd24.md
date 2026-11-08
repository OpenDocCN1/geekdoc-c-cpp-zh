
```csharp
txtXpath.Text += xnavigator.Name + ": " + xnavigator.Value + "\n";

while (xnavigator.MoveToNext())
{
    txtXpath.Text += xnavigator.Name + ": " + xnavigator.Value + "\n";
}

xnavigator.MoveToParent();
}
} while (xnavigator.MoveToNext());
}
```

The main XPath classes used in processing an XML document are `XPathDocument` and `XPathNavigator`. The `XPathDocument` object creates an in-memory representation of XML document using the XPath data model. The `XPathNavigator` object is created depending on the `XPathDocument` object.

Let’s now learn how to convert an ADO.NET dataset to XML by using the `XmlDataDocument` class.

### ADO.NET and XML

In one of the previous chapters, we have discussed that ADO.NET is used to connect a Web page to a database using dataset. The .NET platform provides a way to integrate a relationship between ADO.NET and XML. It provides some of the useful methods that help in reading the dataset and storing the data values to an XMLDocument. The methods used in this case are WriteXml, WriteXmlSchema, ReadXml, and ReadXmlSchema. The WriteXml method writes the dataset in the XML format and the WriteXmlSchema method writes the XSD file of that dataset object. During the retrieval of dataset, we use ReadXml and ReadXmlSchema to retrieve the XML and XSD files, respectively.

We can also access the dataset object through a class known as XmlDataDocument. Using this class, we can retrieve the data from the XML and XSD files and store it in a dataset format provided by XmlDataDocument. Listing 20.16 shows the code to retrieve the data from an XML file and present it in a grid view by using XmlDataDocument:

**Listing 20.16:** Showing the implementation of the XmlDataDocument class

```csharp
public void workwithXmlDataDocument()
{
    //Declaring the XML file path
    string filePath = @"C:\XML\MyFirstXML.xml";
    //Declaring the XSD file path
    string xsdFilePath = @"C:\XML\MyFirstXML.xsd";
    //Declaring the XmlDataDocument object
    XmlDataDocument xmlDoc = new XmlDataDocument();
    //Retrieving the data set from the XML file validated using the
    //XSD file
    xmlDoc.DataSet.ReadXmlSchema(xsdFilePath);
    xmlDoc.Load(filePath);
    //Bind the dataset with the data control in .NET
    grdXmlDataDoc.DataSource = xmlDoc.DataSet;
    grdXmlDataDoc.DataBind();
}
```

In the preceding method, we have declared an object of XmlDataDocument. Next, we have retrieved the data from the XSD file using the Load() method. At the end, we have bound the dataset to the ASP data control. Therefore, the XmlDataDocument class bridges a gap between ADO.NET and XML.

With this, we come to the end of the chapter; let’s now summarize the main points discussed in the chapter.

### Summary

At the beginning of the chapter, we have learned about the XML language and its structural representation. Next, we have discussed the XmlTextReader, XmlTextWriter, and XmlDocument classes that help in creating and reading an XML document. With the help of these classes, we have developed the My XML Manager application to create and read an XML document. After that, the chapter has discussed XSD, XSLT, and XPath. Towards the end, we have learned how to convert an ADO.NET dataset to XML by using the XmlDataDocument class.

In the next chapter, we learn about the file system and I/O operations using C#.

### Quick Revise

#### Multiple Choice Questions

- **Q1.** XML is an abbreviation of
  - i. Extended Markup language
  - ii. Expensive Markup language
  - iii. Extensible Markup language
  - iv. Extent markup language

- **Q2.** What is the syntax used before writing XML?
  - i. `<xml version = "1.0">`
  - ii. `<xml version = "1.0" \>`
  - iii. `<xml version = "1.0" ?>`
  - iv. `</xml version = "1.0"?>`

- **Q3.** In XML, data is described using:
  - i. DTD
  - ii. XSL
  - iii. Description node
  - iv. XQuery

- **Q4.** XML uses the features of:
  - i. HTML
  - ii. XHTML
  - iii. VML
  - iv. SGML

- **Q5.** Which of the following is a correct XML document?
  - i. `<tag1> data1</tag1>`  
    `<tag2> data2 </tag2>`
  - ii. `<tag1> data1`  
    `<tag2> data2 </tag2>`  
    `</tag1>`
  - iii. `<tag1> data1`  
    `<tag2> data2 </tag1>`  
    `</tag2>`
  - iv. `</tag1>data1`  
    `<tag2>data2<tag1>>`

- **Q6.** Using XSLT, we can transform an XML into
  - i. XML, HTML, CSV, Text
  - ii. XML, HTML
  - iii. XML, HTML, Text
  - iv. XML, HTML, XHTML

- **Q7.** An XML method that creates an in-memory object is
  - i. XmlReader
  - ii. XmlTextWriter
  - iii. XmlWriter
  - iv. XmlDocument
  - v. XmlDataDocument

- **Q8.** The popularly used XML class that helps in transforming an XML document to its HTML counterpart is
  - i. XslCompiledTransform
  - ii. XslArgumentList
  - iii. XslTransformXml
  - iv. XslCompleteTransform

- **Q9.** The namespaces used to apply XSD in XML are
  - i. `using System.Xml.xsd;`  
    `using System.IO;`
  - ii. `using System.Xml.xsd;`
  - iii. `using System.Xml.Schema;`  
    `using System.IO;`
  - iv. `using System.Xml.Schema;`

- **Q10.** Which of the following line needs to be added just after the XML declaration tag to run the XSLT file for an XML?
  - i. `<?xml-stylesheet type="text/xsl" href="FileName.xsl" \>`
  - ii. `<?xml-stylesheet href="FileName.xsl"?>`
  - iii. `<?xml-stylesheet type="text/xsl" href="FileName.xsl"?>`
  - iv. `<?xml-stylesheet type="text/xsl">`

#### Subjective Questions

- 1. Point out the difference between the XmlTextWriter and XmlDocument classes.

- 2. What is the need for using XSLT?

- 3. Why DTD has been replaced by XSD? Describe the advantages and disadvantages of both XSD and DTD.

- 4. Modify the My XML Manager application to incorporate more than one child node. The existing solution is restricted to add only one child and its sub-child element. Therefore, modify the application in such a way that it can be more dynamic by incorporating more than one child element in an XML document.

- 5. Modify the My XML Manager application so that it can also incorporate the read operation using the XmlDocument class.

  > **NOTE**
  > 
  > Implement the read functionality using the methods of the XmlDocument class on the click of the Create XML using XMLDocument button.

- 6. Create a new application that incorporates the following features:
  - i. It can create an XML document
  - ii. It can validate the XML document
  - iii. It can transform the XML document through XSLT into HTML design

  > **NOTE**
  > 
  > Prepare a Web page that contains three buttons: Create XML, Validate XML, and Transform XML. While a user clicks the Create XML button, the user should be redirected to the My XML Manager page, where he/she can create an XML document. Other two buttons use the same XML to run the validation and transformation processes, respectively.

![](img/43c5f409f9b17790a628c4b4df854b61_720_0.png)

## Chapter 21: File System and I/O Operations Using C#

| If you need an Information on: | See page: |
|---|---|
| Exploring the File System Architecture | 680 |
| Understanding Risks Concerning File Systems in a Web Application | 681 |
| Describing File System Classes | 681 |
| Exploring the Classes for File and Directory Operations | 685 |
| Creating a File System Application using C# | 693 |
| Introducing the File Compression Technique | 706 |
| Describing the Isolated Storage | 713 |
| Writing an Email Script | 715 |

A file system stores and organizes files and their data. It typically has directories or folders that allow the grouping of similar files. Various operations, such as updating an existing file, creating a new file, and renaming a directory, can be performed on a file system. C# provides the System.IO namespace that offers various classes, methods, and properties to manipulate files and directories. For example, the System.IO namespace provides the FileStream, StreamReader, StreamWriter, File, and FileInfo classes to perform operations, such as moving, copying, and deleting files. In addition, the namespace provides the Directory and DirectoryInfo classes that can be used to create, move, and delete directories.

In this chapter, we learn about the file system architecture and various risks involved in using files in a Web application. Further, the chapter discusses various file system classes, namely FileStream, StreamReader, and StreamWriter. Next, we learn the classes, such as Directory, DirectoryInfo, File, and FileInfo, for directory and file operations. We also learn to create a file system application by using C#. In addition, the chapter discusses the file compression technique and isolated storage. Towards the end, we learn to write different types of emails using C#.

Let’s begin the chapter by exploring the architecture of a file system.

### Exploring the File System Architecture

In a file system, a file is the basic unit of resources. A file comprises metadata and textual content. Metadata can be defined as data about data. In other words, metadata specifies the information about the data or content in a file. Generally, metadata contains the following information about a file:

- Creation date of the file
- Last modification date of the file
- Last accessed date of the file
- Size of the file
- Location of the file in a system
- Type of the file

However, depending on the type of a file, other information can also be associated with the metadata. For example, metadata for a video file also contains the length of the video to define its duration.

When we create files, they are always stored inside a directory. Directory is nothing but a folder that is created to store files in it. In other words, a folder in a file system corresponds to a directory. This directory or folder may contain another set of directories or files.

A file system deals with the file storage architecture and file manipulation methods. The general services that a file system provides are:

- Move a file to a different location
- Copy a file from one location to another
- Delete a file from a specific location
- Append a file to another existing file
- Edit the existing file
- Upload a file to a specific location
- Create a file to a specified location
- Modify the structure of a file

In the next section, let’s discuss the risks involved in file systems when they are used in a Web application.
