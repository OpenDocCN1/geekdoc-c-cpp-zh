+   - Generate DataSet classes from an XSD schema file
+   - Generate runtime classes that have the custom attributes for XmlSerialization
+   - Generate an XSD file from classes that you have already developed
+   - Limit which elements are created in code
+   - Determine which programming language the generated code should be in (C#, Visual Basic .NET, or JScript .NET)
+   - Create schemas from types in compiled assemblies

You should refer to the Framework documentation for details of command-line options for xsd.exe.

Despite these capabilities, you don’t have to use xsd.exe to create the classes for serialization. The process is quite simple. The following is a simple application that serializes a class. At the beginning of the example, you have very simple code that creates a new Product object, pd, and fills it with some data:

```
private void button1_Click(object sender, EventArgs e)
{
    //new products object
    Product pd = new Product();
    //set some properties
    pd.ProductID = 200;
    pd.CategoryID = 100;
    pd.Discontinued = false;
    pd.ProductName = "Serialize Objects";
    pd.QuantityPerUnit = "6*";
    pd.ReorderLevel = 1;
    pd.SupplierID = 1;
    pd.UnitPrice = 100;
    pd.UnitsInStock = 10;
    pd.UnitsOnOrder = 0;
}
```

The Serialize() method of the XmlSerializer class actually performs the serialization, and it has nine overloads. One of the parameters required is a stream to write the data to. It can be a Stream, TextWriter, or an XmlWriter parameter. In the example, you create a TextWriter-based object, tr. The next thing to do is to create the XmlSerializer-based object, sr. The XmlSerializer needs to know type information for the object that it is serializing, so you use the typeof keyword with the type that is to be serialized. After the sr object is created, you call the Serialize() method, passing in the tr (Stream-based object) and the object that you want serialized, in this case pd. Be sure to close the stream when you are finished with it:

```
//new TextWriter and XmlSerializer
TextWriter tr = new StreamWriter("serialprod.xml");
XmlSerializer sr = new XmlSerializer(typeof(Product));
//serialize object
sr.Serialize(tr, pd);
tr.Close();
webBrowser1.Navigate(AppDomain.CurrentDomain.BaseDirectory + "serialprod.xml");
```

Next is the Product class, the class to be serialized. The only differences between this and any other class that you may write are the C# attributes that have been added. The XmlRootAttribute and XmlElementAttribute classes in the attributes inherit from the System.Attribute class. Don’t confuse these attributes with the attributes in an XML document. A C# attribute is simply some declarative