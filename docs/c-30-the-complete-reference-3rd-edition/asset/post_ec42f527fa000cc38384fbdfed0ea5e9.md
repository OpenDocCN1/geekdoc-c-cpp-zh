
## The C# Language

Part I discusses the elements of the C# language, including its keywords, syntax, and operators. Also described are several foundational C# techniques, such as using I/O and reflection, which are tightly linked with the C# language.

## PART

- CHAPTER 1
- The Creation of C#
- CHAPTER 2
- An Overview of C#
- CHAPTER 3
- Data Types, Literals, and Variables
- CHAPTER 4
- Operators
- CHAPTER 5
- Program Control Statements
- CHAPTER 6
- Introducing Classes and Objects
- CHAPTER 7
- Arrays and Strings
- CHAPTER 8
- A Closer Look at Methods and Classes
- CHAPTER 9
- Operator Overloading
- CHAPTER 10
- Indexers and Properties
- CHAPTER 11
- Inheritance
- CHAPTER 12
- Interfaces, Structures, and Enumerations
- CHAPTER 13
- Exception Handling
- CHAPTER 14
- Using I/O
- CHAPTER 15
- Delegates, Events, and Lambda Expressions
- CHAPTER 16
- Namespaces, the Preprocessor, and Assemblies
- CHAPTER 17
- Runtime Type ID, Reflection, and Attributes
- CHAPTER 18
- Generics
- CHAPTER 19
- LINQ
- CHAPTER 20
- Unsafe Code, Pointers, Nullable Types, and Miscellaneous Topics

## The Creation of C#

C# is Microsoft’s premier language for .NET development. It leverages time-tested features with cutting-edge innovations and provides a highly usable, efficient way to write programs for the modern enterprise computing environment. It is, by any measure, one of the most important languages of the 21st century.

The purpose of this chapter is to place C# into its historical context, including the forces that drove its creation, its design philosophy, and how it was influenced by other computer languages. This chapter also explains how C# relates to the .NET Framework. As you will see, C# and the .NET Framework work together to create a highly refined programming environment.

## C#'s Family Tree

Computer languages do not exist in a void. Rather, they relate to one another, with each new language influenced in one form or another by the ones that came before. In a process akin to cross-pollination, features from one language are adapted by another, a new innovation is integrated into an existing context, or an older construct is removed. In this way, languages evolve and the art of programming advances. C# is no exception.

C# inherits a rich programming legacy. It is directly descended from two of the world’s most successful computer languages: C and C++. It is closely related to another: Java. Understanding the nature of these relationships is crucial to understanding C#. Thus, we begin our examination of C# by placing it in the historical context of these three languages.

## C: The Beginning of the Modern Age of Programming

The creation of C marks the beginning of the modern age of programming. C was invented by Dennis Ritchie in the 1970s on a DEC PDP-11 that used the UNIX operating system. While some earlier languages, most notably Pascal, had achieved significant success, C established the paradigm that still charts the course of programming today.

C grew out of the structured programming revolution of the 1960s. Prior to the 1960s, large programs were difficult to write because the program logic tended to degenerate into what is known as “spaghetti code,” a tangled mass of jumps, calls, and returns that is difficult to follow. Structured languages addressed this problem by adding well-defined control statements, subroutines with local variables, and other improvements.

Through the use of structured techniques programs became better organized, more reliable, and easier to manage.

Although there were other structured languages at the time, C was the first to successfully combine power, elegance, and expressiveness. Its terse, yet easy-to-use syntax coupled with its philosophy that the programmer (not the language) was in charge quickly won many converts. It can be a bit hard to understand from today's perspective, but C was a breath of fresh air that programmers had long awaited. As a result, C became the most widely used structured programming language of the 1980s.

However, even the venerable C language had its limits. One of the most troublesome was its inability to handle large programs. The C language hits a barrier once a project reaches a certain size, and after that point, C programs are difficult to understand and maintain. Precisely where this limit is reached depends upon the program, the programmer, and the tools at hand, but there is always a threshold beyond which a C program becomes unmanageable.

## The Creation of OOP and C++

By the late 1970s, the size of many projects was near or at the limits of what structured programming methodologies and the C language could handle. To solve this problem, a new way to program began to emerge. This method is called object-oriented programming (OOP). Using OOP, a programmer could handle much larger programs. The trouble was that C, the most popular language at the time, did not support object-oriented programming. The desire for an object-oriented version of C ultimately led to the creation of C++.

