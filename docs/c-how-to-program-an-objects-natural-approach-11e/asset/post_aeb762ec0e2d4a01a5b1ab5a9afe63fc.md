
## 1.4 Machine Languages, Assembly Languages and High-Level Languages

Programmers write instructions in various programming languages, some directly understandable by computers and others requiring intermediate translation steps. Hundreds of such languages are in use today. These may be divided into three general types:

- Machine languages.
- Assembly languages.
- High-level languages.

### Machine Languages

Any computer can directly understand only its own machine language, defined by its hardware design. Machine languages generally consist of strings of numbers (ultimately reduced to 1s and 0s) that instruct computers to perform their most elementary operations one at a time. Machine languages are machine-dependent—a particular machine language can be used on only one type of computer. Such languages are cumbersome for humans. For example, here’s a section of an early machine-language payroll program that adds overtime pay to base pay and stores the result in gross pay:

```text
+1300042774
+1400593419
+1200274027
```

In our Building Your Own Computer case study (Exercises 7.9–7.11), you’ll “peel open” a “made-up” computer and look at its internal structure. We’ll introduce machine-language programming, and you’ll write several machine-language programs. To make this an especially valuable experience, you’ll then build a software simulation of a computer on which you can execute your machine-language programs. This will give you a friendly introduction to the contemporary computer architecture concept of “virtual machines.”

### Assembly Languages and Assemblers

Programming in machine language was too slow and tedious for most programmers. Instead of using the strings of numbers that computers could directly understand, programmers began using English-like abbreviations to represent elementary operations. These abbreviations formed the basis of assembly languages. Translator programs called assemblers were developed to convert assembly-language programs to machine language at computer speeds. The following section of an assembly-language payroll program also adds overtime pay to base pay and stores the result in gross pay:

```text
    load    basepay
    add     overpay
    store   grosspay
```

Although such code is clearer to humans, it’s incomprehensible to computers until it’s translated into machine language.

### High-Level Languages and Compilers

With the advent of assembly languages, computer usage increased rapidly. However, programmers still had to use numerous instructions to accomplish even simple tasks. To speed the programming process, high-level languages were developed in which single statements could accomplish substantial tasks. A typical high-level-language program contains many statements, known as the program’s source code.

Translator programs called compilers convert high-level-language source code into machine language. High-level languages allow you to write instructions that look almost like everyday English and contain common mathematical notations. A payroll program written in a high-level language might contain a statement such as

```text
grossPay = basePay + overTimePay
```

From the programmer’s standpoint, high-level languages are preferable to machine and assembly languages. C++ is among the world’s most widely used high-level programming languages.

In our Building Your Own Compiler case study (Exercises 13.29–13.34), you’ll build a compiler that takes programs written in a simple “made-up” high-level programming language and converts them to the Simpletron Machine Language that you learn in Exercise 7.9. Exercises 13.29–13.34 “tie” together the entire programming process. You’ll write programs in a simple high-level language, compile the programs on the compiler you build, then run the programs on the Simpletron simulator virtual machine you build in Exercise 7.10.

### Interpreters

Compiling large high-level language programs into machine language can take considerable computer time. Interpreters execute high-level language programs directly, avoiding compilation delays, but your code runs slower than compiled programs. Some programming languages, such as Java³⁴, Python³⁵ and C#³⁶, use a clever mixture of compilation and interpretation to run programs.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_72_0.png)

### Checkpoint

- 1. **(Fill-In)** ______ programs, developed to execute high-level-language programs directly, avoid compilation delays, although they run slower than compiled programs  
  **Answer:** Interpreter.
- 2. **(True/False)** High-level languages allow you to write instructions that look almost like everyday English and contain common mathematical notations.  
  **Answer:** True.

- 34. “Java virtual machine.” Wikipedia. Wikimedia Foundation. Accessed March 18, 2023. https://en.wikipedia.org/wiki/Java_virtual_machine#Bytecode_interpreter_and_just-in-time_compiler.
- 35. “The Bytecode Interpreter.” Accessed March 18, 2023. https://devguide.python.org/internals/interpreter/
- 36. “Common Language Runtime (CLR) overview.” Accessed March 18, 2023. https://learn.microsoft.com/en-us/dotnet/standard/clr.

## 1.5 Operating Systems

Operating systems are software that make using computers more convenient for users, software developers and system administrators. They provide services that allow applications to execute safely, efficiently and concurrently with one another. The software that contains the core operating-system components is called the kernel. Linux, Windows and macOS are popular desktop/laptop operating systems—you can use any of these with this book. The most popular mobile operating systems used in smartphones and tablets are Google’s Android and Apple’s iOS.

### Windows—A Proprietary Operating System

In the mid-1980s, Microsoft developed the Windows operating system, consisting of a graphical user interface built on top of DOS (Disk Operating System)—an enormously popular desktop/laptop operating system that users interacted with by typing commands. Windows 11 is Microsoft’s latest operating system. Windows is a proprietary operating system controlled exclusively by Microsoft. It is the world’s most widely used desktop and notebook operating system, with almost 72% market share (February 2023).

### Linux—An Open-Source Operating System

The Linux operating system is among the greatest successes of the open-source movement. Proprietary software for sale or lease dominated software’s early years. With open source, individuals and companies contribute to developing, maintaining and evolving the software. Anyone can then use that software for their own purposes—normally at no charge, but subject to various (typically generous) licensing requirements. Open-source code is often scrutinized by a much larger audience than proprietary software, so errors can get removed faster, making the software more robust. Open-source increases productivity and has contributed to an explosion of innovation. You’ll use various popular open-source libraries and tools throughout this book.

Some key organizations in the open-source community are:

- GitHub provides tools for managing open-source software-development projects. It has millions of them underway.
- The Apache Software Foundation created the Apache web server and now oversees 350+ open-source projects, including many big-data infrastructure technologies.
- The Eclipse Foundation oversees over 400 open-source projects, including the Eclipse Integrated Development Environment.
- The Mozilla Foundation is the creator of the Firefox web browser and several other projects, including Firefox Reality (a virtual reality web browser), Hubs (a virtual reality meeting space), Project Things (for building Internet of Things apps), WebXR Viewer (an augmented reality viewer) and Spoke (for building 3D social environments that can be visited using virtual reality devices).

- 37. Alison DeNisco Rayome and Shelby Brown. “Every Difference You Should Care About Between Windows 10 and Windows 11.” November 5, 2022. Accessed March 18, 2023. https://www.cnet.com/tech/computing/every-difference-you-should-care-about-between-windows-10-and-windows-11/.
- 38. “Desktop Operating System Market Share Worldwide.” Accessed March 18, 2023. https://gs.statcounter.com/os-market-share/desktop/worldwide.
- 39. “Welcome to the Apache Projects Directory.” Accessed March 18, 2023. https://projects.apache.org/.
- 40. “Eclipse Foundation.” Wikipedia. Wikimedia Foundation. Accessed March 18, 2023. https://en.wikipedia.org/wiki/Eclipse_Foundation.
- 41. “Welcome to the Mozilla Laboratory.” Accessed March 18, 2023. https://labs.mozilla.org/projects/.
