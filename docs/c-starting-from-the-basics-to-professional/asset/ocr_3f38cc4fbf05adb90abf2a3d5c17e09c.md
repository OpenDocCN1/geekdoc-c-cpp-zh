In the first half of the book, your programs will consist of a single source file. In Chapter 11 we will show you how to compose a larger program, consisting of multiple module and source files.

**Note** The concrete steps you have to follow to get from your source code to a functioning executable differ from compiler to compiler. While most of our examples are small enough to compile and link through a series of command-line instructions, it is probably easier to use a so-called *integrated development environment* (IDE) instead. Modern IDEs offer a very user-friendly graphical user interface to edit, compile, link, run, and debug your programs. References to the most popular compilers and IDEs can easily be found online.

In practice, compilation is an iterative process because you’re almost certain to have made typographical and other errors in the code. Once you’ve eliminated these from each source file, you can progress to the link step, where you may find that yet more errors surface. Even when the link step produces an executable, your program may still contain logical errors; that is, it doesn’t produce the results you expect. To fix these, you must go back and modify the source code and try to compile it once more. You continue this process until your program works as you think it should. As soon as you declare to the world at large that your program works, someone will discover a number of obvious errors that you should have found. It hasn’t been proven beyond doubt so far as we know, but it’s widely believed that any program larger than a given size will always contain errors. It’s best not to dwell on this thought when flying…

# Procedural and Object-Oriented Programming

Historically, procedural programming is the way almost all programs were written. To create a procedural programming solution to a problem, you focus on the process that your program must implement to solve the problem. Here is a rough outline of what you do, once the requirements have been defined precisely:

+   - You create a clear, high-level definition of the overall process that your program will implement.
+   - You segment the overall process into workable units of computation that are, as much as possible, self-contained. These will usually correspond to functions.
+   - You code the functions in terms of processing basic types of data: numerical data, single characters, and character strings.

Apart from the common requirement of starting out with a clear specification of what the problem is, the object-oriented approach to solving the same problem is quite different:

+   - From the problem specification, you determine what types of *objects* the problem is concerned with. For example, if your program deals with baseball players, you’re likely to identify BaseballPlayer as one of the types of data your program will work with. If your program is an accounting package, you may well want to define objects of type Account and type Transaction. You also identify the set of *operations* that the program will need to carry out on each type of object. This will result in a set of application-specific data types that you will use in writing your program.

¹ The total flight software of a Boeing 787 reportedly consists of about 14 million lines of code (about half of which is part of the avionics and online support systems). Knowing that some studies claim you can expect a few or even dozens of defects per thousand lines of code… Precisely: best not to dwell…