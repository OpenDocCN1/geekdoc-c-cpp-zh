
```
```scala
{years.map(yearToXML)}
{rideInfo.map(rideDataToXML)}
{employeeInfo.map(employeeToXML)}
</themeParkData>)
```
```

There is completely new code at the bottom to allow for data entry that is added to the main variables. There is also a do-while loop that handles the menu functionality. The script ends by saving the main data elements back out to the same XML file.

## 14.4 End of Chapter Material

### 14.4.1 Summary of Concepts

- XML is a text markup language that can be used to encode arbitrary data. Being text means that it is as easy to work with as flat text files, but it allow you to attach meaning to the values in the file and the flexibility of the parsing makes it easier to extend XML files than flat text files.
- An XML file is composed of markup and content. The content is plain text. Markup has a number of options as must follow a certain format.
  - The primary markup is tags. A tag starts with `<` and ends with `>`. Each tag has a name.
  - The combination of a matching start and end tag defines an element. An element can contain content and other elements.
  - Start tags can be given attributes to store basic information.
  - Special characters that can not appear as plain text can be specified by markup tokens that begin with a `&` and end with a `;`.
  - You can put comments into an XML file by starting them with `<!--` and ending them with `-->`.
  - The entire contents of an XML file must be held inside of a single element.
- The Scala language has native support for XML. This makes it significantly easier to work with XML in Scala than in most other languages. XML elements can be written directly into Scala source code.
  - An XML file can be loaded using `XML.loadFile(fileName:String):Elem`.
  - The `\` and `\\` operators can be used to pull things out of XML.
  - You can build XML by typing in XML literals. You can put Scala code into the XML by surrounding it with curly braces.
  - XML can be written back out to file using `XML.save(fileName:String,node:Node)`.
  - Patterns can be made using XML with the limitation that attributes can not be part of the match. Values can be bound by including names in curly braces.

### 14.4.2 Self-Directed Study

Enter the following statements into the REPL and see what they do. Some will produce errors. You should try to figure out why. Try some variations to make sure you understand what is going on.

```
scala> val xml1 = <tag>contents</tag>
scala> xml1.text
scala> val <tag>{str}</tag> = xml1
scala> val xml2 = <data type="simple">
| <language>Scala</language>
| <lesson>Programming is an art.</lesson>
| <lesson>Software runs the world</lesson>
| </data>
scala> xml2 \ "language"
scala> xml2 \ "lesson"
scala> val xml3 = <randPoints>
| {(1 to 20).map(i => <point x={math.random.toString} y={math.random.toString}/>)}
| </randPoints>
scala> (xml3 \ "point").map(p => {
| val x = (p \ "@x").text.toDouble
| val y = (p \ "@y").text.toDouble
| math.sqrt(x*x+y*y)
| })
scala> for(<point x={x} y={y}/> <- xml3) yield math.sqrt(x*x+y*y)
scala> val xml4 = <randPoints>
| {(1 to 20).map(i => <point><x>{math.random}</x><y>{math.random}</y></point>)}
| </randPoints>
scala> for(<point><x>{x}</x><y>{y}</y></point> <- xml4 \ "point") println(x+" "+y)
```

### 14.4.3 Exercises

1. Chapter 10 had several exercises where you were supposed to design case classes for a number of different types of data. For each of those, write code to convert to and from XML.
   - A transcript for a student.
   - Realtor information for a house.
   - Data for a sports team.

2. On the website for the book there are a number of XML data files. Write case classes to represent that data in each one and then write code to load the files and build objects from it.

3. Pick some other case class that you have written and create code to convert it to and from XML.

4. Find a Really Simple Syndication (RSS) feed for a website you visit and save the feed as a file. Use Scala to look through the XML.

### 14.4.4 Projects

- 1. If you have been working on the different graphics options for earlier projects, the material in this chapter gives you a clear extension, stores your geometry data in an XML file instead of a flat text file. You can use tags like “sphere” and “plane” to give meaning to the information. Add in a “light” tag as well in anticipation of adding lighting in a future project.

After you have the XML format set up and some data to play with, alter the code from project 7 (p.311) to use this data format.

- 2. Project 3 (p.244) on the text adventure is very nicely extended with the use of XML data files. Using XML also makes it easier to extend the file to include additional information. For this project you should convert your map over to an XML format and have the code read in that format. In addition, you should add items. This will involve adding another case class for an item and putting some items into rooms in the XML data file.

To make the items significant, you need to have it so that the case class for your room includes items in that room and the text description of the room lists what items are there. You should also give you player an inventory and implements commands for “get” and “drop”. So if the player enters “get” followed by the name of an item in the room, that item will be taken out of the room and added to the players inventory. An “inv” command would be nice to let the player see what is in his/her inventory. If the player uses the “drop” command followed by an item in inventory, that item should be removed from inventory and placed in the current room. If “get” or “drop” are provided with an invalid item name, print an appropriate message for the user.

- 3. If you did project 4 (p.346) extending your game, you had a text file that specified the high scores for players of a particular game. For this project you should modify you code and the text file to use XML instead of a flat file.

- 4. If you have been doing the other recipe projects, you can change the format so that it uses XML to save the data. If you do this, you need to add in instructions for the recipes as well as the ability to add comments and other information like how much certain recipes are favored. You can merge what are currently separate text files into a single XML file if you want.

The fact that your script keeps track of recipes and pantry contents points to one other piece of functionality you should be able to add in. Allow the user to see only the recipes that they have the ingredients to cook. If you have a preference level, sort them by preference.

- 5. If you have been doing the scheduling options, convert the data file for courses over to XML. In doing this, you can also add the ability to include comments on courses, instructors, or other things that make sense to you, but which did not fit as well in the limited formatting of a plain text file.

- 6. You can extend project 14 (p.312) on your music library by changing the format of the data file from a flat file to an XML file. Use the hierarchical nature of XML to simplify the file. You can have tags for <artist> at a higher level with <album> tags inside of those and <song> tags at the lowest level. With the XML you could add the ability for the user to insert notes about any element that will be displayed in a manner similar to the album cover when the appropriate item is selected in the GUI. Menu options could be used to allow editing of the notes.

7. This is a continuation of project 5 (p.310) on turtle graphics to draw fractal shapes generated with L-systems. You can find a full description of L-systems in "The Algorithmic Beauty of Plants", which can be found online at http://algorithmicbotany.org/papers/#abop. The first chapter has all the material that will be used for this project and a later one.

In the last turtle project you made it so that you could use a turtle to draw figures from Strings using the characters 'F', 'f', '+', and '-'. L-systems are formal grammars that we will use to generate strings that have interesting turtle representations. An L-system is defined by an initial String and a set of productions. Each production maps a character to a String. So the production F -> F-F++F-F will cause any F in a String to be replaced by F-F++F-F. The way L-systems work is that all productions are applied at the same time to all characters. Characters that do not have productions just stay the same.

So with this example you might start with F. After one iteration you would have F-F++F-F. After the second iteration you would have F-F++F-F-F-F++F-F++F-F++F-F-F-F++F-F. The next iteration will be about five times longer than that. The String in an L-system grow exponentially in length. As a result, you probably want to have the length of the turtle move for an F or f get exponentially shorter. Start with a good value and divide by an appropriate value for each generation. For this example dividing by a factor of 3 is ideal. This one also works best with a turn angle of 60 degrees.

The productions for an L-system can be implemented as a List[(Char,String)]. You can use the find method on the List and combine that with flatMap to run through generations of your String. You can decide how elaborate you want your GUI to be and if users should be able to enter productions or if they will be hard coded. Look in "The Algorithmic Beauty of Plants", chapter 1 for examples of other interesting production rules.

8. If you have done the box score options from any of the last three chapters you can extend to use XML encoding for the box score. You probably want to do this by having functionality to load in a plain text box score and add it to an XML file with all the box scores. To really take advantage of the XML formatting, you should allow the user to add comments to whatever elements you feel are appropriate.

Additional exercises and projects, along with data files, are available on the book's website.
