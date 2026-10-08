optimise the performance of almost any other function, your effort will be wasted!

Before making any serious attempt to optimise your code, it is advisable that you profile it.

Unless your performance requirements are very precise, you may not need to buy a separate piece of software to profile your code. A simple approach is to execute the slow bit of code and then stop the processing randomly ten times and record what is happening. You will probably find that the code is doing much the same thing each time you stop it. You can safely deduce that this is where the performance problem is.

It is important to say that this book is about writing good quality C++ code, but it is not about writing C++ code for absolutely optimal performance. For most problems, it is far more important that your code executes correctly than that it executes as fast as humanly possible. Most of the time it is worth sacrificing some speed for other qualities of good code such as being easy to understand, read, and extend.

Donald Knuth, a winner of the prestigious Turing Prize and a celebrated programming expert, famously said, “Premature optimisation is the root of all evil”.

# **15.4.10    Example**

This book has a complex build. The text is written using LaTeX and it refers to various C++ files in numerous different projects. Each time a change is made to this book, all of the C++ code is compiled and tested both on Windows and on Unix. In addition there are tests to check that all the code shown in the LaTeX document matches the C++ code in the computer projects. Finally, the process of putting all the code examples and text onto a website is fully automated.

Without an automated build this book would be riddled with (even more) errors. All code contains bugs, and doubtless this book contains many errors. Nevertheless, the automated build ensures that the most egregious problems are quickly eliminated.

# **Exercises**

+   15.4.1.   Find and fix all the bugs in FMLib15.

+   15.4.2.   Try running FMLib without the debug information and with optimised machine code instead.
You can do this using Visual Studio by choosing the Release option from the menu bar. In addition, for experts, the project configuration options give you