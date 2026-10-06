# Chapter 1

# Getting started

C is one of the most widely used programming languages
learn how to use it to program the Raspberry Pi!

# What's so great about C?

C is a very versatile and widely used programming language. It has been used to write pretty much everything, from low-level routines to control the hardware in embedded microcontrollers with graphical user interfaces. In spite of this huge flexibility, it is also relatively simple – the language only has about 20 or so keywords, but there are huge libraries of additional functions that you can call on when you need them. In the first part of this book, we are going to concentrate on learning about the keywords, with a few of the more commonly used library functions; the second part of the book shows how to use the GTK library to make it easy to write graphical interfaces in C.

Many of the languages you may have seen, such as Python, are all called interpreted languages. This means that the code you write is run directly; each line of code is read in and interpreted as you run it. C is different: it's a compiled language. This means that the code you write, known as the source code, is never run directly. The source code is passed through a program compiler, which converts it into a machine-readable version called an executable or a binary; then you run the executable.

This may seem complex, but it has a few advantages. First, it means that you don't need to have a copy of C itself on every computer you want to run your program on; once compiled, the executable is standalone and self-contained. Second, the compilation process will find a lot of errors before you even run the program (but you won't usually find all of them). importantly, the compilation process means that the time-consuming translation of readable code into machine-readable instructions has already happened, which means that compiled code generally runs many times faster than interpreted code would.

# CHOOSE YOUR EDITOR

You can use whatever editor you like to enter code, as long as it saves it as plain text. The Gesny editor included in Raspbian is a good choice, but you can also use Leafpad, nano, or any others that you prefer.