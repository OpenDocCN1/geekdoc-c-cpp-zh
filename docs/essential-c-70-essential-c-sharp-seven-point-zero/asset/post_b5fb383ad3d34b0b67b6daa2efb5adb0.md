
I hope you find this book to be a great resource in establishing your C# expertise and that you continue to reference it for those areas that you use less frequently well after you are proficient in C#.

—Mark Michaelis

IntelliTect.com/mark

Twitter: @IntelliTect, @MarkMichaelis

> Register your copy of Essential C# 7.0 on the InformIT site for convenient access to updates and/or corrections as they become available. To start the registration process, go to informit.com/register and log in or create an account. Enter the product ISBN (9781509303588) and click Submit. Look on the Registered Products tab for an Access Bonus Content link next to this product, and follow that link to access any available bonus materials. If you would like to be notified of exclusive offers on new editions and updates, please check the box to receive email from us.

## Acknowledgments

No book can be published by the author alone, and I am extremely grateful for the multitude of people who helped me with this one. The order in which I thank people is not significant, except for those who come first. Given that this is now the sixth edition of the book, you can only imagine how much my family has sacrificed to allow me to write over the last 10 years (not to mention the books before that). Benjamin, Hanna, and Abigail often had a Daddy distracted by this book, but Elisabeth suffered even more so. She was often left to take care of things, holding the family's world together on her own. (While on vacation in 2017, I spent days indoors writing while they would much have preferred to go to the beach.) A huge sorry and ginormous Thank You!

Over the years, many technical editors reviewed each chapter in minute detail to ensure technical accuracy. I was often amazed by the subtle errors these folks still managed to catch: Paul Bramsman, Kody Brown, Ian Davis, Doug Dechow, Gerard Frantz, Thomas Heavey, Anson Horton, Brian Jones, Shane K. Ercheval, Angelika Langer, Eric Lippert, John Michaelis, Jason Morse, Nicholas Paldino, Jon Skeet, Michael Stokesbary, Robert Stokesbary, John Timney, Neal Lundby, Andrew Comb, Jason Peterson, Andrew Scott, Dan Haley, Phil Spokas (who helped with portions of the writing in Chapter 22), and Kevin Bost.

Of course, Eric Lippert is no less than amazing. His grasp of C# is truly astounding, and I am very appreciative of his edits, especially when he pushed for perfection in terminology. His improvements to the C# 3.0 chapters were incredibly significant, and in the second edition my only regret was that I didn't have him review all the chapters. However, that regret is no longer. Eric painstakingly reviewed every *Essential C# 4.0* chapter and even served as a contributing author for *Essential C# 5.0* and *Essential C# 6.0*. I am extremely grateful for his role as a technical editor for *Essential C# 7.0*. Thanks, Eric! I can't imagine anyone better for the job. You deserve all the credit for raising the bar from good to great.

Like Eric and C#, there are fewer than a handful of people who know .NET multithreading as well as Stephen Toub. Accordingly, Stephen concentrated on the two rewritten (for a third time) multithreading chapters and their new focus on async support in C# 5.0. Thanks, Stephen!

Thanks to everyone at Pearson/Addison-Wesley for their patience in working with me in spite of my frequent focus on everything else except the manuscript. Thanks to Trina Fletcher Macdonald, Anna Popick, Julie Nahil, and Carol Lallier. Trina deserves a special medal for putting up with the likes of me when she clearly was juggling myriad other more important things as well. Also, Carol's attention to detail was invaluable, and her ability to improve the writing and red-line potential writing faux pas (even catching them when they occurred in code listings) was so appreciated.

### About the Author

**Mark Michaelis** is the founder of IntelliTect, a high-end software engineering and consulting company where he serves as the chief technical architect and trainer. Mark speaks at developer conferences and has written numerous articles and books. Currently, he is the Essential .NET columnist for *MSDN Magazine*.

Since 1996, Mark has been a Microsoft MVP for C#, Visual Studio Team System, and the Windows SDK. In 2007, he was recognized as a Microsoft Regional Director. He also serves on several Microsoft software design review teams, including C# and VSTS.

Mark holds a bachelor of arts in philosophy from the University of Illinois and a masters in computer science from the Illinois Institute of Technology.

When not bonding with his computer, Mark is busy with his family or playing racquetball (having suspended competing in Ironman back in 2016). Mark lives in Spokane, Washington, with his wife, Elisabeth, and three children, Benjamin, Hanna, and Abigail.

