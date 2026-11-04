
- 19.11.1 LINQ Extension Methods Min, Max, Sum and Average 619
- 19.11.2 Aggregate Extension Method for Reduction Operations 619
- 19.11.3 The Where Extension Method for Filtering Operations 621
- 19.11.4 Select Extension Method for Mapping Operations 622
- 19.12 PLINQ: Improving LINQ to Objects Performance with Multicore 622
- 19.13 (Optional) Covariance and Contravariance for Generic Types 626
- 19.14 Wrap-Up 628

## 20 Databases and LINQ 629

- 20.1 Introduction 630
- 20.2 Relational Databases 631
- 20.3 A Books Database 632
- 20.4 LINQ to Entities and the ADO.NET Entity Framework 636
- 20.5 Querying a Database with LINQ 637
- 20.5.1 Creating the ADO.NET Entity Data Model Class Library 639
- 20.5.2 Creating a Windows Forms Project and Configuring It to Use the Entity Data Model 643
- 20.5.3 Data Bindings Between Controls and the Entity Data Model 645
- 20.6 Dynamically Binding Query Results 651
- 20.6.1 Creating the Display Query Results GUI 652
- 20.6.2 Coding the Display Query Results App 653
- 20.7 Retrieving Data from Multiple Tables with LINQ 655
- 20.8 Creating a Master/Detail View App 661
- 20.8.1 Creating the Master/Detail GUI 661
- 20.8.2 Coding the Master/Detail App 663
- 20.9 Address Book Case Study 664
- 20.9.1 Creating the Address Book App's GUI 666
- 20.9.2 Coding the Address Book App 667
- 20.10 Tools and Web Resources 671
- 20.11 Wrap-Up 671

## 21 Asynchronous Programming with async and await 672

- 21.1 Introduction 673
- 21.2 Basics of async and await 675
- 21.2.1 async Modifier 675
- 21.2.2 await Expression 675
- 21.2.3 async, await and Threads 675
- 21.3 Executing an Asynchronous Task from a GUI App 676
- 21.3.1 Performing a Task Asynchronously 676
- 21.3.2 Method calculateButton_Click 678
- 21.3.3 Task Method Run: Executing Asynchronously in a Separate Thread 679
- 21.3.4 awaiting the Result 679
- 21.3.5 Calculating the Next Fibonacci Value Synchronously 679
- 21.4 Sequential Execution of Two Compute-Intensive Tasks 680
- 21.5 Asynchronous Execution of Two Compute-Intensive Tasks 682
- 21.5.1 awaiting Multiple Tasks with Task Method WhenAll 685
- 21.5.2 Method StartFibonacci 686
- 21.5.3 Modifying a GUI from a Separate Thread 686
- 21.5.4 awaiting One of Several Tasks with Task Method WhenAny 686
- 21.6 Invoking a Flickr Web Service Asynchronously with HttpClient 687
- 21.6.1 Using Class HttpClient to Invoke a Web Service 691
- 21.6.2 Invoking the Flickr Web Service’s flickr.photos.search Method 691
- 21.6.3 Processing the XML Response 692
- 21.6.4 Binding the Photo Titles to the ListBox 693
- 21.6.5 Asynchronously Downloading an Image’s Bytes 694
- 21.7 Displaying an Asynchronous Task’s Progress 694
- 21.8 Wrap-Up 698

## A Operator Precedence Chart 700

## B Simple Types 702

## C ASCII Character Set 704

## Index 705

## Contacting the Authors

As you read the book, if you have a question, we're easy to reach at

```
deitel@deitel.com
```

We'll respond promptly.

## Join the Deitel & Associates, Inc. Social Media Communities

For book updates, visit

```
http://www.deitel.com/books/CSharp6FP
```

subscribe to the Deitel® Buzz Online newsletter

```
http://www.deitel.com/newsletter/subscribe.html
```

and join the conversation on

- Facebook®—http://facebook.com/DeitelFan
- LinkedIn®—http://linkedin.com/company/deitel-&-associates
- YouTube®—http://youtube.com/DeitelTV
- Twitter®—http://twitter.com/Deitel
- Instagram™—http://instagram.com/DeitelFan
- Google+™—http://google.com/+DeitelFan

## New C# 6 Features

We introduce key new C# 6 language features throughout the book (Fig. 1)—each defining occurrence is marked with a “6” margin icon as shown next to this paragraph.

