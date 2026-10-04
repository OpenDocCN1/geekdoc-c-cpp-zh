
## Introduction to C++;
Programming Concepts and Applications

As computers become more and more part of our everyday lives, it is easy to imagine them as controlling our lives. Programming gives us a chance to truly be in charge of the computers. Programming lets us specify how a computer should operate at the lowest levels. And by using low-level commands we mastered, we can get the computer to do many interesting things.

You explore how the flow through a computer program is managed, looking at the key concepts of conditionals—where choices can be made (lecture 3)—and loops, where commands can be repeated (lecture 5). You also learn how to make use of the numerous functions that C++ provides in standard libraries (lecture 6).

full support OOP development. OOP typically involves 3 key ideas, of which is explored: encapsulation, where similar data and functions are grouped together (lecture 16); inheritance, where variables and functions are shared from one structure to another (lecture 19); and polymorphism, where different functions can be used interchangeably (lecture 20).

OOP also brings the use of constructors, and operators are defined similarly. Finally, it is not an OOP-specific topic, the need to allocate and indicate how memory comes up in the context of C++.

This course explores the process of programming—specifically using the C++. It is one of the most powerful programming languages available, giving programmers the power to control from the lowest levels—specifying individual elements of memory. C++ supports various paradigms, the traditional and procedural approach which have long been a part of many languages, the object-oriented approaches that began to dominate programming, and declarative approaches that let programmers specify behavior at an even greater general level.

Next, the course turns to that C++ provides for handling amounts of data. You are introduced to arrays, a method carried over from the C language that forms the basis for storing data in a large block of memory (lecture 7); and the that that array structure to provide additional safety and functionality (lecture 8). The vectors that are treated in C++ is very similar to the ways it handles strings, collections of characters used to handle text (lecture 9). For large amounts of data, interactive input and output are less feasible, so you will also learn how C++ can handle files (lecture 10).

The last major topic is generic programming, emphasizing the use of the Standard Template Library (STL) in C++. You discover key aspects of the STL and how it can simplify your programming (lecture 22 and 23).

This course walks through the start of programming, providing a tour of all the key aspects of programming in C++. No prior programming knowledge is assumed, and instructions are provided to help novice programmers get everything up to begin their programming journey.

With fundamental concepts programming, the course turns to the heart of procedural programming: the use of functions, allowing you to encapsulate, making it feasible to develop larger and more complex programs. You will learn to write your own functions (lecture 12) and the different ways you can handle parameters, including the introduction of the reference (lecture 13).

Throughout the course, we are interspersed with the larger issues of how to move from simple lines of code to developing larger programs (lectures 4, 11, 15, 21 and 24). The course covers topics including memory management, exception handling, top-down and bottom-up design, and object-oriented programming.

The lectures start with the basics of programming, describing how variables work, how basic input and output is, and how computations can be performed (lectures 1 and 2).

Following this, the course turns to object-oriented programming (OOP). It is the most commonly used paradigm today, and C++ provides

the power of OOP is to design a game engine that can play with different games (lecture 21). The course concludes with a final showing showing how C++ can be used to develop algorithms and in particular focuses on how an artificial intelligence can be the opponent in a game (lecture 24).

Course Scope

## 01 Compiling Your First C++ Program

C++ is one of the most powerful, efficient, and flexible programming languages that exists. It allows you to program in a way that closely corresponds to machine instructions while also providing several higher-level features to make it easier for people to understand. C++ supports multiple programming styles, or paradigms, that have emerged over time, and it is particularly strong in allowing you to use a variety of different paradigms in your programs. As a result, C++ is used as the basis for a wide variety of applications across many domains.

IN THIS LECTURE:

- Introduction to Computer Programming
- What Happens When You Program
- Program 1_1
- Program 1_9
- Program 1_10

- Quiz

- Quiz Solutions

## INTRODUCTION TO COMPUTER PROGRAMMING

Computers operate by following a set of instructions. But the instructions that a computer can understand are a bunch of 0s and 1s—a long sequence of binary numbers that encode the instructions and data for a computer to use. For people, this is nearly impossible to follow, and this is why programming languages have been developed.

> C++ has been used to develop many of the programs you've probably experienced—from Microsoft Windows to the code underlying Google's search and website to YouTube, Facebook, Amazon, and PayPal. It's been used to control devices ranging from ship engines to Mars Rovers and in phone systems worldwide.

What is sometimes considered the first program was written in the 1840s by Ada Lovelace, who wrote computational instructions that could run, in theory, on a machine that was designed but not built.

The first modern programming languages were developed in the 1950s, with Fortran being the first widely used. In fact, Fortran is a procedural language, and **procedural programming** is still common approach used today, including as style of C++ programming. Since Fortran, hundreds of languages have been developed, and each one has its own strengths and weaknesses.

In the 1980s, Bjarne Stroustrup wanted to retain the low-level efficiency advantages of C while adding some of the more modern programming approaches. Thus, C++ was born!

One big advantage of C++ was that it added the ability to do **object-oriented programming**, which lets you group your data and operations in more useful ways. But C++ is not only an object-oriented language. New features have been added, too, to reflect the most recent advances in programming language design.

at a much higher level, using cutting-edge programming constructs that let you write code once and apply that to a wide range of applications.

C++ was developed as a sort of extension of the programming language C, which was a descendant of an earlier language called B. All of these came from Bell Labs, later known as AT&T Labs. While B never got much use, C—which was developed in the early 1970s—became widely used and still today.

C++ is also a language that continues to be developed today. There's a large and active international C++ committee that is continually working to improve the language, including adding new features.

This makes C++ incredibly powerful, letting you work across a full range of paradigms. Like C, you can work

## WHAT HAPPENS WHEN YOU PROGRAM

Programmers generate a program written in a programming language, such as C++. The program is just a text file, and you're free to write it in many different ways. You could use your own word processor if you want and save it as a text file. You could use Notepad or WordPad on a PC or TextEdit on a Mac. There are also editors specifically designed to write code, such as Notepad++.

or executed, by a machine. This compiled version of the program is called an executable program, and you can run it on your computer whenever you want.

As you go through this course, you'll find it much more rewarding and experience if you're able to practice writing your code. See lecture 0b—C++ QUICK START.

that code, the compiler compiles it into machine language, and then run it—often with just one click of a button.

Once you write a program, the compiler takes the instructions in C++ and translates them into machine instructions—instructions that the computer can understand. So, a compiled program is a program that's ready to be,

As people develop code, they'll go through this many times to see if it's working. To make it easier to develop this code, programmers use an **integrated development environment (IDE)**, which will have an editor that lets you write, usually with some special features to help you write code in language. The IDE will have an easy way to automatically save

And there are other features built into the IDE, such as a **debugger**, which is a tool that helps you find and fix errors in your program. The IDE integrates all these things—and more—into one package so that you can edit and compile and debug your code all in one program.

Lecture 01 | Compiling Your First C++ Program

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_8_0.png)