### About the Technical Editor

**Eric Lippert** works on developer tools at Facebook; he is a former member of the C# language design team at Microsoft. When not answering C# questions on StackOverflow or editing programming books, Eric does his best to keep his tiny sailboat upright. He lives in Seattle, Washington, with his wife, Leah.

## 1 Introducing C#

C# is now a well-established language that builds on features found in its predecessor C-style languages (C, C++, and Java), making it immediately familiar to many experienced programmers.¹ Furthermore, the C# programming language can be used to build software components and applications that run on a wide variety of operating systems (platforms).

![](img/ef6a8a417630b222bfb3f3b949facff0_37_0.png)

This chapter introduces C# using the traditional Hello World program. It focuses on C# syntax fundamentals, including defining an entry point into the C# program, which will familiarize you with the C# syntax style and structure and enable you to produce the simplest of C# programs. Prior to the discussion of C# syntax fundamentals is a summary of managed execution context, which explains how a C# program executes at runtime. This chapter ends with a discussion of variable declaration, writing and retrieving data from the console, and the basics of commenting code in C#.

### Hello, World

The best way to learn a new programming language is to write code. The first example is the classic Hello World program. In this program, you will display some text to the screen.

Listing 1.1 shows the complete Hello World program; in the following sections, you will compile and run the code.

**LISTING 1.1: Hello World in C#**²

```csharp
class HelloWorld
{
    static void Main()
    {
        System.Console.WriteLine("Hello. My name is Inigo Montoya.");
    }
}
```

> **NOTE**
> C# is a case-sensitive language: Incorrect case prevents the code from compiling successfully.

Those experienced in programming with Java, C, or C++ will immediately see similarities. Like Java, C# inherits its basic syntax from C and C++,³ Syntactic punctuation (such as semicolons and curly braces), features (such as case sensitivity), and keywords (such as class, public, and void) are familiar to programmers experienced in these languages. Beginners and programmers from other languages will quickly find these constructs intuitive.

¹ The first C# design meeting took place in 1998.
² Refer to the movie *The Princess Bride* if you're confused about the Inigo Montoya references.
³ When creating C#, the language creators reviewed the specifications for C/C++, literally crossing out the features they didn't like and creating a list of the ones they did like. The group also included designers with strong backgrounds in other languages.

### Creating, Editing, Compiling, and Running C# Source Code

Once you have written your C# code, it is time to compile and run it. You have a choice of which .NET implementation(s) to use—sometimes referred to as the .NET framework(s). Generally, the implementation is packaged into a software development kit (SDK). The SDK includes the compiler, the run-time execution engine, the framework of pragmatically accessible functionality that the runtime can access (see “Application Programming Interface” later in the chapter), and any additional tooling (such as a build engine for automating build steps) that might be bundled with the SDK. Given that C# has been publicly available since 2000, there are several different .NET frameworks to choose from (see “Multiple .NET Frameworks” later in the chapter).

For each .NET framework, the installation instructions vary depending on which operating system you are developing on and which .NET framework you select. For this reason, I recommend you visit https://www.microsoft.com/net/download for download and installation instructions, selecting first the .NET framework and then the package to download based on which operating system you will be developing for. While I could provide further details here, the .NET download site has the most updated instructions for each combination supported.

If you are unsure about which .NET framework to work with, choose .NET Core by default. It works on Linux, macOS, and Microsoft Windows and is the implementation where the .NET development teams are applying the majority of their investments. Furthermore, because of the cross-platform capabilities, I will favor .NET Core instructions inline within the chapters.

There are also numerous ways to edit your source code, including with the most rudimentary of tools, such as Notepad on Windows, TextEdit on Mac/macOS, or vi on Linux. However, you’re likely to want something more advanced so that at least your code is colorized. Any programming editor that supports C# will suffice. If you don’t already have a preference, I recommend you consider the open source editor Visual Studio Code (https://code.visualstudio.com). Or, if you are working on Windows or Mac, consider Microsoft Visual Studio 2017 (or later)—see https://www.visualstudio.com. Both are available free of charge.

In the next two sections, I provide instructions for both editors. For Visual Studio Code, we rely on the command line (Dotnet CLI) for creating the initial C# program scaffolding in addition to compiling and running the program. For Windows and Mac, we focus on using Visual Studio 2017.
