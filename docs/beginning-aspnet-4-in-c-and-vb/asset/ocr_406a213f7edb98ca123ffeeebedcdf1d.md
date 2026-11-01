The Inventory class is the one of interest here. If you are to serialize this class, you need to insert an attribute containing XmlArrayItem constructors for each type that can be added to the array. You should note that XmlArrayItem is the name of the .NET attribute represented by the XmlArrayItemAttribute class.

The first parameter supplied to these constructors is what you would like the element name to be in the XML document that is created during serialization. If you leave off the ElementName parameter, the elements will be given the same name as the object type (Product and BookProduct in this case). The second parameter that must be specified is the type of the object.

There is also an XmlArrayAttribute class that you would use if the property were returning an array of objects or primitive types. Because you are returning different types in the array, you use XmlArrayItemAttribute, which allows the higher level of control.

In the button4_Click() event handler, you create a new Product object and a new BookProduct object (newProd and newBook). You add data to the various properties of each object, and add the objects to a Product array. You next create a new Inventory object and pass in the array as a parameter. You can then serialize the Inventory object to recreate it later:

```
```csharp
private void button4_Click(object sender, EventArgs e)
{
    //create the XmlAttributes object
    XmlAttributes attrs = new XmlAttributes();
    //add the types of the objects that will be serialized
    attrs.XmlElements.Add(new XmlElementAttribute("Book", typeof(BookProduct)));
    attrs.XmlElements.Add(new XmlElementAttribute("Product", typeof(Product)));
    XmlAttributeOverrides attrOver = new XmlAttributeOverrides();
    //add to the attributes collection
    attrOver.Add(typeof(Inventory), "InventoryItems", attrs);
    //create the Product and Book objects
    Product newProd = new Product();
    BookProduct newBook = new BookProduct();
    newProd.ProductID = 100;
    newProd.ProductName = "Product Thing";
    newProd.SupplierID = 10;
    newBook.ProductID = 101;
    newBook.ProductName = "How to Use Your New Product Thing";
    newBook.SupplierID = 10;
    newBook.ISBN = "123456789";
    Product[] addProd = { newProd, newBook };
    Inventory inv = new Inventory();
    inv.InventoryItems = addProd;
    TextWriter tr = new StreamWriter("inventory.xml");
    XmlSerializer sr = new XmlSerializer(typeof(Inventory), attrOver);
    sr.Serialize(tr, inv);
    tr.Close();
    webBrowser1.Navigate(AppDomain.CurrentDomain.BaseDirectory + "inventory.xml");
}
```
```

code snippet frmSerial.cs

The XML document looks like this:

```
```xml
<?xml version="1.0" encoding="utf-8"?>
<Inventory xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
<ProductDiscount>0</ProductDiscount>
<ProductID>100</ProductID>
<ProductName>Product Thing</ProductName>
<SupplierID>10</SupplierID>
<CategoryID>0</CategoryID>
<UnitPrice>0</UnitPrice>
```
```