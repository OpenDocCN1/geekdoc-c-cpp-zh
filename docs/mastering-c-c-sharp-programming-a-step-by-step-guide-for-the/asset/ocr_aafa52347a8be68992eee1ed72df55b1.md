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

The first line in the code is pointing to SampleData.xml, which is the XML sample data file. In the function, we use the function called Load() to load the xml file, and once this is done, child ‘toy’ elements are retrieved by using the function called Doc.descendents(). After that, each of the ‘toy’ child elements is selected and we retrieve the ID along with the two inner elements. These are then passed to comingToys, which is a dynamic variable. At the end, a foreach loop is used to display the data we retrieved.

The output will be:

Toy ID 1 Toy Name Millie Toy Price $0.45

Toy ID 1 Toy Name Dove Toy Price $0.40

Toy ID 1 Toy Name Rook Toy Price $0.55

In much the same way, if we wanted a child element removed from the XML file, we would do it like this:

```
```csharp
private string file = ‘SampleData.xml’;

private void DeleteData (int id)

{

    try
```
```