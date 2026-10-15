
```
New XElement("CompanyName", "Wrox"),
New XElement("CompanyAddress",
    New XElement("Street", "111 River Street"),
    New XElement("City", "Hoboken"),
    New XElement("State", "NJ"),
    New XElement("Country", "USA"),
    New XElement("Zip", "07030-5774")))
Console.WriteLine(root.ToString())
Console.WriteLine("Press ENTER to exit")
Console.ReadLine()
End Sub

End Module
```

In this case, an XNamespace object is created by assigning it a value of http://www.example.com/somenamespace. From there, it is actually used in the root element <Company> with the instantiation of the XElement object:

```
Dim root As New XElement(ns + "Company",
```

This will produce the results shown in Figure 9-8.

![](img/d99870e80390742f93963da7be0b2e61_391_0.png)

## FIGURE 9-8

Besides dealing with the root element, you can also apply namespaces to all your elements:

```
Imports System.Xml.Linq

Module Main

    Sub Main()
        Dim ns1 As XNamespace = "http://www.example.com/ns/root"
        Dim ns2 As XNamespace = "http://www.example.com/ns/address"

        Dim root As New XElement(ns1 + "Company",
            New XElement(ns1 + "CompanyName", "Wrox"),
            New XElement(ns2 + "CompanyAddress",
                New XElement(ns2 + "Street", "111 River Street"),
                New XElement(ns2 + "City", "Hoboken"),
                New XElement(ns2 + "State", "NJ"),
                New XElement(ns2 + "Country", "USA"),
                New XElement(ns2 + "Zip", "07030-5774")))

        Console.WriteLine(root.ToString())
        Console.WriteLine("Press ENTER to exit")
        Console.ReadLine()
    End Sub

End Module
```

## VISUAL BASIC AND XML LITERALS

Visual Basic takes LINQ to XML one step further, enabling you to place XML directly in your code. Using *XML literals*, you can place XML directly in your code for working with the XDocument and XElement objects. Here, the use of the XElement object was presented as follows:

```
```vb
Imports System.Xml.Linq

Module Main

    Sub Main()
        Dim root As New XElement("Company",
                                 New XElement("CompanyName", "Wrox"),
                                 New XElement("CompanyAddress",
                                              New XElement("Street", "111 River Street"),
                                              New XElement("City", "Hoboken"),
                                              New XElement("State", "NJ"),
                                              New XElement("Country", "USA"),
                                              New XElement("Zip", "07030-5774")))
        Console.WriteLine(root.ToString())
        Console.WriteLine("Press ENTER to exit")
        Console.ReadLine()
    End Sub

End Module
```
```

Using XML literals, you can use the following syntax:

```
```vb
Module Main

    Sub Main()
        Dim root As XElement =
            <Company>
                <CompanyName>Wrox</CompanyName>
                <CompanyAddress>
                    <Street>111 River Street</Street>
                    <City>Hoboken</City>
                    <State>NJ</State>
                    <Country>USA</Country>
                    <Zip>07030-5774</Zip>
                </CompanyAddress>
            </Company>
        Console.WriteLine(root.ToString())
        Console.WriteLine("Press ENTER to exit")
        Console.ReadLine()
    End Sub

End Module
```
```

This enables you to place the XML directly in the code (see Figure 9-11). The best part about this is the IDE support for XML literals. Visual Studio 2010 has IntelliSense and excellent color-coding for the XML that you place in your code file.

![](img/d99870e80390742f93963da7be0b2e61_394_0.png)

## FIGURE 9-11

You can also use inline variables in the XML document. For instance, if you wanted to declare the value of the <CompanyName> element outside the XML literal, then you could use a construct similar to the following:

```
Module Module1
    Sub Main()
        Dim companyName As String = "Wrox"
        Dim xe As XElement = _
            <Company>
                <CompanyName><%= companyName %></CompanyName>
                <CompanyAddress>
                    <Street>111 River Street</Street>
                    <City>Hoboken</City>
                    <State>NJ</State>
                    <Country>USA</Country>
                    <Zip>07030-5774</Zip>
                </CompanyAddress>
            </Company>
        Console.WriteLine(xe.ToString())
        Console.ReadLine()
    End Sub
End Module
```

In this case, the <CompanyName> element is assigned a value of Wrox from the companyName variable, using the syntax <%= companyName %>.

## USING LINQ TO QUERY XML DOCUMENTS

Now that you can get your XML documents into an XDocument object and work with the various parts of this document, you can also use LINQ to XML to query your XML documents and work with the results.

### Querying Static XML Documents

