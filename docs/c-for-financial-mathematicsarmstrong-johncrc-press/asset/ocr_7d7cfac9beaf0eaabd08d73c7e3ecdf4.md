which is widely used on Unix computers is a *recursive acronym*. GNU stands for “GNU’s Not Unix”. It doesn’t even deserve a groan, does it?

# 3.3 Libraries

As we have seen, a C++ console application needs a **main** method. However, there are many other kinds of program such as Windows programs, web applications, and so forth. One particularly important kind of program is a *library*. A library is a collection of software routines that is designed to be used inside other computer programs.

In practice, you are more likely to write libraries than you are to write stand-alone applications. For example, your job may be to write routines to price individual types of financial derivatives. It will then be somebody else’s job to assemble your libraries with libraries written by other people in order to, say, write a trading application.

As a result we are not actually very interested in the **main** method of our program at all. We will keep a **main** method for the purpose of testing, but you should stop thinking in terms of writing a program. From now on, you should imagine that the software we are writing in this book is a library for pricing and not a stand-alone program. Our aim is to write useful functions rather than to write a single program.

# 3.4 Declaring and defining functions

In our example code, we defined the function `compoundInterest` before the **main** function. We did this because the **main** function uses the `compoundInterest` function.

In more sophisticated recursive code, you may want to write functions that both call each other. To support this, C++ allows you to *declare* a function and then *define* it later.

When you *declare* a function, you say what its name is and the types of arguments that it requires. When you *define* a function you say what the function actually does.

In all our function definitions so far, we have put the declaration and definition together. But if you want you can separate the declaration and definition.

Here is a stand-alone *declaration* for a compound interest function.