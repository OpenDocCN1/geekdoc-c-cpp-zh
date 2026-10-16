```
{
    XDocument sampleXML = XDocument.Load(file);
    IEnumerable<XElement> cToy =
    sampleXML.Descendants("Toy").Where(c => (int)c.Attribute("ID") ==
    id);
    cToy.First().Remove();
    sampleXML.Save(file);
}
    catch (Exception e)
    {
    Console.WriteLine(e.Message);
    }
}
```

Once the target file is loaded, the code above will traverse through the child ‘toys’ to find a match to the toy ID we passed in. Once found, the match is removed using the function called Remove() and the file is saved.

# Insert and Update XML data

It isn’t a much different route to take for adding data to an XML file. In essence, all we really need is an object that is of XElement type that has a matching signature to the elements that already exist in the target file. Then that object is inserted in the data file by using an object of XDocument type:

```
private string file = ‘SampleData.xml’;
```

```
private static void InsertData(string name, string price)
{
    try
    {
    XDocument doc = XDocument.Load(file);
    XElement newToy = new XElement("Toy", new
    XElement("Name", name), new XElement("Price", price));
    var lastToy = doc.Descendants("Toy").Last();
```