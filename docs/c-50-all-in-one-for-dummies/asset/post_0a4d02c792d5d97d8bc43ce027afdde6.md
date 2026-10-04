
# Introduction

C# 5.0 All-in-One For Dummies represents a different way of looking at programming languages. Rather than present the standard For Dummies format, which includes only 350 pages on quite a large subject, the book was expanded to include a broader scope and just a few pages were added.

So, although you find all the original C# For Dummies goodness in this book, you also find discussions about Visual Studio, Windows Presentation Foundation (WPF), service-oriented development, web development, and a host of other topics. This book is a one-stop shop for a C# developer.

The C# programming language is a powerful and, at some 11 years old, relatively mature descendant of the earlier C, C++, and Java languages. Programming with C# is lots of fun, as you’re about to find out in this book.

Microsoft created C# as a major part of its .NET initiative. The company turned over the specifications for the C# language to the ECMA (pronounced “ek-ma”) international standards committee in the summer of 2000 so that any company can, in theory, come up with its own version of C# written to run on any operating system, on any machine larger than a calculator.

When the first edition of this book was published, the Microsoft C# compiler was the only game in town, and its Visual Studio .NET suite of tools was the only way to program C# (other than at the Windows command line). Since then, however, Visual Studio has undergone three major revisions — the latest is Visual Studio 2012. And, at least two other players have entered the C# game.

You can now write and compile C# programs on Windows and a variety of Unix-based machines using implementations of .NET and C#, such as Mono (www.mono-project.com), an open source software project sponsored by Novell Corporation. Version 1.2 was released in November 2006. Though Mono lags Microsoft .NET by half a version or so, it appears to be moving fast, having implemented basically all of .NET 1.1 and much of .NET 2.0, along with those versions of C#.

Both Mono and a less well developed competitor, Portable .NET (www.dotgnu.org/pnet.htm), claim to run C# programs on Windows and a variety of Unix flavors, including Linux and the Apple Macintosh operating system. At the time of this writing, Portable .NET reaches the greater

![](img/6df7bb88e9302e98442acc219cfbd7fc_27_0.png) number of flavors, whereas Mono boasts a more complete .NET implementation. So choosing between them can be complicated, depending on your project, your platform, and your goals. (Books about programming for these platforms are becoming available already. Check online booksellers.)

Open source software is written by collaborating groups of volunteer programmers and is usually free to the world.

A description of how to make C# and other NET languages portable to other operating systems is far beyond the scope of this book. But you can expect that within a few years, the C# Windows programs that you discover how to write in this book will run on all sorts of hardware under all sorts of operating systems — matching the claim of Sun Microsystems' Java language to run on any machine. That's undoubtedly a good thing, even for Microsoft. The road to that point is still under construction, so it's no doubt riddled with potholes and obstacles to true universal portability for C#. But it's no longer just Microsoft's road.

For the moment, however, Microsoft Visual Studio has the most mature versions of C# and .NET and the most feature-filled toolset for programming with them.

Note: Though three authors contributed to this book, saying I rather than we throughout the main text seemed more economical, so that's what we (or I) do throughout.

# What's New in C# 5.0

Although much of C# 5.0 is still virtually the same as the previous version, this new version adds some exciting new features, most of which revolve around making it easier to write modern applications that are fast and fluid.

The principle feature that provides the speed enhancements to the end user experience is complete embracing of Asynchronous development through the language. Simply put, a developer can now write a piece of code that can run without blocking the user interface, and without using the System.Threading classes.

Because you know what they say: If you decide to use threading to solve a problem, now problems two have you.

Leaving aside a few of the more esoteric and advanced additions, I mention a few smaller items here and there as appropriate. (Don't worry if parts of this introduction are Geek to you. You'll get there.)

# About This Book

The goal of this book is to explain C# to you. To write usable programs, you need a specific coding environment. We’re betting that most readers will use Microsoft Visual Studio, although we suggest alternatives. Because this book is an All-in-One, we give you comprehensive coverage of Visual Studio in Book IV.

The original version of C# For Dummies (like all programming language books) focused on C# as a language, not all of the things you do with C#. This version of the book — in the mondo-size All-in-One format — covers Windows development, web development, service development, and .NET Framework development, such as graphics and databases.

Our goal is to make a one-stop shop for development with Microsoft products, though there is indeed more to the topics than fits in this book. Office development isn’t covered, for instance. SharePoint has way too much going on to cover it along with everything else (although Bill co-authored VSTO For Dummies). This book is designed to handle 20 percent of readers will be working on something we don’t cover.

# What You Need in Order to Use This Book

You need, at minimum, the .NET Common Language Runtime (CLR) before you can even execute the programs. Visual Studio 2012 copies the CLR onto your machine as part of its installation. Alternatively, you can download the .NET Software Development Kit (SDK) from the Microsoft website at mdn.microsoft.com. If all you need is C#, you can download the free version of Visual Studio, Visual Studio 2012 Express, from mdn.microsoft.com/vstudio/express. The Express versions include the new C# 5.0 features.![](img/6df7bb88e9302e98442acc219cfbd7fc_28_0.png) Alternatively, see SharpDevelop (www.icsharpcode.net), a good, free Visual Studio “workalike,” which is provided on the website for this book.![](img/6df7bb88e9302e98442acc219cfbd7fc_29_0.png) You can still create most of the programs in this book using earlier versions of Visual Studio, such as Visual Studio 2008, if you need to. The exceptions are the programs that cover the new features available only in C# 5.0.

# Conventions Used in This Book

Throughout this book, we use several conventions to help you get your bearings. Terms that aren’t “real words,” such as the names of program variables, appear in this font to minimize confusion. Program listings are offset from the text this way:

```
use System;
namespace MyNameSpace
{
    public class MyClass
    {
    }
}
```Each listing is followed by a clever, insightful explanation. Complete programs are included on the website for your viewing pleasure; small code segments are not.

When you see a command arrow, as in the instruction “Choose File→Open With→Notepad,” you simply choose the File menu option. Then, from the menu that appears, choose Open With. Finally, from the resulting submenu, choose Notepad.

# How to Use This Book

We’ve made this book as easy to use as possible. Figuring out a new language is hard enough — why make it any more complicated than it needs to be? Though this book is divided into seven minibooks, we use an even easier subdivision.

Books I and II comprise the bulk of the original C# For Dummies book, and they cover the C# language, updated for version 5.0. Books III and IV cover technologies that are peripheral to C#. Books V, VI, and VII cover the three main types of development you do in C# — Windows Presentation Foundation, web development, and service-oriented programming.
