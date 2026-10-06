
# Introduction

F# is a functional programming language from Microsoft. It is the first-class language shipped in Visual Studio. It has been applied successfully in several areas, such as in the areas of financial software and web development. If you are a C# developer and want to use functional programming to write concise code with fewer bugs, F# is the tool for you.

F for C# Developers introduces, in an organized way, the F# language and several applications. It starts from how F# can perform imperative and object-oriented programming tasks and moves to covering unique F# features, such as type providers. By introducing F# design patterns with a large number of samples, the book not only delivers a basic introduction but also helps you apply F# in your daily programming work.

In addition to covering F# core features, I also discuss F# HTML5 development, F# Azure development, and using general-purpose processing units (GPGPUs) with F#. By beyond the explanatory content, each chapter includes examples and downloadable sample projects you can explore for yourself.

# Who Should Read this Book

I write this book to help existing C# developers understand the core concepts of F# and help C# developers use F# in their daily work. It is especially useful for C# programmers looking to write concise code for algorithm design, web development, and cloud development. Although most readers have no prior experience with F#, the book is also useful for those familiar with earlier versions of F# and who are interested in learning about the newest features.

You should have at least a minimal understanding of .NET development and object-oriented programming concepts to get the most benefit from this book. You should also have a basic understanding of data structures and generic algorithms. Experience in using C# is required as well.

# Who Should Not Read This Book

This book is aimed at both experienced .NET C# developers who are interested in extending their knowledge in functional programming and beginners in F# who want to understand F# and apply F# to their daily programming work. If you have no C# programming experience, this book might be difficult for you.

# Organization of This Book

This book is divided into three sections, each of which focuses on a different aspect. Part I, "C# and F#," introduces how to port your C# knowledge to F#. This section introduces basic data structures and performing object-oriented implementations using F#. Part II, "F#'s Unique Features," introduces unique F# features and how to use them in your daily programming work. Part III, "Real-World Applications," introduces several real-world applications, including web development, Azure cloud development, and GPGPU.

# Finding Your Best Starting Point in This Book

The various sections of F for C# Developers cover a wide range of technologies. Depending on your needs and your existing understanding, you might want to focus on specific areas of the book. Use the following table to determine how best to proceed through the book.

| If you are | Follow these steps |
| :--- | :--- |
| New to F# but experienced with C# | Focus on Part I to understand the basics and Part II for some unique F# features |
| Familiar with earlier versions of F# | Briefly read Parts I and II if you need a refresher on the core concepts, but also want to focus on type providers. |

Most of the book’s chapters include hands-on samples that let you try out the concepts just learned. No matter which sections you choose to focus on, be sure to download and install the sample applications on your system.

# Conventions and Features in This Book

This book presents information using conventions designed to make the information readable and easy to follow:

- Boxed elements with labels such as "Note" provide additional information or alternative methods for completing a step successfully.
- Text that you type (apart from code blocks) appears in bold. A plus (+) between two key names means that you must press those keys at the same time. For example, "Press Alt+Tab" means that you hold down the Alt key while you press the Tab key.

# System Requirements

You will need the following hardware and software to complete the practice exercises in this book:

- Windows 7 or Windows 8
- Visual Studio 2012, any edition (multiple downloads might be required if you're using Express Edition products)
- 1 GB (32 Bit) or 2 GBs (64 Bit) RAM
- 3.5 GBs of available hard disk space
- DirectX 9 capable video card running at 1024 x 768 or higher-resolution display
- DVD-ROM drive (if installing Visual Studio from DVD)
- Internet connection to download software or chapter examples
- If you want to run the GPU code, you need an NVIDIA graphics card and you need to download CUDA SDK from the NVIDIA web site.

Depending on your Windows configuration, you might require Local Administrator rights to install or configure Visual Studio 2012.

# Code Samples

Most of the chapters in this book include exercises that let you interactively try out new material learned in the main text. All sample projects, in both their pre-exercise formats, can be downloaded from F# sample pack site
(http://fsharp3sample.codeplex.com/)

Follow the instructions to download the 670266_FSharp4CSharp_CompanionContent.zip file.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

# Installing the Code Samples

Follow these steps to install the code samples on your computer so that you can use them with the exercises in this book:

- 1. Unzip file that you downloaded.
- 2. If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- Using the: from the same.

# Using the Code Samples

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- If prompted, review the displayed end user license agreement. If you accept the terms, select the accept option, and then click Next.

> Note: In addition to the code samples, your system should have Visual Studio 2012.

- Using the: from the same.

# Errata & Book

If you find an error that is not already listed, you can report it to us at:

```
http://aka.ms/Fsharerrata
```

If you need additional support, email mspinput@microsoft.com.
