```
SqlDataAdapter dAProduct = new SqlDataAdapter
("SELECT Name, StandardCost, ProductCategoryID FROM SalesLT.Product", conn);
SqlDataAdapter dACategory = new SqlDataAdapter
("SELECT ProductCategoryID, Name FROM SalesLT.ProductCategory", conn);
// Fill DataSet from both SqlAdapters
daProduct.Fill(ds, "Products");
daCategory.Fill(ds, "Categories");
// Add the relation
ds.Relations.Add(ds.Tables["Categories"].Columns["ProductCategoryID"],
ds.Tables["Products"].Columns["ProductCategoryID"]);
// Write the Xml to a file so we can look at it later
ds.WriteXml("Products.xml", XmlWriteMode.WriteSchema);
// load data into grid
dataGridView1.DataSource = ds.Tables[0];
// create the XmlDocument
doc = new XmlDocument(ds);
// Select the productname elements and load them in the grid
XmlNodeList nodeList = doc.SelectNodes("//XMLProducts/Products");
textBox1.Text = "";
foreach (XmlNode node in nodeList)
{
    textBox1.Text += node.InnerXml + "\r\n";
}
```

code snippet frmADOXML.cs

In the sample you are creating, there are two DataTables in the XMLProducts DataSet: Products and Categories. You create a new relation on the ProductCategoryID column in both tables.

By using the same WriteXml() method call that you did in the previous example, you will get the following XML file (SuppProd.xml):

```
<?xml version="1.0" standalone="yes"?>
<XMLProducts xmlns="" xmlns:xsi="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">
  <xs:schema id="XMLProducts" xmlns="" xmlns:xs="http://www.w3.org/2001/XMLSchema" msdata:IsDataSet="true" msdata:UseCurrentLocale="true">
    <xs:complexType name="XMLProducts">
      <xs:choice minOccurs="0" maxOccurs="unbounded">
        <xs:element name="Products">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="Name" type="xs:string" minOccurs="0" />
              <xs:element name="StandardCost" type="xs:decimal" minOccurs="0" />
              <xs:element name="ProductCategoryID" type="xs:int" minOccurs="0" />
            </xs:sequence>
          </xs:complexType>
        </xs:element>
        <xs:element name="Categories">
          <xs:complexType>
            <xs:sequence>
              <xs:element name="ProductCategoryID" type="xs:int" minOccurs="0" />
              <xs:element name="Name" type="xs:string" minOccurs="0" />
            </xs:sequence>
          </xs:complexType>
        </xs:element>
      </xs:choice>
    </xs:complexType>
    <xs:unique name="Constraint1">
      <xs:selector xpath=".//Categories" />
```