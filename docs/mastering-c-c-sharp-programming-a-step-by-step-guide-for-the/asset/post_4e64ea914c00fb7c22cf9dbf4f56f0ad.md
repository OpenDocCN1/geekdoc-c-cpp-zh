
In this code, a variable called toys has been declared. We cast it to the SelectListItem type so that the resulting row is saved from our LINQ query. We have two methods, called Where and Select, that we use to find the target that matched with our specific query. The line that reads ‘toy => toy.Tag == curTag.ID’ will choose a toy as per a tag that gets passed but the line that reads ‘toy => new SelectListItem {Value = toy.Name, Text = toy.ID’ will choose the toy based on an ID and name that are passed. The result, the toy that matches the specified criterion, is saved to the variable called toys.

Now we turn our attention to the way that LINQ works with XML data. XML stands for Extensible Markup Language and it is one of the most used languages on the internet. But it is far more than a set of static labels that are text-based. XML is also sometimes known as self-defining data or self-describing data. Its tag usage is customizable to the highest extent as well as being standardized; it is used globally for sharing data, for accessing it and manipulating it. What we will look at now is how to use LINQ to retrieve XML data, to delete it, and how to insert and update it.

## Retrieve and delete XML data

Every XML data file has a parent or root tag, also known as an element, that will both encapsulate and define the type of its child records and define the attributes for them. The child records or elements that result from this have real data in them that can be manipulated as needed. Look at this example code; this is XML code that we will use throughout the rest of this section for LINQ queries:

```
<?xml version='1.0' encoding='utf-8'?>
<Toys>
  <Toy ID='1'>
    <Name>Millie</Name>
    <Price>$0.45</Price>
  </Toy>
  <Toy ID='2'>
<Name>Dove</Name>
<Price>$0.40</Price>
</Toy>
<Toy ID='3'>
  <Name>Rook</Name>
  <Price>$0.55</Price>
</Toy>
</Toys>
```

In this example, the root element is ‘Toys’ and it has several child elements, each a ‘Toy’ and each of these has its own attribute called ID with two inner elements called Price and Name.

What we want to do is retrieve the child toys and we do that by using a LINQ query, like this:

```
private string file = 'SampleData.xml';
```

```
private void GetData()
{
  try
  {
    XDocument doc = XDocument.Load(file);
    var comingToys = from toy in doc.Descendants("Toy")
    select new
    {
      ID= Convert.ToInt32(toy.Attribute("ID").Value),
      Name = toy.Element("Name").Value ,
      Price = toy.Element("Price").Value
    };

    foreach (var x in comingToys)
```

```
```csharp
{
    Console.Write("Toy ID " + x.ID + " ");
    Console.Write("Toy Name " + x.Name + " ");
    Console.WriteLine("Toy Price " + x.Price+ " ");
}

}
catch (Exception err)
{
    Console.WriteLine(err.Message);
}

}
```
```

The first line in the code is pointing to SampleData.xml, which is the XML sample data file. In the function, we use the function called Load() to load the xml file, and once this is done, child ‘toy’ elements are retrieved by using the function called Doc.Descendants(). After that, each of the ‘toy’ child elements is selected and we retrieve the ID along with the two inner elements. These are then passed to comingToys, which is a dynamic variable. At the end, a foreach loop is used to display the data we retrieved.

The output will be:

Toy ID 1 Toy Name Millie Toy Price $0.45

Toy ID 1 Toy Name Dove Toy Price $0.40

Toy ID 1 Toy Name Rook Toy Price $0.55

In much the same way, if we wanted a child element removed from the XML file, we would do it like this:

```
```csharp
private string file = 'SampleData.xml';

private void DeleteData (int id)

