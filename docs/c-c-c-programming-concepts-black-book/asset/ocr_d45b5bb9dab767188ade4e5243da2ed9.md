+   3. Save the XSD file for future use.

Let's now validate an XML document against the XSD file by using C#. For this, we need to add the following namespace in the program file(<file_name>.aspx.cs):

```
```csharp
using System.Xml.Schema;
```
```

To validate an XML document against an XSD file, two classes of the preceding namespace are used, namely XmlValidatingReader and XmlSchemaCollection. The XmlValidatingReaderclass is used to read the XSD file and validate the XML document; whereas, the XmlSchemaCollectionclass is used to add the XSD file to the XmlValidatingReader object. Let's perform the following steps to describe the process of validating an XML document against an XSD file:

+   1. Declare an object of the XmlTextReader class by using the FileStream object.
+   2. Declare an object of XmlValidatingReader by using the object of XmlTextReader.
+   3. Declare an object of XmlSchemaCollection that stores the XSD file definition.
+   4. Add the XSD file by using the XmlSchemaCollection object to the application whose targetNamespaceis set to the name of the file.
+   5. Attach the object of XmlSchemaCollection to the object of XmlValidatingReader.
+   6. Read the XSD file by using the XmlValidatingReader object. During the read process, if the compiler finds any inconsistency between the XML document and the XSD file, then it will throw an error "XML Document is not well formed!!!".

Listing 20.12: Validating an XML Document against an XSD File

```
```csharp
public void validateXML()
{
    string path = @"C:\XML\";
    string fileName = "MyFirstXML.xml";
    if (File.Exists(path + fileName))
    {
        //Declaring xmlTextReader object
        FileStream fileStream = new FileStream(path + fileName, FileMode.Open);
        XmlTextReader reader = new XmlTextReader(fileStream);

        //Declaring the xmlValidatingReader object which has been
        //created on the xmlTextReader object
        XmlValidatingReader validatingReader =
            new XmlValidatingReader(reader);

        //Declaring the xmlSchemaCollection object that will store the XSD file
        XmlSchemaCollection schemaCollection = new XmlSchemaCollection();

        //Adding the XSD file
        schemaCollection.Add("MyFirstXML", @"C:\XML\MyFirstXML.xsd");

        //Adding the schema collection to the xmlValidatingReader object
        validatingReader.Schemas.Add(schemaCollection);
        try
        {
            //validating the XML document
            while (validatingReader.Read())
            {
            }
        }
    }
}
```
```