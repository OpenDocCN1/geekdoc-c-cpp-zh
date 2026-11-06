
Classes **encapsulate** (i.e., wrap) attributes and member functions into objects created from those classes—an object’s attributes and member functions are intimately related. Objects may communicate with one another, but they’re normally not allowed to know how other objects are implemented—implementation details are *hidden* within the objects themselves. This **information hiding**, as we’ll see, is crucial to good software engineering.

### Inheritance

A new class of objects can be created quickly and conveniently by **inheritance**—the new class absorbs the characteristics of an existing class, possibly customizing them and adding unique characteristics of its own. In our car analogy, an object of class “convertible” certainly is *an* object of the more *general* class “automobile,” but more *specifically*, the roof can be raised or lowered.

### Object-Oriented Analysis and Design (OOAD)

Soon you’ll be writing programs in C++. How will you create the **code** (i.e., the program instructions) for your programs? Perhaps, like many programmers, you’ll simply turn on your computer and start typing. This approach may work for small programs (like the ones we present in the early chapters of the book), but what if you were asked to create a software system to control thousands of automated teller machines for a major bank? Or suppose you were asked to work on a team of thousands of software developers building the next generation of the U.S. air traffic control system? For projects so large and complex, you should not simply sit down and start writing programs.

To create the best solutions, you should follow a detailed **analysis** process for determining your project’s **requirements** (i.e., defining *what* the system is supposed to do) and developing a **design** that satisfies them (i.e., deciding *how* the system should do it). Ideally, you’d go through this process and carefully review the design (and have your design reviewed by other software professionals) before writing any code. If this process involves analyzing and designing your system from an object-oriented point of view, it’s called an **object-oriented analysis and design (OOAD) process**. Languages like C++ are object oriented. Programming in such a language, called **object-oriented programming (OOP)**, allows you to implement an object-oriented design as a working system.

### The UML (Unified Modeling Language)

Although many different OOAD processes exist, a single graphical language for communicating the results of any OOAD process has come into wide use. This language, known as the Unified Modeling Language (UML), is now the most widely used graphical scheme for modeling object-oriented systems. We present our first UML diagrams in **Chapters 3** and **4**, then use them in our deeper treatment of object-oriented programming through **Chapter 12**. In our *optional* ATM Software Engineering Case Study in Chapters 25–26 we present a simple subset of the UML’s features as we guide you through an object-oriented design and implementation experience.

## 1.9 Typical C++ Development Environment

C++ systems generally consist of three parts: a program development environment, the language and the C++ Standard Library. C++ programs typically go through six phases: edit, preprocess, compile, link, load and execute. The following discussion explains a typical C++ program development environment.

### Phase 1: Editing a Program

Phase 1 consists of editing a file with an *editor program*, normally known simply as an *editor* (Fig. 1.6). You type a C++ program (typically referred to as *source code*) using the editor, make any necessary corrections and save the program on your computer’s disk. C++ source code filenames often end with the `.cpp`, `.cxx`, `.cc` or `.C` (uppercase) extensions which indicate that a file contains C++ source code. See the documentation for your C++ compiler for more information on filename extensions. Two editors widely used on Linux systems are `vi` and `emacs`. You can also use a simple text editor, such as Notepad in Windows, to write your C++ code.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_142_0.png)

Fig. 1.6 Typical C++ development environment—editing phase.

**Integrated development environments (IDEs)** are available from many major software suppliers. IDEs provide tools that support the software development process, including editors for writing and editing programs and debuggers for locating **logic errors**—errors that cause programs to execute incorrectly. Popular IDEs include Microsoft® Visual Studio 2015 Community Edition, NetBeans, Eclipse, Apple’s Xcode®, CodeLite and CLion.

### Phase 2: Preprocessing a C++ Program

In Phase 2, you give the command to **compile** the program (**Fig. 1.7**). In a C++ system, a **preprocessor** program executes automatically before the compiler’s translation phase begins (so we call preprocessing Phase 2 and compiling Phase 3). The C++ preprocessor obeys commands called **preprocessing directives**, which indicate that certain manipulations are to be performed on the program before compilation. These manipulations usually include (i.e., copy into the program file) other text files to be compiled, and perform various text replacements. The most common preprocessing directives are discussed in the early chapters; a detailed discussion of preprocessor features appears in **Appendix E**, Preprocessor.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_143_0.png)

**Fig. 1.7** Typical C++ development environment—preprocessor phase.

### Phase 3: Compiling a C++ Program

In Phase 3, the compiler translates the C++ program into machine-language code—also referred to as **object code** (**Fig. 1.8**).

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_144_0.png)

**Fig. 1.8** Typical C++ development environment—compilation phase.

### Phase 4: Linking

Phase 4 is called **linking**. C++ programs typically contain references to functions and data defined elsewhere, such as in the standard libraries or in the private libraries of groups of programmers working on a particular project (**Fig. 1.9**). The object code produced by the C++ compiler typically contains “holes” due to these missing parts. A **linker** links the object code with the code for the missing functions to produce an **executable program** (with no missing pieces). If the program compiles and links correctly, an executable image is produced.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_145_0.png)

**Fig. 1.9** Typical C++ development environment—linking phase.

### Phase 5: Loading

Phase 5 is called **loading**. Before a program can be executed, it must first be placed in memory (**Fig. 1.10**). This is done by the **loader**, which takes the executable image from disk and transfers it to memory. Additional components from shared libraries that support the program are also loaded.

### Phase 6: Execution

Finally, the computer, under the control of its CPU, **executes** the program one instruction at a time (**Fig. 1.11**). Some modern computer architectures often execute several instructions in parallel.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_146_0.png)

**Fig. 1.10** Typical C++ development environment—loading phase.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_146_1.png)

**Fig. 1.11** Typical C++ development environment—execution phase.

### Problems That May Occur at Execution Time

Programs might not work on the first try. Each of the preceding phases can fail because of various errors that we’ll discuss throughout this book. For example, an executing program might try to divide by zero (an illegal operation for integer arithmetic in C++). This would cause the C++ program to display an error message. If this occurred, you’d have to return to the edit phase, make the necessary corrections and proceed through the remaining phases again to determine that the corrections fixed the problem(s). [*Note:* Most programs in C++ input or output data.] Certain C++ functions take their input from `cin` (the **standard input stream**; pronounced “see-in”), which is normally the keyboard, but `cin` can be redirected to another device. Data is often output to `cout` (the **standard output stream**; pronounced “see-out”), which is normally the computer screen, but `cout` can be redirected to another device. When we say that a program prints a result, we normally mean that the result is displayed on a screen. Data may be output to other devices, such as disks, hardcopy printers or even transmitted over the Internet. There is also a **standard error stream** referred to as `cerr`. The `cerr` stream (normally connected to the screen) is used for displaying error messages.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_147_0.png)

### Common Programming Error 1.1

Errors such as division by zero occur as a program runs, so they’re called *runtime errors* or *execution-time errors*. **Fatal runtime errors** cause programs to terminate immediately without having successfully performed their jobs. **Nonfatal runtime errors** allow programs to run to completion, often producing incorrect results.
