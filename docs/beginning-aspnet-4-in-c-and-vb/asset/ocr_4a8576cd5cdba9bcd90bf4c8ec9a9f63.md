```
Console.ReadLine();
}
}
```

code download ConsoleApplication1.sln

In this case, an XDocument object loads up a physical XML file (hamlet.xml) and then performs a LINQ query over the contents of the document:

```
var query = from people in xdoc.Descendants("*PERSONA*")
    select people.Value;
```

The people object is a representation of all the <PERSONA> elements found in the document. Then the select statement gets at the values of these elements. From there, a Console.WriteLine() method is used to write out a count of all the players found using query.Count(). Next, each of the items is written to the screen in a foreach loop. The results you should see are presented here:

26 Players Found

```
CLAUDIUS, king of Denmark.
HAMLET, son to the late king, and nephew to the present king.
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
FORTIMBRAS, prince of Norway.
A Captain.
English Ambassadors.
GERTRUDE, queen of Denmark, and mother to Hamlet.
OPHELIA, daughter to Polonius.
Lords, Ladies, Officers, Soldiers, Sailors, Messengers, and other Attendants.
Ghost of Hamlet's Father.
```

# Querying Dynamic XML Documents

A lot of dynamic XML documents are available on the Internet these days. You will find blog feeds, podcast feeds, and more that provide an XML document by sending a request to a specific URL endpoint. These feeds can be viewed either in the browser, through an RSS-aggregator, or as pure XML. This example shows you how to work with an RSS feed directly from your code.

```
using System;
using System.Linq;
using System.Xml.Linq;

namespace ConsoleApplication1
{
    class Class1
    {
```