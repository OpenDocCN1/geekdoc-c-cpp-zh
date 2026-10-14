(such as device drivers and other hardware interaction) and faster processing, e.g. video games.

Because the language is pre-converted to machine code, it can be processed by the computer much quicker because the compiler has already checked the code for errors and other issues that can cause the program to fail. The compiler won’t catch all errors but it does help. The caveat to using a compiler is that compiling can be a time consuming task; the actual compiling time can take several minutes to hours to complete depending on the program. If errors are found, the developer has to find and fix them then rerun the compiler; this cycle continues until the program works correctly.

Python is considered an interpreted language. It doesn’t have a compiler; the interpreter processes the code line by line and creates a *bytecode*. Bytecode is an in-between “language” that isn’t quite machine code but it isn’t the source code. Because of this in-between state, bytecode is more transferable between operating systems than machine code; this helps Python be cross-platform. Java is another language that uses bytecodes.

However, because Python uses an interpreter rather than compiler, the code processing can be slower. The bytecode still has to be “deciphered” for use by the processor, which takes additional time. But the benefit to this is that the programmer can immediately see the results of his code. He doesn’t have to wait for the compiler to decide if there is a syntax error somewhere that causes the program to crash.

# ## 2.1.3 Prototyping

Because of interpretation, Python and similar languages are used for rapid application development and program prototyping. For example, a simple program can be created in just a few hours and shown to a customer in the same visit.

Programmers can repeatedly modify the program and see the results quickly. This allows them to try different ideas and see which one is best without investing a lot of time on dead-ends. This also applies to creating graphical user interfaces (GUIs). Simple “sketches” can be laid out in minutes because Python not only has several different GUI libraries available but also includes a simple library (*Tkinter*) by default.