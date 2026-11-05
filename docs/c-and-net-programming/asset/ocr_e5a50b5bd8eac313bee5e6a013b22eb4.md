# Example

```
//illustration of reading the file XmlReader and use XmlTextReader as the input of
/ReadXmlSchema

//Create a dataset object
DataSet ds = new DataSet("New DataSet");
// Read xsl in an XmlTextReader
XmlTextReader myXmlReader = new XmlTextReader(@"c:\media.Xml");
// Call Read xml schema
ds.ReadXmlSchema(myXmlReader);
myXmlReader.Close();
```

+   - Writing XML using Data Set

The DataSet class contains methods to write XML file from a DataSet object and fill the data to the file.

# The Writexml Method

The WriteXml method writes the current data (the schema and data) of a DataSet object to an XML file. This is overloaded method. By using this method, data can be written to a file, stream, TextWriter, or XmlWriter.

# Example

```
//illustration writing the data to an XML file using DataSet
using System;
using System.IO;
using System.Xml;
using System.Data;
namespace XmlandADO
{
    class XmlAndDataSetDemo
    {
    public static void Main()
    {
    Try
    {
    // Create a DataSet, namespace and Media table
    // with Name and Type columns
    DataSet ds = new DataSet("DS");
    ds.Namespace = "StdNamespace";
    DataTable mdTable = new DataTable("Media");
    DataColumn col1 = new DataColumn("Name");
    DataColumn col2 = new DataColumn("Type");
    mdTable.Columns.Add(col1);
    mdTable.Columns.Add(col2);
    ds.Tables.Add(mdTable);
    //Add media Data to the table
```