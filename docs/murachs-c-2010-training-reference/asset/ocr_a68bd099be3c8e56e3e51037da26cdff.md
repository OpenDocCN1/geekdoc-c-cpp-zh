# A class that works with an XML document

Page 2

```
public static void SaveProducts(List<Product> products)
{
    // create the XmlWriterSettings object
    XmlWriterSettings settings = new XmlWriterSettings();
    settings.Indent = true;
    settings.IndentChars = (" ");

    // create the XmlWriter object
    XmlWriter xmlOut = XmlWriter.Create(path, settings);

    // write the start of the document
    xmlOut.StartDocument();
    xmlOut.WriteStartElement("Products");

    // write each Product object to the xml file
    foreach (Product product in products)
    {
        xmlOut.WriteStartElement("Product");
        xmlOut.WriteAttributeString("Code",
            product.Code);
        xmlOut.WriteElementString("Description",
            product.Description);
        xmlOut.WriteElementString("Price",
            Convert.ToString(product.Price));
        xmlOut.WriteEndElement();
    }

    // write the end tag for the root element
    xmlOut.WriteEndElement();

    // close the XmlWriter object
    xmlOut.Close();
}
}
```

Figure 22-10 The code for the ProductDB class (part 2 of 2)