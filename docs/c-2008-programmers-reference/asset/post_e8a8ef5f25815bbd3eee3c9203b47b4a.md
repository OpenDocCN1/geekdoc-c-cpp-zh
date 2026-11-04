
- Displaying Progress Using the UpdateProgress Control 565
- Displaying a Modal Dialog Using the ModalPopupExtender Control 566
- Summary 572

## Chapter 18: Developing Windows Mobile Applications 573
- The Windows Mobile Platform 574
- Developing Windows Mobile Applications Using the .NET Compact Framework 576
- Obtaining the Appropriate SDKs and Tools 578
- Building the RSS Reader Application 580
- Building the User Interface 581
- Creating the Helper Methods 583
- Wiring All the Event Handlers 589
- Testing Using Emulators 596
- Testing Using Real Devices 597
- Deploying the Application 598
- Creating a CAB File 598
- Creating a Setup Application 603
- Summary 616

## Chapter 19: Developing Silverlight Applications 617
- The State of Silverlight 617
- Obtaining the Tools 619
- Architecture of Silverlight 620
- Building a Silverlight UI Using XAML 621
- Creating a Bare-Bones Silverlight Application 621
- Understanding XAML 623
- Crafting XAML Using Expression Blend 2 635
- Silverlight 1.0 645
- Animation — Part 1 645
- Animations — Part 2 650
- Playing Media 654
- Creating Your Own Media Player 663
- Silverlight 2.0 675
- Creating the Project Using Visual Studio 2008 676
- Summary 694

## Contents
- Chapter 20: Windows Communication Foundation 695
- What Is WCF? 695
- Comparing WCF with ASMX Web Services 700
- Your First WCF Service 700
- Consuming the WCF Service 708
- Understanding How WCF Works 710
- WCF Communication Protocols 710
- The ABCs of WCF 710
- Messaging Patterns 713
- Hosting Web Services 713
- Building WCF Services 714
- Exposing Multiple Endpoints 714
- Creating Self-Hosted WCF Service 720
- Implementing WCF Callbacks 728
- Calling WCF Services from an AJAX Page 741
- Summary 745
- Part III: Appendices 747
- Appendix A: C# Keywords 749
- Appendix B: Examining the .Net Class Libraries Using the Object Browser 757
- Appendix C: Generating Documentation for Your C# Applications 765
- Index 781

## Introduction

Since the release of the Microsoft .NET Framework in July 2000, the C# programming language has gone through a few iterations to its latest version, 3.0. Over the years, the C# language has gained a lot of followers, partly due to its syntax, which is familiar to Java and C programmers. The clear syntax of the language made it easy to learn, and it's a popular choice for beginning programmers. In addition, the C# language is gaining a lot of traction in the Visual Basic camp, especially among VB6 programmers, who needed to move to .NET and did not want to learn a totally new variant of the Visual Basic language — Visual Basic .NET.

The latest version of C# 3.0 comes with .NET Framework 3.5. It contains many new features that make the language more intuitive and powerful. Coupled with Visual Studio 2008, Microsoft's flagship development environment, developing applications using C# is now available to a wide audience.

In writing this book, I used the approach I believe is the easiest way to learn a new language — by examples. Often, books and articles get into too much of the theory without showing the readers what the concept looks like in code. For each topic, I try to provide numerous examples to illustrate the concept, and I would encourage you to make changes to the program to explore further. If you are an experienced programmer, you can jump directly to a particular chapter, as each chapter comes with independent examples.

## Who This Book Is For

This book is for programmers of all levels. Beginning programmers should find the C# language easy to learn through the many code examples provided in each chapter. Experienced programmers can jump directly to individual chapters covering the topics of interest to them.

A conscious effort is made to illustrate each topic with independent code examples so that readers who want clarification on a topic do not need to wade through the entire chapter.

This book is ideal for the working programmer as well as students taking a semester course in C# programming. The sample projects covered in chapters 16 to 20 provide numerous project ideas as well as motivation for readers to get started working on bigger projects.

## What This Book Covers

This book is divided into three parts. Part I covers the C# language fundamentals; Part II covers application development using C#, and Part III provides three appendices that cover the list of C# keywords, the .NET class libraries, and document generation using the Sandcastle utility.

## Part I: C# Fundamentals

- Chapter 1 introduces the .NET Framework. It examines the key components in the .NET Framework as well as the role played by each of the components. In addition, it discusses the relationships between the various versions of the framework, from version 1.0 to the latest 3.5.
- Chapter 2 covers the use of Microsoft Visual Studio 2008 as the tool for C# development. Visual Studio 2008 is an extremely versatile and powerful environment for developing .NET applications. This chapter explores some of the common features that you will likely use in the process of your development work.
- Chapter 3 introduces the syntax of the C# language and covers all the important topics: C# keywords, variables, constants, comments, XML documentation, data types, flow control, loops, operators, and preprocessor directives.
- Chapter 4 tackles one of the most important topics in C# programming — classes and objects. Classes are essentially templates from which you create objects. In C# .NET programming, everything you deal with involves classes and objects. This chapter provides a firm foundation in the use and creation of classes for code reuse.
- Chapter 5 explains how interfaces can be used to define the contract for a class. It also discusses differences between an interface and an abstract class.
- Chapter 6 looks at how inheritance facilitates code reuse, enabling you to extend the functionality of code that you have already written. This book explains the different types of inheritance and how to define overloaded methods and operators.
- Chapter 7 introduces the concept of delegates and events used in object oriented programming, and discusses what a delegate is and how delegates are used to implement events.
- Chapter 8 examines strings handling in C# and the various ways to manipulate them. For more complex strings pattern matching, you can use regular expressions. This chapter also covers the various ways to format your strings data.
- Chapter 9 looks into the basics of generics and how you can use them to enhance efficiency and type safety in your applications. Generics enable developers to define type-safe data structures without binding to specific fixed data types at design time.
- Chapter 10 explains how to write multithreaded applications using the Thread class in the .NET Framework. It also shows you how to create and synchronize threads as well as how to write thread-safe Windows applications.
- Chapter 11 delves into the concepts of files and streams in .NET. With streams, you can perform a wide range of tasks, including compressing and decompressing data, serializing and deserializing data, and encrypting and decrypting data. This chapter covers the various ways to manipulate files and the various stream objects in .NET.
- Chapter 12 deals with exception handling. An exception is a situation that occurs when your program encounters an error that it is not expecting during runtime. Understanding how to handle exceptions makes your program more robust and resilient.
- Chapter 13 examines arrays and collections. It discusses the many collection classes that you can use to represent groups of data in .NET.
