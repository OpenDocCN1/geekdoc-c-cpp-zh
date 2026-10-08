
# Contents 21

22.8 Creating a Master/Detail View App 965
22.8.1 Creating the Master/Detail GUI 965
22.8.2 Coding the Master/Detail App 967
22.9 Address Book Case Study 968
22.9.1 Creating the Address Book App’s GUI 970
22.9.2 Coding the Address Book App 971
22.10 Tools and Web Resources 975
22.11 Wrap-Up 975

# 23 Asynchronous Programming with async and await 982
23.1 Introduction 983
23.2 Basics of async and await 985
23.2.1 async Modifier 985
23.2.2 await Expression 985
23.2.3 async, await and Threads 985
23.3 Executing an Asynchronous Task from a GUI App 986
23.3.1 Performing a Task Asynchronously 986
23.3.2 Method calculateButton_Click 988
23.3.3 Task Method Run: Executing Asynchronously in a Separate Thread 989
23.3.4 awaiting the Result 989
23.3.5 Calculating the Next Fibonacci Value Synchronously 989
23.4 Sequential Execution of Two Compute-Intensive Tasks 990
23.5 Asynchronous Execution of Two Compute-Intensive Tasks 992
23.5.1 awaiting Multiple Tasks with Task WhenAll 995
23.5.2 Method StartFibonacci 996
23.5.3 Modifying a GUI from a Separate Thread 996
23.5.4 awaiting One of Several Tasks with Method WhenAny 996
23.6 Invoking a Flickr Web Service Asynchronously with HttpClient 997
23.6.2 Invoking the Flickr Web Service flickr.photos.search Method 1001
23.6.3 Processing the XML Response 1002
23.6.4 Binding the Photo Titles to the ListBox 1003
23.6.5 Asynchronously Downloading an Image’s Bytes 1004
23.7 Displaying an Asynchronous Task’s Progress 1004
23.8 Wrap-Up 1008

# Chapters on the Web 1015
# A Operator Precedence Chart 1016
# B Simple Types 1018
# C ASCII Character Set
# Appendices on the Web
# Index
# Online Topics

PDFs presenting additional topics for advanced college courses and professionals are available through the book's Companion Website:

```
http://www.pearsonglobaleditions.com/deitel
```

New copies of this book come with a Companion access code that's located on the book's inside front cover. If the access code is already visible or there is no card, you purchased used book or an edition that does not come with an access code.

# Web App Development with ASP.NET
# XML and LINQ to XML
# Universal Windows Platform (UWP) GUI, Graphics, Multimedia and XAML
# REST Web Services
# Cloud Computing with Microsoft Azure™
# Windows Presentation Foundation (WPF) GUI, Graphics, Multimedia and XAML
# ATM Case Study, Part 1: Object-Oriented Design with the UML
# ATM Case Study, Part 2: Implementing an Object-Oriented Design in C#
# Using the Visual Studio Debugger

# Preface

Welcome to the world of desktop, mobile and web app development with Microsoft's Visual C#® programming language. Visual C# How to Program, 6/e is based on C# 6 and related Microsoft software technologies. You'll be using the .NET platform and the Visual Studio® Integrated Development Environment where you'll conveniently write, test and debug your applications and run them on Windows® devices. The Windows operating runs on desktop and notebook computers, mobile phones and tablets, game systems and a great variety of devices associated with the emerging "Internet of Things".

We believe that this book and its supplements for students and instructors will give you an informative, engaging, challenging and entertaining introduction to Visual#. The book presents leading-edge computing technologies in a friendly manner appropriate for introductory course sequences, based on the curriculum recommendations of two key professional organizations—the ACM and the IEEE.² You'll study for today's most popular programming paradigms:

- object-oriented programming.
- structured programming,
- generic programming and
- functional programming (new in this edition).

At the heart of the book is the Detail live-code approach—rather than using code snippets, we generally present concepts in the context of complete working programs followed by sample executions. We include a broad range of example programs and exercises selected from computer science, business, education, social issues, personal utilities, sports, mathematics, puzzles, simulation, game playing, graphics, multimedia and many other areas. We also provide abundant tables, line drawings and UML diagrams for a more visual learning experience.

- At the time of this writing, Microsoft has not yet released the official C# 6 Specification. To view an unofficial copy, visit https://github.com/jw1004/csharpspec/blob/gh-pages/README.md
-² These recommendations include Computer Science Curricula 2013 Curriculum Guidelines for Undergraduate Degree Programs in Computer Science, December 20, 2013. The Joint Task Force on Computing Curricula, Association for Computing Machinery (ACM), IEEE Society.

Read the Before You Begin section after this Preface for instructions on setting up your computer to run the hundreds of code examples and to enable you to develop your own C# apps. The source code for all of the book's examples is available at

http://www.pearsonglobalitions.com/deitel

Use the code we provide to compile and run each program as you study it—this will help you master Visual# and related Microsoft technologies faster and at a deeper level. Most of the book's examples in Visual Studio on Windows 7, 8 or 10 (there is no 9). The code examples for the online presentation of the Universal Windows Platform (UWP) and XAML specifically require Windows 10.

# Contacting the Authors

As you read the book, if you have a question, we're easy to reach at

```
deitel@deitel.com
```

We'll respond promptly.

# Join the Deitel & Associates, Inc. Social Media Communities

Subscribe to the Deitel® Buzz Online newsletter

http://www.deitel.com

and join the Deitel social communities on

- Facebook®—http://facebook.com
- LinkedIn®—http://linkedin.com
- YouTube®—http://youtube.com
- Twitter®—http://twitter.com
- Instagram®—http://instagram.com
- Google™—http://google.com

# Object-Oriented Programming with an Early Approach

The book introduces the basics and terminology of object-oriented programming in Chapter 1. In Chapter 2, you *will* manipulate objects, such as labels. In Chapter 3, Introduction to C# App Programming, you develop your first classes. Presenting objects early gets you “thinking about objects” immediately and mastering these concepts. Our early objects presentation continues in Chapters 5–9 with a variety of case studies. In Chapters 10–12, we take a deeper look at classes, then use those concepts throughout the remainder of the book.

# New C# 6 Features

We introduce new C#  language features throughout the book (Fig. 1)—each defining occurrence is marked with a "6" margin icon as shown next to this paragraph.

| C# 6 language feature | First introduced in |
|---|---|
| string interpolation | 3.5 |
| expression bodied methods and get accessors | 7.15 |
| auto-implemented property initializers | 8.6.1 |
| getter-only auto-implemented properties | 8.6.1 |
| nameof operator | 10.5 |
| null-conditional operator (?) | 13.9 |
| when clause for filtering | 13.10 |
| using static directive | 21.3.1 |
| null conditional operator (?]) | 21.6 |
| collection initializers for any collection with An extension method | 21.7 |
| index initializers | 21.7 |

> Fig. I | C# 6 new features.

# Interesting, Entertaining and Challenging Exercises

The book contains hundreds of exercises to practice the skills you learn. Extensive-review exercises and answers are included for self-study. Also, each chapter concludes with a substantial set of exercises, which generally include

- simple recall of important terminology and concepts,
- identifying the errors in code samples,
- writing individual program statements,
- writing methods to perform specific tasks,
- writing C# classes,
- writing complete programs and
- implementing major projects.
