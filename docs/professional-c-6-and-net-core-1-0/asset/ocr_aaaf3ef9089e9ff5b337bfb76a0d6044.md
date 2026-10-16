> **NOTE** *LINQ is covered in Chapter 13, “Language Integrated Query.” The specific implementation of LINQ, LINQ to XML, is covered in this chapter.*

To serialize and deserialize .NET objects to XML, you can use the `XmlSerializer`. With .NET Core, the NuGet package needed here is `System.Xml.XmlSerializer` with the namespace `System.Xml.Serialization`.

WCF uses another method for XML serialization: data contract serialization. Although the `XmlSerializer` does allow you to differ serialization between attributes and elements, this is not possible with the `DataContractSerializer` serializing XML.

> **NOTE** *WCF is covered in Chapter 44, “Windows Communication Foundation.”*

# JSON

JavaScript Object Notation (JSON) came up in recent years because it can be directly used from JavaScript, and it has less overhead compared to XML. JSON is defined by IETF RFC 7159 (`https://tools.ietf.org/html/rfc7159`), and the ECMA standard 404 (`http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf`).

For sending JSON documents, there’s an official MIME type `"application/json"`. Some frameworks still use older, unofficial MIME types `"text/json"` or `"text/javascript"`.

The same content as the earlier XML file is described here using JSON. Arrays of elements are contained within brackets. In the example, the JSON file contains multiple `book` objects. Curly brackets define objects or dictionaries. The key and value are separated by a colon. The key needs to be quoted; the value is a string:

```
"book": {
  "genre":"autobiography",
  "publicationdate": 1991,
  "ISBN":"1-861003-11-0",
  "title":"The Autobiography of Benjamin Franklin"
  "author": {
    "first-name":"Benjamin",
    "last-name":"Franklin"
  },
  "price": 8.99
},
"book": {
  "genre":"novel",
  "publicationdate": 1967,
  "ISBN":"1-861001-57-6",
  "title":"The Confidence Man"
```