
| Programming language | Description |
|---|---|
| JavaScript | JavaScript is the most widely used scripting language. It’s primarily used to add programmability to web pages—for example, animations and interactivity with the user. It’s provided with all major web browsers. |
| Ruby on Rails | Ruby—created in the mid-1990s by Yukihiro Matsumoto—is an open-source, object-oriented programming language with a simple syntax that’s similar to Perl and Python. Ruby on Rails combines the scripting language Ruby with the Rails web application framework developed by 37Signals. Their book, *Getting Real* (getting-real.37signals.com/toc.php), is a must read for web developers. Many Ruby on Rails developers have reported productivity gains over other languages when developing database-intensive web applications. Ruby on Rails was used to build Twitter’s user interface. |
| Scala | Scala (www.scala-lang.org/node/273)—short for “scalable language”—was designed by Martin Odersky, a professor at École Polytechnique Fédérale de Lausanne (EPFL) in Switzerland. Released in 2003, Scala uses both the object-oriented programming and functional programming paradigms and is designed to integrate with Java. Programming in Scala can reduce the amount of code in your applications significantly. Twitter and Foursquare use Scala. |

**Fig. 1.5** | Other programming languages. (Part 3 of 3.)

## 1.9 C++ and a Typical C++ Development Environment

C++ evolved from C, which was developed by Dennis Ritchie at Bell Laboratories. C is available for most computers and is hardware independent. With careful design, it’s possible to write C programs that are portable to most computers.

The widespread use of C with various kinds of computers (sometimes called **hardware platforms**) unfortunately led to many variations. A standard version of C was needed. The American National Standards Institute (ANSI) coordinated with the International Organization for Standardization (ISO) to standardize C worldwide; the joint standard document was published in 1990 and is referred to as *ANSI/ISO 9899: 1990*.

C99 is the latest ANSI standard for the C programming language. It was developed to evolve the C language to keep pace with increasingly powerful hardware and ever more demanding user requirements. C99 also makes C more consistent with C++. For more information on C and C99, see our book *C How to Program, 6/e* and our C Resource Center (located at www.deitel.com/C).

C++, an extension of C, was developed by Bjarne Stroustrup in the early 1980s at Bell Laboratories. C++ provides a number of features that “spruce up” the C language, but more importantly, it provides capabilities for object-oriented programming.

You’ll begin developing customized, reusable classes and objects in Chapter 3, Introduction to Classes, Objects and Strings. The book is object oriented, where appropriate, from the start and throughout the text.

We also provide an optional automated teller machine (ATM) case study in Chapters 25–26, which contains a complete C++ implementation. The case study presents a carefully paced introduction to object-oriented design using the UML—an industry standard graphical modeling language for developing object-oriented systems. We guide you through a friendly design experience intended for the novice.

### C++ Standard Library

C++ programs consist of pieces called **classes** and **functions**. You can program each piece yourself, but most C++ programmers take advantage of the rich collections of classes and functions in the **C++ Standard Library**. Thus, there are really two parts to learning the C++ “world.” The first is learning the C++ language itself; the second is learning how to use the classes and functions in the C++ Standard Library. We discuss many of these classes and functions. P. J. Plauger’s book, *The Standard C Library* (Upper Saddle River, NJ: Prentice Hall PTR, 1992), is a must read for programmers who need a deep understanding of the ANSI C library functions included in C++. Many special-purpose class libraries are supplied by independent software vendors.

> **Software Engineering Observation 1.2**
> 
> Use a “building-block” approach to create programs. Avoid reinventing the wheel. Use existing pieces wherever possible. Called software reuse, this practice is central to object-oriented programming.

![](img/bfd978e7e9b192bab46ec2a89e481263_51_0.png)

> **Software Engineering Observation 1.3**
> 
> When programming in C++, you typically will use the following building blocks: classes and functions from the C++ Standard Library, classes and functions you and your colleagues create and classes and functions from various popular third-party libraries.

![](img/bfd978e7e9b192bab46ec2a89e481263_51_1.png)

