
- Chapter 14 introduces a new feature in .NET 3.5: Language Integrated Query (LINQ). It covers all the important implementations of LINQ — LINQ to Objects, LINQ to XML, LINQ to Dataset, and LINQ to SQL.

- Chapter 15 explores the concept of assemblies. In .NET, the basic unit deployable is called an assembly. Assemblies play an important part of the development process where understanding how they work is useful in helping you develop scalable and efficient .NET applications.

## Part II: Application Development Using C#

- Chapter 16 demonstrates how you can build a Windows application using the C# language. The sample application illustrates how to perform FTP using the classes available in the .NET Framework. You will also see how to perform printing in a .NET application and how to deploy Windows applications using the ClickOnce technology.

- Chapter 17 takes you through building an ASP.NET web application in C#. You perform data binding using the new LinqDataSource control and see how to AJAX-enable your web pages.

- Chapter 18 illustrates Windows Mobile development using the .NET Compact Framework, a subset of the .NET Framework. It examines the basics of the Windows Mobile development and builds a sample RSS reader application. Finally, it shows you how to create a professional setup package for your application so that it can be distributed to your readers for installation.

- Chapter 19 helps you get started with Silverlight and provides an opportunity for you to get a feel for how Silverlight development works. It covers Silverlight 1.0 and 2, and contains several examples showing the capabilities of Silverlight, including animation, media, and .NET integration.

- Chapter 20 provides a quick introduction to the new Windows Communication Foundation (WCF) technology and shows how it addresses some of the limitations of today's web services technology. While most books and conferences focus heavily on the theory behind WCF, this chapter shows you how to build WCF services and then explains the theory behind them. It ends with an example that creates a ticketing application, allowing multiple clients to obtain updated seat information in real time.

## Part III: Appendixes

- Appendix A lists the various keywords in C# that are predefined and have special meanings to the compiler.

- Appendix B summarizes the features of the various versions of the .NET Framework and explains how to use the Object Browser feature in Visual Studio 2008 to browse the available namespaces and classes in the .NET Framework.

- Appendix C shows you how to generate MSDN-style documentation for your project using Visual Studio 2008 and a third-party documentation generation tool — Sandcastle.

## What You Need to Use This Book

For all the examples demonstrated in this book, I used Microsoft Visual Studio Team System 2008. However, Microsoft has released a plethora of editions of Visual Studio designed for the different types of C# developers:

- [ ] Visual Web Developer 2008 Express Edition
- [ ] Visual C# 2008 Express Edition
- [ ] Visual Studio 2008 Standard Edition
- [ ] Visual Studio 2008 Professional Edition
- [ ] Visual Studio 2008 Team System Architecture Edition
- [ ] Visual Studio 2008 Team System Database Edition
- [ ] Visual Studio 2008 Team System Development Edition
- [ ] Visual Studio 2008 Team System Test Edition
- [ ] Visual Studio 2008 Team System Team Suite

*For a detailed discussion of the features available in each edition, check out the following URL:*
http://msdn.microsoft.com/en-us/vs2008/products/cc149003.aspx.

Express editions are designed for hobbyists and are available for download at no charge. This is a great way to get started with Visual Studio 2008 and is ideal for students and beginning programmers. However, if you are a professional developer, you should purchase either the Standard or Professional Edition. If you are developing Windows Mobile applications, you need the Professional Edition (or higher). If you are working in a large development environment and need to develop collaboratively with other developers on large projects, check out the Team System editions.

*If you are not ready to purchase Visual Studio 2008, you can always download a 90-day trial edition of Visual Studio 2008 Professional from* http://msdn.microsoft.com/en-us/vs2008/products/cc268305.aspx.

Depending on the edition of Visual Studio you are using, some of the steps illustrated in this book may not appear exactly the same on your screen. However, the differences are minor, and you should not have any problem in following the steps outlined in each chapter.

In addition, readers using Windows Vista should launch Visual Studio 2008 (as well as the Command Prompt window) in Administrator mode. To do so:

- [ ] Click on Vista Start button.
- [ ] Locate the program you want to launch (Visual Studio 2008, or Command Prompt).
- [ ] Right-click on the program and select Run as Administrator.

## Conventions

A number of conventions are used throughout the book to help you get the most from the text and keep track of what's happening.

Boxes like this one hold important, not-to-be forgotten information that is directly relevant to the surrounding text.

*Tips, hints, tricks, and asides to the current discussion are offset and placed in italics like this.*

As for styles in the text:

- New terms and important words are highlighted and introduced.
- Keyboard strokes look like this: Ctrl+A.
- Filenames, URLs, and code within the text looks like this: `persistence.properties`.
- Code is presented in two different ways:

```
Code examples nearly always look like this.
```

Gray highlighting is used to show where new code is added to existing code, or to point out a specific section of code that's being explained in the text.

## Source Code

As you work through the examples in this book, you may choose either to type in all the code manually or to use the source code files that accompany the book. All of the source code used in this book is available for download at www.wrox.com. Once at the site, simply locate the book's title (either by using the Search box or by using one of the title lists), and click the Download Code link on the book's detail page to obtain all the source code for the book.

## Errata

Every effort is made to ensure that there are no errors in the text or in the code. However, no one is perfect, and mistakes do occur. If you find an error such as a spelling mistake or faulty piece of code in one of our books, we would be grateful for your feedback. By sending in errata, you may save another reader hours of frustration, and at the same time you will be helping us provide even higher-quality information.

## Introduction

To find the errata page for this book, go to www.wrox.com and locate the title using the Search box or by using one of the title lists. Then, on the book details page, click the Book Errata link. On this page, you can view all errata that has been submitted for this book and posted by Wrox editors. A complete book list including links to each book's errata is also available at www.wrox.com/misc-pages/booklist.shtml.

If you don't spot “your” error on the Book Errata page, go to www.wrox.com/contact/techsupport.shtml, and complete the form there to send us the error you have found. We'll check the information and, if appropriate, post a message to the book's errata page and fix the problem in subsequent editions of the book.

## p2p.wrox.com

For author and peer discussion, join the P2P forums at p2p.wrox.com. The forums are a web-based system for you to post messages relating to Wrox books and related technologies and interact with other readers and technology users. The forums offer a subscription feature to email you topics of interest of your choosing when new posts are made to the forums. Wrox authors, editors, other industry experts, and your fellow readers are present on these forums.

At http://p2p.wrox.com, you will find a number of different forums that will help you not only as you read this book but also as you develop your own applications. To join the forums, just follow these steps:

1. Go to p2p.wrox.com, and click the Register link.
2. Read the terms of use, and click Agree.
3. Complete the required information to join as well as any optional information you wish to provide, and click Submit.
4. You will receive an email with information describing how to verify your account and complete the joining process.

> > You can read messages in the forums without joining P2P but to post your own messages, you must join.

Once you join, you can post new messages and respond to messages other users post. You can read messages at any time on the web. If you would like to have new messages from a particular forum emailed to you, click the Subscribe to this Forum icon by the forum name in the forum listing.

For more information about how to use the Wrox P2P, be sure to read the P2P FAQs for answers to questions about how the forum software works as well as many common questions specific to P2P and Wrox books. To read the FAQs, click the FAQ link on any P2P page.