| C# 6 new language feature | First introduced in |
|---|---|
| string interpolation | Section 3.5 |
| expression-bodied methods and get accessors | Section 7.15 |
| auto-implemented property initializers | Section 8.6.1 |
| getter-only auto-implemented properties | Section 8.6.1 |
| nameof operator | Section 10.5.1 |
| null-conditional operator (?. ) | Section 13.9.1 |
| when clause for exception filtering | Section 13.10 |
| using static directive | Section 19.3.1 |
| null conditional operator (?[]) | Section 19.6 |
| collection initializers for any collection with an Add extension method | Section 19.7 |
| index initializers | Section 19.7 |

Fig. 1 | C# 6 new language features.

## A Tour of the Book

Here’s a quick walkthrough of the book’s key features.

### *Introduction to Visual C# and Visual Studio 2015 Community Edition*

The discussions in

- Chapter 1, Introduction
- Chapter 2, Introduction to Visual Studio and Visual Programming

introduce the C# programming language, Microsoft’s .NET platform and Visual Programming. The vast majority of the book’s examples will run on Windows 7, 8 and 10 using the *Visual Studio 2015 Community* edition with which we test-drive a *Painter* app in Section 1.7. Chapter 1 briefly reviews object-oriented programming terminology and concepts on which the rest of the book depends.

### *Introduction to C# Fundamentals*

The discussions in

- Chapter 3, Introduction to C# App Programming
- Chapter 4, Introduction to Classes, Objects, Methods and strings
- Chapter 5, Control Statements: Part 1
- Chapter 6, Control Statements: Part 2
- Chapter 7, Methods: A Deeper Look
- Chapter 8, Arrays; Introduction to Exception Handling

present rich coverage of C# programming fundamentals (data types, classes, objects, operators, control statements, methods and arrays) through a series of object-oriented programming case studies. Chapter 3 briefly introduces exception handling with an example that demonstrates attempting to access an element outside an array’s bounds.

### *Object-Oriented Programming: A Deeper Look*

The discussions in

- Chapter 9, Introduction to LINQ and the List Collection
- Chapter 10, Classes and Objects: A Deeper Look
- Chapter 11, Object-Oriented Programming: Inheritance
- Chapter 12, OOP: Polymorphism and Interfaces
- Chapter 13, Exception Handling: A Deeper Look

provide a deeper look at object-oriented programming, including classes, objects, inheritance, polymorphism, interfaces and exception handling. An online two-chapter case study on designing and implementing the object-oriented software for a simple ATM is described later in this preface.

Chapter 9 introduces Microsoft’s Language Integrated Query (LINQ) technology, which provides a uniform syntax for manipulating data from various data sources, such as arrays, collections and, as you’ll see in later chapters, databases and XML. Chapter 9 is intentionally simple and brief to encourage readers to begin using LINQ technology early.

Section 9.4 introduces the List collection. Later in the book, we take a deeper look at LINQ, using LINQ to Entities (for querying databases) and LINQ to XML.

### *Windows Forms Graphical User Interfaces (GUIs)*

The discussions in

- Chapter 14, Graphical User Interfaces with Windows Forms: Part 1
- Chapter 15, Graphical User Interfaces with Windows Forms: Part 2

present a detailed introduction to building GUIs using Windows Forms. We also use Windows Forms GUIs in several later chapters.

### *Strings and Files*

The discussions in

- Chapter 16, Strings and Characters: A Deeper Look
- Chapter 17, Files and Streams

investigate strings in more detail, and introduce text-file processing and object-serialization for inputting and outputting entire objects.

### *Generics and Generic Collections*

The discussions in

- Chapter 18, Generics
- Chapter 19, Generic Collections; Functional Programming with LINQ/PLINQ

introduce generics and generic collections. Chapter 18 introduces C# generics and demonstrates how to create type-safe generic methods and a type-safe generic class. Rather than "reinventing the wheel," most C# programmers should use .NET's built-in searching, sorting and generic collections (prepackaged data structures) capabilities, which are discussed in Chapter 19.

### *Functional Programming with LINQ, PLINQ, Lambdas, Delegates and Immutability*

In addition to generic collections, Chapter 19 now introduces functional programming, showing how to use it with LINQ to Objects to write code more concisely and with fewer bugs than programs written using previous techniques. In Section 19.12, with one additional method call, we demonstrate with timing examples how PLINQ (Parallel LINQ) can improve LINQ to Objects performance substantially on multicore systems.

### *Database with LINQ to Entities and SQL Server*

The discussions in

- Chapter 20, Databases and LINQ

introduce database programming with the ADO.NET Entity Framework, LINQ to Entities and Microsoft's free version of SQL Server that's installed with the Visual Studio 2015 Community edition.

### *Asynchronous Programming*

The discussions in