C++ was invented by Bjarne Stroustrup beginning in 1979 at Bell Laboratories in Murray Hill, New Jersey. He initially called the new language “C with Classes.” However, in 1983 the name was changed to C++. C++ contains the entire C language. Thus, C is the foundation upon which C++ is built. Most of the additions that Stroustrup made to C were designed to support object-oriented programming. In essence, C++ is the object-oriented version of C. By building upon the foundation of C, Stroustrup provided a smooth migration path to OOP. Instead of having to learn an entirely new language, a C programmer needed to learn only a few new features before reaping the benefits of the object-oriented methodology.

C++ simmered in the background during much of the 1980s, undergoing extensive development. By the beginning of the 1990s, C++ was ready for mainstream use, and its popularity exploded. By the end of the decade, it had become the most widely used programming language. Today, C++ is still the preeminent language for the development of high-performance system code.

It is critical to understand that the invention of C++ was not an attempt to create an entirely new programming language. Instead, it was an enhancement to an already highly successful language. This approach to language development—beginning with an existing language and moving it forward—established a trend that continues today.

## The Internet and Java Emerge

The next major advance in programming languages is Java. Work on Java, which was originally called Oak, began in 1991 at Sun Microsystems. The main driving force behind Java’s design was James Gosling. Patrick Naughton, Chris Warth, Ed Frank, and Mike Sheridan also played a role.

Java is a structured, object-oriented language with a syntax and philosophy derived from C++. The innovative aspects of Java were driven not so much by advances in the art of programming (although some certainly were), but rather by changes in the computing environment. Prior to the mainstreaming of the Internet, most programs were written, compiled, and targeted for a specific CPU and a specific operating system. While it has always been true that programmers like to reuse their code, the ability to port a program easily from one environment to another took a backseat to more pressing problems. However, with the rise of the Internet, in which many different types of CPUs and operating systems are connected, the old problem of portability reemerged with a vengeance. To solve the problem of portability, a new language was needed, and this new language was Java.

Although the single most important aspect of Java (and the reason for its rapid acceptance) is its ability to create cross-platform, portable code, it is interesting to note that the original impetus for Java was not the Internet, but rather the need for a platform-independent language that could be used to create software for embedded controllers. In 1993, it became clear that the issues of cross-platform portability found when creating code for embedded controllers are also encountered when attempting to create code for the Internet. Remember: The Internet is a vast, distributed computing universe in which many different types of computers live. The same techniques that solved the portability problem on a small scale could be applied to the Internet on a large scale.

Java achieved portability by translating a program’s source code into an intermediate language called *bytecode*. This bytecode was then executed by the Java Virtual Machine (JVM). Therefore, a Java program could run in any environment for which a JVM was available. Also, since the JVM is relatively easy to implement, it was readily available for a large number of environments.

Java’s use of bytecode differed radically from both C and C++, which were nearly always compiled to executable machine code. Machine code is tied to a specific CPU and operating system. Thus, if you wanted to run a C/C++ program on a different system, it needed to be recompiled to machine code specifically for that environment. Therefore, to create a C/C++ program that would run in a variety of environments, several different executable versions of the program would be needed. Not only was this impractical, it was expensive. Java’s use of an intermediate language was an elegant, cost-effective solution. It is also a solution that C# would adopt for its own purposes.

As mentioned, Java is descended from C and C++. Its syntax is based on C, and its object model is evolved from C++. Although Java code is neither upwardly nor downwardly compatible with C or C++, its syntax is sufficiently similar that the large pool of existing C/C++ programmers could move to Java with very little effort. Furthermore, because Java built upon and improved an existing paradigm, Gosling, et al., were free to focus their attention on the new and innovative features. Just as Stroustrup did not need to “reinvent the wheel” when creating C++, Gosling did not need to create an entirely new language when developing Java. Moreover, with the creation of Java, C and C++ became an accepted substrata upon which to base a new computer language.

### The Creation of C#

While Java has successfully addressed many of the issues surrounding portability in the Internet environment, there are still features that it lacks. One is *cross-language interoperability*, also called *mixed-language programming*. This is the ability for the code produced by one language to work easily with the code produced by another. Cross-language interoperability is needed for the creation of large, distributed software systems. It is also desirable for programming software components because the most valuable component is one that can be used by the widest variety of computer languages, in the greatest number of operating environments.