Notice that querying a static XML document using LINQ to XML takes almost no work at all. The following example makes use of the hamlet.xml file, querying for all the players (actors) who appear in a play. Each of these players is defined in the XML document with the <PERSONA> element:

```
Module Main
    Sub Main()
        Dim xdoc As XDocument = XDocument.Load("C:\hamlet.xml")
        Dim query = From people In xdoc.Descendants("PERSONA") _
            Select people.Value
```

```
Console.WriteLine("{0} Players Found", query.Count())
Console.WriteLine()
For Each item In query
    Console.WriteLine(item)
Next
Console.WriteLine("Press ENTER to exit")
Console.ReadLine()
End Sub
End Module
```

In this case, an XDocument object loads a physical XML file (hamlet.xml) and then performs a LINQ query over the contents of the document:

```
Dim query = From people In xdoc.Descendants("PERSONA") _
    Select people.Value
```

The people object is a representation of all the <PERSONA> elements found in the document. Then the Select statement gets at the values of these elements. From there, a Console.WriteLine method is used to write out a count of all the players found, using query.Count. Next, each of the items is written to the screen in a For Each loop. The results you should see are presented here:

```
26 Players Found
CLAUDIUS, king of Denmark.
HAMLET, son to the late, and nephew to the present king.
POLONIUS, lord chamberlain.
HORATIO, friend to Hamlet.
LAERTES, son to Polonius.
LUCIANUS, nephew to the king.
VOLTIMAND
CORNELIUS
ROSENCRANTZ
GUILDENSTERN
OSRIC
A Gentleman
A Priest.
MARCELLUS
BERNARDO
FRANCISCO, a soldier.
REYNALDO, servant to Polonius.
Players.
Two Clowns, grave-diggers.
FORTINBRAS, prince of Norway.
A Captain.
English Ambassadors.
GERTRUDE, queen of Denmark, and mother to Hamlet.
OPHELIA, daughter to Polonius.
Lords, Ladies, Officers, Soldiers, Sailors, Messengers, and other Attendants.
Ghost of Hamlet's Father.
```

### Querying Dynamic XML Documents

Numerous dynamic XML documents can be found on the Internet these days. Blog feeds, podcast feeds, and more provide XML documents by sending a request to a specific URL endpoint. These feeds can be viewed either in the browser, through an RSS aggregator, or as pure XML This code uses LINQ to XML to read a RSS feed:

```
Module Module1
    Sub Main()
        Dim xdoc As XDocument = _
            XDocument.Load("http://weblogs.asp.net/mainfeed.aspx")
        Dim query = From rssFeed In xdoc.Descendants("channel") _
            Select Title = rssFeed.Element("title").Value, _
```

```
```vb
Description = rssFeed.Element("description").Value, _
Link = rssFeed.Element("link").Value
For Each item In query
    Console.WriteLine("TITLE: " + item.Title)
    Console.WriteLine("DESCRIPTION: " + item.Description)
    Console.WriteLine("LINK: " + item.Link)
Next
Console.WriteLine()
Dim queryPosts = From myPosts In xdoc.Descendants("item") _
                 Select Title = myPosts.Element("title").Value, _
                        Published = _
                            DateTime.Parse(myPosts.Element("pubDate").Value), _
                        Description = myPosts.Element("description").Value, _
                        Url = myPosts.Element("link").Value
For Each item In queryPosts
    Console.WriteLine(item.Title)
Next
Console.WriteLine("Press ENTER to exit")
Console.ReadLine()
End Sub
End Module
```
```

Here, the Load method of the XDocument object points to a URL where the XML is retrieved. The first query pulls out all the main sub-elements of the `<channel>` element in the feed and creates new objects called `Title`, `Description`, and `Link` to get at the values of these sub-elements.

From there, a `For Each` statement is run to iterate through all the items found in this query. The second query works through all the `<item>` elements and the various sub-elements it contains (these are all the blog entries found in the blog). Though a lot of the items found are rolled up into properties, in the `For Each` loop, only the `Title` property is used. You will see results similar to that shown in Figure 9-12.

![](img/d99870e80390742f93963da7be0b2e61_396_0.png)

## FIGURE 9-12

## WORKING WITH THE XML DOCUMENT

If you have been working with the XML document `hamlet.xml`, you probably noticed that it is quite large. You’ve seen how you can query into the XML document in a couple of ways, and now this section takes a look at reading and writing to the XML document.

### Reading from an XML Document

Earlier you saw just how easy it is to query into an XML document using the LINQ query statements, as shown here:
