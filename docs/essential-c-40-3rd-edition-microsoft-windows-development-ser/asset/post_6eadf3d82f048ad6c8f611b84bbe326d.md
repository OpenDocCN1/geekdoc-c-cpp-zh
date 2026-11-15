
- 2. For readers already familiar with C#, this book provides insight into some of the more complex programming paradigms and provides in-depth coverage of the features introduced in the latest version of the language, C# 4.0 and .NET Framework 4.

- 3. It serves as a timeless reference, even after you gain proficiency with the language.

The key to successfully learning C# is to start coding as soon as possible. Don’t wait until you are an “expert” in theory; start writing software immediately. As a believer in iterative development, I hope this book enables even a novice programmer to begin writing basic C# code by the end of Chapter 2.

A number of topics are not covered in this book. You won’t find coverage of topics such as ASP.NET, ADO.NET, smart client development, distributed programming, and so on. Although these topics are relevant to the .NET Framework, to do them justice requires books of their own. Fortunately, Addison-Wesley’s .NET Development Series provides a wealth of writing on these topics. Essential C# 4.0 focuses on C# and the types within the Base Class Library. Reading this book will prepare you to focus on and develop expertise in any of the areas covered by the rest of the series.

## Target Audience for This Book

My challenge with this book was to keep advanced developers awake while not abandoning beginners by using words such as assembly, link, chain, thread, and fusion, as though the topic were more appropriate for blacksmiths than for programmers. This book’s primary audience is experienced developers looking to add another language to their quiver. However, I have carefully assembled this book to provide significant value to developers at all levels.

- Beginners: If you are new to programming, this book serves as a resource to help transition you from an entry-level programmer to a C# developer, comfortable with any C# programming task that’s thrown your way. This book not only teaches you syntax, but also trains you in good programming practices that will serve you throughout your programming career.

- Structured programmers: Just as it's best to learn a foreign language through immersion, learning a computer language is most effective when you begin using it before you know all the intricacies. In this vein, this book begins with a tutorial that will be comfortable for those familiar with structured programming, and by the end of Chapter 4, developers in this category should feel at home writing basic control flow programs. However, the key to excellence for C# developers is not memorizing syntax. To transition from simple programs to enterprise development, the C# developer must think natively in terms of objects and their relationships. To this end, Chapter 5's Beginner Topics introduce classes and object-oriented development. The role of historically structured programming languages such as C, COBOL, and FORTRAN is still significant but shrinking, so it behooves software engineers to become familiar with object-oriented development. C# is an ideal language for making this transition because it was designed with object-oriented development as one of its core tenets.

- Object-based and object-oriented developers: C++ and Java programmers, and many experienced Visual Basic programmers, fall into this category. Many of you are already completely comfortable with semicolons and curly braces. A brief glance at the code in Chapter 1 reveals that at its core, C# is similar to the C and C++ style languages that you already know.

- C# professionals: For those already versed in C#, this book provides a convenient reference for less frequently encountered syntax. Furthermore, it provides answers to language details and subtleties that are seldom addressed. Most importantly, it presents the guidelines and patterns for programming robust and maintainable code. This book also aids in the task of teaching C# to others. With the emergence of C# 3.0 and C# 4.0, some of the most prominent enhancements are:
  - Implicitly typed variables (see Chapter 2)
  - Extension methods (see Chapter 5)
  - Partial methods (see Chapter 5)
  - Anonymous types (see Chapter 11)
  - Generics (see Chapter 11)
  - Lambda statements and expressions (see Chapter 12)
  - Expression trees (see Chapter 12)
  - Standard query operators (see Chapter 14)
  - Query expressions (see Chapter 15)
  - Dynamic programming (Chapter 17)
  - Multithreaded programming with the Task Programming Library (Chapter 18)
  - Parallel query processing with PLINQ
  - Concurrent collections (Chapter 19)

These topics are covered in detail for those not already familiar with them. Also pertinent to advanced C# development is the subject of pointers, in Chapter 21. Even experienced C# developers often do not understand this topic well.

## Features of This Book

Essential C# 4.0 is a language book that adheres to the core C# Language 4.0 Specification. To help you understand the various C# constructs, the book provides numerous examples demonstrating each feature. Accompanying each concept are guidelines and best practices, ensuring that code compiles, avoids likely pitfalls, and achieves maximum maintainability.

To improve readability, code is specially formatted and chapters are outlined using mind maps.

## Code Samples

The code snippets in most of this text (see sample listing on the next page) can run on any implementation of the Common Language Infrastructure (CLI), including the Mono, Rotor, and Microsoft .NET platforms. Platform- or vendor-specific libraries are seldom used, except when communicating important concepts relevant only to those platforms (appropriately handling the single-threaded user interface of Windows, for example). Any code that specifically requires C# 3.0 or 4.0 compliance is called out in the C# 3.0 and C# 4.0 indexes at the end of the book.

Here is a sample code listing.

## LISTING 1.17: Commenting Your Code

```
class CommentSamples
{
    static void Main()
    {
        string firstName; // Variable for storing the first name
        string lastName; // Variable for storing the last name
        System.Console.WriteLine("Hey you!");
        // delimited comment inside statement
        System.Console.Write("/* No New Line */ (");
        "Enter your first name: ");
        firstName = System.Console.ReadLine();
        System.Console.Write /* No New Line */ (
        "Enter your last name: ");
        lastName = System.Console.ReadLine();
        /* Display a greeting to the console
        using composite formatting. */ { delimited comment
        System.Console.WriteLine("Your full name is {0} {1}.",
        firstName, lastName);
        // This is the end
        // of the program listing
    }
}
```

The formatting is as follows.

- Comments are shown in italics.

```
/* Display a greeting to the console
using composite formatting. */
```

- Keywords are shown in bold.

```
static void Main()
```

- Highlighted code calls out specific code snippets that may have changed from an earlier listing, or demonstrates the concept described in the text.

```
System.Console.Write /* No New Line */ (
```

Highlighting can appear on an entire line or on just a few characters within a line.

```
System.Console.WriteLine(
 "Your full name is {0} {1}." ,

```

- Incomplete listings contain an ellipsis to denote irrelevant code that has been omitted.
  // ...

- Console output is the output from a particular listing that appears following the listing.

## OUTPUT 1.4:

```
>HeyYou.exe
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
```

- User input for the program appears in italics.

Although it might have been convenient to provide full code samples that you could copy into your own programs, doing so would detract you from learning a particular topic. Therefore, you need to modify the code samples before you can incorporate them into your programs. The core omission is error checking, such as exception handling. Also, code samples do not explicitly include using System statements. You need to assume the statement throughout all samples.

You can find sample code and bonus material at intelliTecture.com/EssentialCSharp and at informit.com/msdnetserseries.

## Mind Maps

Each chapter's introduction includes a mind map, which serves as an outline that provides an at-a-glance reference to each chapter's content. Here is an example (taken from Chapter 5).
