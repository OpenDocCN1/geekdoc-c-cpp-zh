Object Oriented Programming using C#

The Unified Modelling Language (UML)

# 2.5 UML Object Diagrams

Class diagrams and package diagrams allow us to visualise and discuss the architecture of a system, however at times we wish to discuss the data processes. Object diagrams allow us to visual one instance of time and the data that a system may contain in that moment.

Object diagrams look superficially similar to class diagrams however boxes represent represent instances of objects.

Boxes are titled with :-

```
objectName : ClassName
```

As each box describes a particular object at a specific moment in time the box contains attributes and their values (at that moment in time).

```
attribute = value
```

These diagrams are useful for illustrating particular 'snapshot' scenarios during design.

The object diagram shows several several object that may exist at a moment in time for a library catalogue system. The system contains two classes :-

+   Book, which stores the details of a book andnLibrary, which maintains a collection of books, with books being added, searched for or removed as required.

![](bbox=[0.263, 0.506, 0.843, 0.745])

| book1 : Book |
| title = "OO Programming Using C#" author = "S Kendal" |
| book2 : Book |
| title = "Fishing Made Simple" author = "A Trout" |
| book3 : Book |
| title = "Cooking for Beginners" author = "A Chef" |

Looking at this diagram we can see that at a particular moment in time, while three books have been created only two have been added to the library: If we were to search the library for 'Cooking for Beginners' we would not expect the book to be found.

Download free ebooks by bookboom.com

56