{

    try
```

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

## Insert and Update XML data

It isn’t a much different route to take for adding data to an XML file. In essence, all we really need is an object that is of XElement type that has a matching signature to the elements that already exist in the target file. Then that object is inserted in the data file by using an object of XDocument type:

```
private string file = 'SampleData.xml';
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

```
int newID = Convert.ToInt32 (lastToy.Attribute ("ID").Value);
newToy.SetAttributeValue("ID",++newID);
doc.Element ("Toys").Add (newToy);
doc.Save (file);
}
catch (Exception err)
{
Console.WriteLine(err.Message);
}
}
```

Once the object of XDocument type is created we also created an object of XElement type whose signature matches that to the Toy elements that already exist. This is done using the line that reads XElement newToy = new XElement('Toy', new XElement('Name', name), new XElement('Price', price))''. Then we use a function called doc.Descendants('Toy').Last() to get the final toy element from the variable called lastToy.

When we have that element, we retrieve the value for the ID and increment it at the same time as setting the attribute to the new element, using the line that reads newToy.SetAttributeValue('ID',++newID)". Last, the toy object is inserted using the function called Add() and the changes to the file are saved.

In our sample file, we now have another child. If, for example, we had passed in a name of 'John ' with a price of $0.1 to the function above, it would look like this:

```
<Toy ID='4'>
  <Name>Hare</Name>
  <Price>$0.65</Price>
</Toy>
```

To change XML data or elements that already exist, the first thing we need to do is find the target element against certain criteria with data

values that we want to change, which is the line that reads XElement cToy = doc.Descendants('Toy'). In this line, (c=>c.Attribute('ID').Value.Equals(id)" does that by looking for a match to the ID we provided and letting cToy, which is the XElement object, point to the element. As soon as we have the reference to the element, the values of its inner elements can be updated using cToy.Element('Price').Value = price. And, finally, the XML document is saved with all the changes.

```
private string file = 'SampleData.xml';
private static void UpdateData(string name, string price, int id)
{
    try
    {
    XDocument doc = XDocument.Load(file);
    IEnumerable<XElement> cToy =
    doc.Descendants("Toy").Where (c=>(int)c.Attribute("ID") == id);
    cToy.First().Element("Name").Value = name;
    cToy.First().Element("Price").Value = price;
    doc.Save(file);
    }
    catch (Exception err)
    {
    Console.WriteLine(err.Message);
    }
}
```

Now let’s assume that we passed that function above three more values as arguments – id=1, name=Alligator, and price=$0.75. Once the above function has been executed the XML data file will no longer show toy name=Millie at id=1. Instead, name=Alligator will be there instead:

```
<Toy ID='1'>
  <Name>Alligator</Name>
  <Price>$0.75</Price>
```

</Toy>

Next, we move on to PLINQ and Parallel Classes.

## Parallel Class and PLINQ

PLINQ or Parallel LINQ is nothing more than a parallel implementation of a LINQ pattern. PLINQ queries are very much like standard LINQ queries to Objects. And like a standard LINQ query, the PLINQ query operates on any in-memory IEnumerable or any IEnumerable<T> data source. Their execution is deferred, meaning that execution does not start until the specified query has been enumerated.

The main difference is PLINQ tries to make use of every processor on a system and this is done by partitioning each data source into segments; the data query is then executed on each of the segments on a separate worker thread on multiple processors and in parallel. In some cases, using PLINQ will ensure that the query is much faster.

Using parallel execution, PLINQ can provide some serious improvements to performance against the legacy code for some query types and that can often be achieved simply by adding a query called AsParallel to the data source. However, with some query types, using parallelism will only slow them down so it is important that you understand PLINQ.

We will be using Lambda expressions to define delegates and we are going to go over PLINQ classes, and how PLINQ queries are created. What you won’t get is an in-depth look at everything, but more of an overview with examples.

### The ParallelEnumerable Class

Most of the PLINQ functionality is exposed in the class called System.Linq.ParallelEnumerable. Both this and the other namespace types for System.Linq are compiled into the assembly called System.Core.dll and the default projects in Visual Studio (C# and Visual Basic) will all referencing the assembly and they will import the relevant namespace.

With ParallelEnumerable, you get the implementations of every standard query operator that is supported by LINQ to Object but
