```
public static void UseEvaluate()
{
    //modify to match your path structure
    var doc = new XPathDocument(BooksFileName);
    //create the XPath navigator
    XPathNavigator nav = doc.CreateNavigator();
    //create the XPathNodeIterator of book nodes
    XPathNodeIterator iterator = nav.Select("/bookstore/book");
    while (iterator.MoveNext())
    {
        if (iterator.Current.MoveToChild("title", string.Empty))
        {
            WriteLine($"{iterator.Current.Name}:
{iterator.Current.Value}");
        }
    }
    WriteLine("============================");
    WriteLine($"Total Cost =
{nav.Evaluate("sum(/bookstore/book/price)")}");
}
```

When you run the application, you can see all book titles and the summary price:

```
title: The Autobiography of Benjamin Franklin
title: The Confidence Man
title: The Gorgias
============================
Total Cost = 30.97
```

# Changing XML Using XPath

Next, make some changes using XPath. This part of the code only works with the full .NET Framework, thus preprocessor directives are used to handle the code differences. To create a changeable XPathNavigator, with .NET 4.6, the XmlDocument class is used. Using .NET Core, XmlDocument does not offer a CreateNavigator method, and thus the navigator is always read-only. With .NET 4.6, the CanEdit property of the XPathNavigator returns true, and thus the InsertAfter method can be invoked. Using InsertAfter, a discount is added as sibling after the price element. The newly created XML document is accessed using the OuterXml property of the navigator, and a new XML file is saved (code file XPathNavigatorSample/Program.cs):

```
public static void Insert()
{
#if DNX46
    var doc = new XmlDocument();
    doc.Load(BooksFileName);
#else
    var doc = new XPathDocument(BooksFileName);
#endif

    XPathNavigator navigator = doc.CreateNavigator();

    if (navigator.CanEdit)
    {
        XPathNodeIterator iter =
        navigator.Select("/bookstore/book/price");
```