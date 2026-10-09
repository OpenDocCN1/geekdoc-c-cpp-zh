
the older way of compilation. There is no turning back. ☺

## Book Organization

The lessons in this book are organized into four parts: First Steps, Moving Forward, Having Fun, and Final Projects.

This division is somewhat arbitrary, but the first part, Part I: First Steps, mostly focuses on general programming. If you are coming from a different programming language background, especially languages like C++ or Java, then you will feel comfortable with the lessons in this part. One thing to note is that we introduce "generics" rather early in the book, unlike many "introductory" beginner's books. Generics is an essential part of the modern C# programming language.

The second part, Part II: Moving Forward, mainly focuses on the object oriented style programming in C#. In some object oriented programming (OOP) languages, there is only one or two constructs, such as class or struct, to create a custom type. In C#, there are several. In particular, C# has class, struct, record, and interface, among others.

In Part II, we discuss the fundamental concepts of object oriented programming, and the C#s support for the OOP. In addition, this part introduces some features in C# that support the functional programming style. We will also go over some basic examples of Web programming in C# as well in this part.

In Part III: Having Fun, we will cover a few independent topics, mostly to help the readers internalize the important programming concepts in C#, like object-oriented and functional programming styles.

Finally, in Part IV: Final Projects, we will work on a few hands-on projects. We will design and implement a program to solve Rubik's Cube, among other things. The readers are encouraged to tackle all the projects in this part. They are excellent projects for beginning programmers as well as more experienced developers.

## Notes on C# 10.0

This book was completely revised after the release of C# 10.0, in the late 2021 and early 2022. Although the C# changes were relatively minor, there were still a few parts in the book that required some substantial updates.

Most notably, C# 10.0 introduced another way to create a custom type, namely, `record struct`. This is essentially a combination of the C# 9.0 record (which can now be alternatively declared as `record class`) and the struct.

Another major change is that C# now allows overriding the parameterless default constructor of the struct type. This can have some far-reaching implications depending on how you have been using structs.

Furthermore, C# 10.0 also includes the features known as the "global using", "implicit usings", and "file-scoped namespace" declarations. They are mostly "cosmetic", but they can change the general look of any C# code (along with the C# 9.0 top-level statement feature). And hence they are really significant changes.

We will discuss these features throughout this revised edition.

## Final Remarks

Regarding the sample programs, one thing to note is that we do not include comments in the code. Comments will mostly add clutter in books like this. The content of the book serves as code comments. And, more. In practice, writing good comments, and documentations, is a very important skill to learn.

All exercises are "optional" in that the lessons in the book mostly focus on the "code reading", and not writing. The exercises may also require knowledge on some subjects that we do not thoroughly cover in this book.

As stated, C# may not be the easiest language to learn. It has a lot of "features". There are many different ways to use C# for the same task. It will take time and effort to become really proficient in the modern C#. Hope you find this book helpful in your journey into the programming world, in C#.

Let's get started.

## Part I: First Steps

The beginning is the most important part of the work. -Plato

The C# programs run on the .NET runtime, among others. A "runtime" can include both the build time and run time support, including the "standard libraries". We will mostly use the .NET runtime version 6 in this book.

We will use the C# version 10.0, which are the default C# language version on .NET 6. The .NET is a cross-platform runtime, meaning that it is not restricted only to the Windows platform. You can run any modern C# programs on .NET, using the .NET libraries.

The word "program" can mean, depending on the context, a binary program, e.g., an executable on a particular computer architecture, or a source program, which is typically a collection of source code files, (Or, even a part of the complete program.)

A C# binary program can be either an executable or a library. In the .NET world, they are called the "assemblies". An assembly can be either an executable (e.g., typically with the file name extension `.exe` on Windows) or a dynamically linked library (e.g., typically with the extension `.dll` on Windows).

C# is a class-based programming language. A `class` plays an essential role in C#. The `class`, and its cousins, allow the programmers to create custom types, which are the core components of any C# programs.

In this first part, we will primarily focus on the programming styles using the built-in or library-supplied types. We will start defining and using our own custom types from the second part.

The code samples in this book are meant to be *read*. You do not have to type them on the computer to get the "hands-on" experience. Just to be clear, however, you will need to make conscious efforts for "reading" (that involves "thinking" ☺). Otherwise, the benefits will be minimal.

### 1.1. Agenda - The Simplest C# Program, Console.WriteLine

Of course, we will *have to* start with a "hello world" program. ☺

![](img/25af69ec45b3c0b589a8dccd0c2a88be_25_0.png)

### 1.2. Code Reading - Hello World 1

This is the simplest C# program.

*hello-world-1/Program.cs*

```
    Console.WriteLine("Hello World!!!");
```

Throughout this book, the label of a source code snippet indicates that the example code is taken from a certain file in a certain folder (on the author’s computer). The particular source file names, and the file paths, are largely irrelevant to the execution of a C# program.

If you are an absolute beginner, then a C# “source file” is just a text file, with a “.cs” extension, which includes the source code. Writing a program means writing one or more of these source files.

#### 1.2.1. Explanation

The program comprises a single source file, “Program.cs”. The file contains a single line of code. It cannot be simpler than this.

You can quickly run the program as follows using the dotnet CLI tool (assuming that you have it installed on your computer), from the same directory where the source file is in:

```
dotnet run
```

It produces the following output:

```
Hello World!!!
```

Yes, as promised, it is indeed a hello world program. The program prints out a text “Hello World!!!” to the console and it terminates.

Throughout this book, we will primarily use the command line interface (CLI). If you are not familiar with any "terminal program", then this might be a good time to learn some basics specific to your platform (e.g., Linux, Mac, or Windows).

![](img/25af69ec45b3c0b589a8dccd0c2a88be_27_0.png)

The book focuses on the fundamentals of programming, and the CLI is more than sufficient for illustrating the basic, and even advanced, programming concepts. Incidentally, there is a quick note at the end of this lesson regarding how to set up a "development environment".

![](img/25af69ec45b3c0b589a8dccd0c2a88be_27_1.png)

This book is *for reading*. The author does all the work. 😊 He even includes all the relevant outputs from all (or, most of) the sample programs in this book. The readers can just sit back and "read". 😊

#### 1.2.2. Grammar

A C# program primarily contains the "custom type definitions", using constructs like *struct* or *class*, as we will learn throughout this book.

This hello world program is an exception, however. It merely includes one "statement". A statement is an instruction to the computer as to what needs to be done. The statements written in a program like this, instead of being included in other constructs like classes or methods, are called the "top level statements" in C# (C# 9.0 and later).

An executable C# program can have at most one source file that contains the top level statements. Furthermore, the top level statements, if present, must be in the beginning part of the source file, before any custom type definitions.

The top level statements can also include static method definitions, as we will illustrate in the next lessons. The top level statement feature (new as of 9.0) makes the main part of a program look a bit simpler by eliminating some boilerplate code.
