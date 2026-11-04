
## Programming Basics I

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_26_0.png)

Taylor & Francis  
Taylor & Francis Group  
http://taylorandfrancis.com

## C# from the Beginning 1

> "Everything should be made as simple as possible, but not simpler."
> —Albert Einstein

This chapter covers the basic aspects of the C# language including its history, compilers, algorithms, variables, and the use of the Base Class Library. Each section is designed to facilitate a quick and easy introduction and to ensure a strong foundation in programming and problem solving. Special attention was placed on what a new programmer needs to know and/or might be confused about; the sections can, however, be covered quickly. There are a few sections set aside to cover history and theory, but the core of this chapter is about programming. Two sections promote good programming habits and there is a section on runtime, programming, and compiler errors (recommended reading even if you don't get into trouble). If you've skimmed the lessons, you know that this first chapter doesn't include any games, but don't let that fool you. All of the concepts covered here are just as important for games as they are for business and/or math related topics.

### An Overview of the C# Language

C# is a high- or mid-level programming language (and just in case you didn't know, a programming language is the collection of words, phrases, and syntax rules used to communicate with the computer). Although there are many high-level programming languages (BASIC, JAVA, FORTRAN, Pascal, Lisp, ADA, Modula-2 and Logo), few have reached the popularity of the original C and C++ languages. C and C++ have been used to create everything from operating systems and word processing packages to compilers for other high-level languages. C and C++ have been the programming languages of choice for more than 50 percent of all programming applications, and with their advances in object-oriented programming and Internet applications, both Managed C++ and C# are sure to fuel the popularity of C languages well into this new millennium.

### A Little History on the Cs

C was developed in the 1970s by Dennis Ritchie while he worked at AT&T Bell Laboratories. Before C, there was a language called B developed by Ken Thompson. While there was an A language, B was actually developed from Basic Combined Programming Language (BCPL), which was developed from a combination of two other languages, namely CPL and Algol 60. C++'s object-oriented portions are attributed to still another language known as Simula 67. CPL begot BCPL; BCPL begot B; B begot C; C begot C++; and C++ begot C#. In 1979, Bjarne Stroustrup (also at AT&T Bell Laboratories) developed the first version of C++ to be an enhanced version of the C language (initially referred to as C with classes). C++ was significantly enhanced with the addition of the Standard Template Library (STL) developed by Alexander Stepanov and Meng Lee at Hewlett-Packard. The STL was based heavily on previous work done by both Stepanov and Musser, from Rensselaer Polytechnic Institute.

Both C and C++ spread quickly in power and use, but eventually all the added features and expansions led to incompatibilities and frustrations. Two standards were created, first with the American National Standards Institute (ANSI) C standard of 1983, and then the American National Standards for Systems Information and International Standards Organization (ISO) C/C++ standards of 1998 (Note: C was also updated in this second standard). The 1998 ANSI/ISO standard is generally referred to as Native C++, while Microsoft's .Net Extensions are known as Managed C++. C# was also standardized with its first release under what is known as the 2001/2002 ECMA certified standard.

C# was developed by a team of Microsoft programmers led by chief architect Anders Hejlsberg. It is intended to supplement the development of applications required for both stream users and intranet/internet programmers alike. C# is definitely one of the most sophisticated languages ever developed, and similar to the entire .Net architecture, it will alter the way programmers think about programming for many years to come.

Hejlsberg was also responsible for the development of Microsoft's Visual J++, Turbo Pascal, and Delphi, for which he finally received the Dr. Dobb's Journal Award for Excellence in Programming early in 2001. For further information on the history of Turbo Pascal, Visual J++, and the Dr. Dobb's Journal Award, you should consult your local library… now let's get back to business.

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_29_0.png)

As you can see, C# evolved from the simpler languages.  
Hey, I thought it was created by a programmer.

### What is the .Net Framework?

The .Net framework is a multitasking, class-based programming library and interface that allows for both the interoperable exchange and execution of data. As a library, the .Net base classes are as powerful as the traditional Windows API function set, but have the added advantage of being completely object-oriented. Object-oriented programming (as explained throughout this book) is a practical method used to develop programs that promotes both the reusability and reliability of code. The .Net runtime (also known as the Common Language Runtime or CLR) serves as a shell or intermediate environment that assists the operating system with program execution(s).

The .Net framework also allows for program interoperability, requiring a Common Type System (CTS) governed through the Intermediate Language commonly known as Microsoft's Intermediate Language (MSIL) and/or the Common Intermediate Language (CIL). Intermediate Language should not be confused with Java's interpreted byte-type coding, which does not have the ability to be compiled. Microsoft has also developed a secondary type of compilation known as JIT (just-in-time) compilations. Under JIT, programs are not only installed into our systems, but the code is optimized for the processor. In addition, JIT compilation shortcuts the basic startup time by limiting compilation to only the required portions, which also improves overall performance.

The .Net architecture also offers some interesting advantages, including memory management (also known as garbage collection) and zero-impact installation. Garbage collection (stemming from Java) is a systematic approach to eliminating previously allocated memory that is no longer being referenced. While garbage collection diminishes the programmer's power to control memory deallocation, it does help to prevent dangerous memory leaks, and saves the programmer additional time that would normally be spent implementing destructors. Likewise, zero-impact installation has been developed to save the programmer and consumer many hours of frustration by eliminating the errors caused by faulty versioning. Under normal Windows operation, a typical `*.dll` type file would be included as part of a centralized reference, which in turn would make it subject to deletion whenever a new version is installed. If that new version is not entirely backward compatible, then the replacement file can cause the program to fail. With zero-impact installation, alternate versions of otherwise identical files can exist side by side, thereby eliminating this problem.

In addition, .Net offers increased code security, application domain restrictions, strong typing, and namespacing. The increase in security allows the consumer to control the level of access granted to any single program, with MSIL also determining the level of access requested by a program before its execution (This may help to prevent some unscrupulous programmers from damaging our files.). *Application domain restrictions* prevent memory conflicts between interrelated applications through the use of *virtual memory barriers*, which are barriers that restrict access, but do not impose processor delays. (This process is controlled through MSIL.) *Strong typing*, also governed by MSIL, requires that we specifically state data types, thus preventing ambiguous runtime errors; unfortunately, this also prevents us from using templates (excluded from the C# programming language). Finally, *namespacing*, originally designed to prevent Native C++ naming conflicts, is now a requirement of the .Net architecture, wherein all types must be defined with either an explicit or a global namespace.

### Managed Code and Assemblies

*Managed code* is the term used to define the coding implemented under the .Net framework, while the terms *native* and *unmanaged code* are used to indicate coding that bypasses this new architecture and is implemented directly through the Windows API. *Assemblies* are units in which managed coding is stored. Assemblies also contain information packets referred to as *metadata*: metadata packets keep track of an assembly's contents including its objects, methods, and types. Shared assemblies are stored in a central area referred to as the assembly's *cache*. Metadata packets are stored in an area inside these assemblies known as the *manifest*.
