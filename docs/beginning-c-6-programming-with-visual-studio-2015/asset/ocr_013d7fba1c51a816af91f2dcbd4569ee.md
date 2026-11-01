```
new XElement("customers",
    new XElement("customer",
        new XAttribute("ID", "A"),
        new XAttribute("City", "New York"),
        new XAttribute("Region", "North America"),
        new XElement("order",
            new XAttribute("Item", "Widget"),
            new XAttribute("Price", 100)
        ),
        new XElement("order",
            new XAttribute("Item", "Tire"),
            new XAttribute("Price", 200)
        )
    ),
    new XElement("customer",
        new XAttribute("ID", "B"),
        new XAttribute("City", "Mumbai"),
        new XAttribute("Region", "Asia"),
        new XElement("order",
            new XAttribute("Item", "Oven"),
            new XAttribute("Price", 501)
        )
    )
);
WriteLine(xdoc);
Write("Program finished, press Enter/Return to continue:");
ReadLine();
}
```

5. Compile and execute the program (you can just press F5 for Start Debugging). You will see the output shown here:

```
<customers>
  <customer ID="A" City="New York" Region="North America">
    <order Item="Widget" Price="100" />
    <order Item="Tire" Price="200" />
  </customer>
  <customer ID="B" City="Mumbai" Region="Asia">
    <order Item="Oven" Price="501" />
  </customer>
</customers>
Program finished, press Enter/Return to continue:
```

The XML document shown on the output screen contains a very simplified set of customer/order data. Note that the root element of the XML document is <customers>, which contains two nested <customer> elements. These in turn contain a number of nested <order> elements. The <customer> elements have two attributes, City and Region, and the <order> elements have Item and Price attributes.

Press Enter/Return to exit the program and make the console screen disappear. If you used Ctrl+F5 (Start Without Debugging), you might need to press Enter/Return twice.