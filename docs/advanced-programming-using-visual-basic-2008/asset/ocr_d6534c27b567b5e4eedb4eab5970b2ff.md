in the Pubs SQL Server database, represented in XML. (Later in this chapter, you will use the Pubs database for VB projects.)

```
<?xml version="1.0" standalone="yes"?>
<AuthorsDataSet xmlns="AuthorsDataSet.xsd">
  <authors>
    <au_id>172-32-1176</au_id>
    <au_lname>White</au_lname>
    <au_fname>Johnson</au_fname>
    <phone>408 496-7223</phone>
    <address>10932 Bigge Rd.</address>
    <city>Menlo Park</city>
    <state>CA</state>
    <zip>94025</zip>
    <contract>true</contract>
  </authors>
  <authors>
    <au_id>213-46-8915</au_id>
    <au_lname>Green</au_lname>
    <au_fname>Marjorie</au_fname>
    <phone>415 986-7020</phone>
    <address>309 63rd St. #411</address>
    <city>Oakland</city>
    <state>CA</state>
    <zip>94618</zip>
    <contract>true</contract>
  </authors>
</AuthorsDataSet>
```

Each typed DataSet has a schema, which defines the fields, data types, and any constraints, such as required fields. ADO.NET validates the data against the schema and checks for constraint violations.

The format of XML data offers several advantages for programming. Because the schema provides for strong data typing, the various data types can be handled properly. ADO.NET can treat the XML data as objects, allowing the IntelliSense feature of the Visual Studio environment to provide information for the programmer. In addition, data handling in XML and ADO.NET executes faster than in earlier forms of ADO.

# The Visual Studio IDE

The VS IDE provides tools to help you develop database applications. You will use the Data Sources window to set up the data sources for your applications, as well as the Server Explorer (called the Database Explorer in the Express Edition), which replaces some of the functions of the Server Explorer of previous editions.

# The Data Sources Window

The Data Sources window provides an easy way to set up the data sources for an application. Using the Data Sources window, you can easily create data-bound controls on a form. After you set up the data source, you can add grids or individual fields by dragging a table or fields from the Data Sources window to the form. Or you can make an existing control display database data by dragging a field from the Data Sources window and dropping it on the control, which causes data binding to be set up automatically.