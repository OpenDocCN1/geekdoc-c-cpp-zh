
- Deploying Your Masterpiece............................................................................... 713
- Lots of options............................................................................................. 713
- Copying Web sites with “Copy Web”............................................................... 714
- Package/Publish............................................................................................ 715

## Book VII: Service-Oriented Development ................................. 717

## Chapter 1: Getting Acquainted with Web Services ........................ 719

- Understanding Web Services......................................................................... 719
- Loosely coupled.................................................................................................. 721
- Contract driven.............................................................................................. 722
- Chunky versus chatty...................................................................................... 724
- Building Service-Oriented Applications..................................................... 726
- Providing XML Web Services............................................................... 728
- Building Three Sample Apps............................................................................... 728

## Chapter 2: Building Web Services with ASMX ............................ 731

- Getting to Know SOAP................................................................................... 732
- SOAP and standards............................................................................................... 732
- The WS-* standards....................................................................................... 733
- The impact to you............................................................................................ 733
- Big, fat, and slow................................................................................................ 734
- Making an ASMX Service...................................................................... 735
- Creating a new service....................................................................... 735
- Building the code for SHARP............................................................... 739
- Deploying...................................................................................................... 741
- Consuming services in your applications............................................................... 743

## Chapter 3: Building Web Services with WCF ............................ 745

- Getting to Know WCF.................................................................................. 746
- Creating a WCF Service........................................................................ 748
- Breaking it down......................................................................................... 748
- Making a registration service............................................................... 750
- Configuring............................................................................................... 752
- Deploying.................................................................................................. 756
- Consuming................................................................................................ 757

## Chapter 4: Building Web Services with ReST .................................. 759

- Getting to Know ReST............................................................................... 759
- Understanding the Guiding Principles of ReST.................................. 760
- Diving into the details of ReST.......................................................... 761
- Changing a WCF Service to Use ReST.................................................. 762
- Getting the WCF service....................................................................... 762
- Exposing the ReST service.................................................................. 762
- Returning data in different ways........................................................... 763

## Book III: New! Features in C# 4.0 ................................................................ 767

- Chapter 1: Programming Dynamically!.................................................................. 769
- Shifting C# Toward Dynamic Typing.................................................................. 770
- Programming Dynamically...................................................................................................... 772
- Putting Dynamic to Use........................................................................................... 774
- Classic examples......................................................................................................................... 774
- Making static operations dynamic............................................................................................... 775
- Understanding what's happening under the cover............................................................... 775
- Running with the Dynamic Language Runtime....................................................................... 776
- Dynamic Ruby..................................................................................................................... 777
- Dynamic C#....................................................................................................................... 778

- Chapter 2: Improving Productivity with Named and ................................................ 781
- Optional Parameters............................................................................................................. 782
- Reference types.................................................................................................................. 784
- Output parameters............................................................................................................... 785
- Named Parameters.................................................................................................................. 786
- Overload Resolution.............................................................................................................. 787

- Chapter 3: Helping Out with Interop ................................................... 789
- Using Dynamic Import........................................................................................................ 790
- Working without Primary Interop Assemblies....................................................................... 791
- Skipping the Ref Statement...................................................................................................... 793

- Chapter 4: Revising Generics...................................................................................... 795
- Variance............................................................................................................................... 796
- Contravariance............................................................................................................... 796
- Covariance........................................................................................................................... 798

## Index ................................................................................................................ 799

## Introduction

2010 All-in-One Dummies represents a different way of looking at programming languages. Rather than present the For Dummies format, which includes only 350 pages on quite a large subject, the book was expanded to include a broader scope and just a few pages were.

So, although you find all the original C# For Dummies goodness in your book, you also find discussions about Visual Studio, Windows Presentation Foundation (WPF), service-oriented development, Web development, and a host of other topics. This book is a one-stop shop for a C# developer.

The C# programming language is a powerful, and at some years old, relatively mature descendant of the earlier C, C++, and Java languages. Programming with C# is lots of fun, and you're about to find out in this book.

Microsoft created C# as a major part of its .NET initiative. The company turned the specifications for the C# language to the ECMA ("ek-ma") international standards committee in the year of 2000 so that any company can, in theory, come up with its own version of C# written to run on any operating system, on a machine larger than a calculator.

When the first edition of this book was published, the Microsoft C# compiler was the only game in town, and its Visual Studio .NET suite of tools was the only way to program C# (other than at the Windows command line). Since then, Visual Studio has undergone three major revisions — the latest is Visual Studio 2010. And, at least two others have entered the C# game.

You can now write and compile C# programs on Windows and a variety of Unix-based machines using implementations of .NET and C#, as Mono (www.mono-project.com), an open source project sponsored by Nov Corporation. Version 1.2 was released in November 2006. Though Mono lags .NET by half a version or so, it appears to be moving fast, having implemented basically all of .NET 1.1 and .NET 2.0.

Both Mono and a well developed competitor, Portable .NET (www.dotnet.org), claim to run C# programs on Windows and a variety of flavors, including Linux and the Apple Macintosh operating system. At the time of this writing, Portable .NET reaches the greater number of flavors, whereas Mono boasts a more complete .NET implementation. So choosing between them can be complicated, depending on your project, your platform, and your goals. (Books about programming for these platforms are becoming available already. Check online booksellers.)