The advantage of creating your own functions and classes is that you’ll know exactly how they work. You’ll be able to examine the C++ code. The disadvantage is the time-consuming and complex effort that goes into designing, developing and maintaining new functions and classes that are correct and that operate efficiently.

> **Performance Tip 1.1**
> 
> Using C++ Standard Library functions and classes instead of writing your own versions can improve program performance, because they’re written carefully to perform efficiently. This technique also shortens program development time.

![](img/bfd978e7e9b192bab46ec2a89e481263_51_2.png)

> **Portability Tip 1.1**
> 
> Using C++ Standard Library functions and classes instead of writing your own improves program portability, because they’re included in every C++ implementation.

![](img/bfd978e7e9b192bab46ec2a89e481263_51_3.png)

We now explain the commonly used steps in creating and executing a C++ application using a C++ development environment (illustrated in Figs. 1.6–1.11). C++ systems generally consist of three parts: a program development environment, the language and the C++ Standard Library. C++ programs typically go through six phases: edit, preprocess,

### Phase 3: Compiling a C++ Program

In Phase 3, the compiler translates the C++ program into machine-language code—also referred to as object code (Fig. 1.8).

![](img/bfd978e7e9b192bab46ec2a89e481263_53_0.png)

**Fig. 1.8** | *Typical C++ development environment—compilation phase.*

### Phase 4: Linking

Phase 4 is called linking. C++ programs typically contain references to functions and data defined elsewhere, such as in the standard libraries or in the private libraries of groups of programmers working on a particular project (Fig. 1.9). The object code produced by the C++ compiler typically contains “holes” due to these missing parts. A linker links the object code with the code for the missing functions to produce an executable program (with no missing pieces). If the program compiles and links correctly, an executable image is produced.

![](img/bfd978e7e9b192bab46ec2a89e481263_53_1.png)

**Fig. 1.9** | *Typical C++ development environment—linking phase.*

### Phase 5: Loading

Phase 5 is called loading. Before a program can be executed, it must first be placed in memory (Fig. 1.10). This is done by the loader, which takes the executable image from disk and transfers it to memory. Additional components from shared libraries that support the program are also loaded.

![](img/bfd978e7e9b192bab46ec2a89e481263_53_2.png)

**Fig. 1.10** | *Typical C++ development environment—loading phase.*

### Phase 6: Execution

Finally, the computer, under the control of its CPU, executes the program one instruction at a time (Fig. 1.11). Some modern computer architectures can execute several instructions in parallel.

![](img/bfd978e7e9b192bab46ec2a89e481263_54_0.png)

**Fig. 1.11** | Typical C++ development environment—execution phase.

### Problems That May Occur at Execution Time

Programs might not work on the first try. Each of the preceding phases can fail because of various errors that we’ll discuss throughout this book. For example, an executing program might try to divide by zero (an illegal operation for whole-number arithmetic in C++). This would cause the C++ program to display an error message. If this occurred, you’d have to return to the edit phase, make the necessary corrections and proceed through the remaining phases again to determine that the corrections fixed the problem(s).

**[Note:** Most programs in C++ input or output data. Certain C++ functions take their input from the *standard input stream* (pronounced “see-in”), which is normally the keyboard, but `cin` can be redirected to another device. Data is often output to `cout` (the *standard output stream*, pronounced “see-out”), which is normally the computer screen, but `cout` can be redirected to another device. When we say that a program prints a result, we normally mean that the result is displayed on a screen. Data may be output to other devices, such as disks and hardcopy printers. There is also a *standard error stream* referred to as `cerr`. The `cerr` stream (normally connected to the screen) is used for displaying error messages.**]

> **Common Programming Error 1.1**
> 
> Errors such as division by zero occur as a program runs, so they’re called *runtime errors* or *execution-time errors*. *Fatal runtime errors* cause programs to terminate immediately without having successfully performed their jobs. *Nonfatal runtime errors* allow programs to run to completion, often producing incorrect results.

## 1.10 Test-Driving a C++ Application

In this section, you’ll run and interact with your first C++ application. You’ll begin by running an entertaining guess-the-number game, which picks a number from 1 to 1000 and
