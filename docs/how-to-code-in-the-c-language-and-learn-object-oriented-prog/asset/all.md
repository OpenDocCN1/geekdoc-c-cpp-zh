![](Images/cover00229.jpeg)

C++ Programming Made Simple for Beginner’s

A Powerful and Proven Programming Beginners Guide to Get Immediate Results

C++ Programming Made Simple for Beginner’s

Written by Alexander Harrison

and

Artwork by Joanne Snowden

Disclaimer

All rights reserved. No section of this publication is allowed to be reproduced or transmitted in any form, whether mechanical or electronically, without written authorization from the author.

This book details the author’s personal experiences with C++ programming language. Furthermore, the author is not licensed as an educational or programming professional.

The author and publisher are providing this book and its contents on a tutorial basis. In addition, the author and publisher do not represent or warrant the information accessible via this book is completely accurate, complete or up to date.

Except as specifically stated in this book, neither the author or publisher, nor any authors, contributors, or other representatives will be liable for damages arising out of or in connection with the use of this book. This is a comprehensive limitation of liability that applies to all damages of any kind, including (without limitation) compensatory; direct, indirect or consequential damages; loss of data, income or profit; loss of or damage to property and claims of third parties.

This book provides content related to educational, computing and programming topics. As such, use of this book implies your acceptance of this disclaimer.

# Introduction

“By Failing To Prepare, You Are Preparing To Fail.”

(Benjamin Franklin)

“Success is not final, failure is not fatal: it is the courage to continue that counts.”

(Winston Churchill)

## Ready for C++ Programming?

Congratulations for taken aboard the decision to learn the C++ programming language. You are someone special for having the desire to learn the mechanics and syntaxes of an extremely powerful computer programming language.

I am going to assume you identify the basic use for a computer programming language. Since this book focuses on the C++ language, I am also going to assume you have a general, but perhaps imprecise, notion of the power the programming language can produce.

No matter what circumstances you have for purchasing or borrowing this book from the Kindle store, I guarantee it’ll help you on the road to learning C++.

## What You’ll Learn in this Book

Inside C++ Programming Made Simple for Beginner’s, there is a wealth of programming knowledge to learn. Whether you have simply started to learn C++ or are a little knowledgeable about the language, you’ll discover something new. Written to help wannabe-programmers, the book examines the basics and teaches core fundamentals required to build programs. The topics contained in the book includes:

*   Constants.
*   Functions.
*   Object-Oriented Programming (OOP).
*   Program Design.
*   Statements.
*   Variables.
*   And Much More…

The book opens with the basics of C++, via the old C language. C++ Programming Made Simple for Beginner’s does not require any prior knowledge of C, C++ or any computer language. However, any knowledge you might have will certainly help to understand C++ effectively. Don’t get totally confused though. This book does not ask much, but it does hope you are not entirely technologically impotent and you understand the basics of operating a computer, from opening files to accessing the internet.

## How this Book is Laid Out

I am not going to pretend and declare C++ is an easy language to learn, as it blatantly isn’t. To help absorb and become adept at writing code, each chapter has numerous programming examples to replicate. Each example is built as a Win32 console application, meaning it has a text-based interface, which operates without the power of Windows API. For a C++ beginner, using a Win32 console is good to start building on.

By understanding the information and code examples from each chapter, the next one will seem easier to grasp. For example, in, Chapter 03: Data Storage, Variables and Constants you attain the knowledge to use program variables and understand how to store them in computer memory. Then at Chapter 04: Basic Operators, by using the knowledge read about in the previous chapter, you’ll find it easier to understand the data types capable of serving different varieties of mathematical operators.

If you are a beginner, then this book will certainly have an abundance of information for you. On the other hand, if you have purchased this book to use as a reference guide, then it will help you rediscover programming topics you have mislaid in your memory, such as variables, operators and functions.

## Conventions and Practices

Amongst the pages of this book, you’ll discover three bold titles focusing on programming techniques. The following illustrates the titles spread out amongst the numerous pages.

| Programming KnowledgeThese boxes are filled with necessary information, which can help to enhance your knowledge of the C++ language. |

| Programming Technical TalkThese boxes are for the “geek” inside us, which desires to learn and absorb the information of in-depth C++ programming concepts. |

| Programming WarningsThese boxes point out dangerous areas that a programmer should be aware of before attempting to code something, via a certain programming concept. |

Chapter 01

# C++ Program Design

## Program and Design Software

The initial attribute in regards to building computer programs is the ability to understand software design. There is no point in learning C++ and not having an awareness of how to design programs. Hence, software design forms the basis of developing programs.

## Two Hour Pen and Paper Brainstorm Method

The best practise to finish a design – whether it be software design or some other form – is to throw questions left, right and centre at it. This is the stage I call "The Two Hour Pen & Paper Brainstorm Method", because when you begin to throw program design concepts at a blank canvas, you require a productive attitude.

The designs you scribble down are the beginning of a blueprint. Nonetheless, don’t think when drafting a blueprint every line of program code is required. If anyone was to sit down and draw out a blueprint for a piece of software by writing every line of code, it would take forever and they would be forced into a complete muddle. In short, they would end up throwing the idea in the bin, or begging for the men in white coats to escort them away.

| Warning: Avoid the ComputerIt sounds ludicrous to consider not using a computer when starting to program, but when drafting your design blueprint try and avoid the computer, until you have the initial idea down on paper. There are two reasons behind this madness. 
1.  Modern computers have the internet, which is a possible distraction.
2.  Typing on a computer is less natural then scribbling notes down on paper.

 |

Warning: Avoid the Computer

It sounds ludicrous to consider not using a computer when starting to program, but when drafting your design blueprint try and avoid the computer, until you have the initial idea down on paper. There are two reasons behind this madness.

Modern computers have the internet, which is a possible distraction.

Typing on a computer is less natural then scribbling notes down on paper.

## Why Should I Design Programs Before Writing Code?

The primary stages of learning C++ might raise several questions such as, "Why is it better to construct design blueprints for your programs before writing a line of code?" Well, that is a good question, one that bewilders the handful of budding programmers. No matter the computer language, beginners who opt to learn programming choose to study the language nuts-and-bolts (programming syntax), instead of being swayed to learn the principles of both program design and programming.

If you take time to learn both together, it’ll excel your chances of remembering the language. Furthermore, the learning process will appear quicker, because you absorb information more thoroughly using this technique.

## Question the Programs Purpose

Programs are developed for the core reason of solving problems. Hence, one program is built to solve one problem. Therefore, for you to befit a software developer and designer, one question that is necessary to consider is the purpose of why a certain program is demanded

| Knowledge: Four Questions of Software DevelopmentWhen inspiration knocks at the door and offers an idea for a new program, you should ask these four questions of software development. 
1.  What is the purpose of the program?
2.  What problem does the program solve?
3.  Does today’s market already have a program that solves the problem?
4.  Can the program be created in time?

 |

Software development companies use hours of time brainstorming, considering and discussing hundreds of reasons why a certain piece of software should be developed. Millions of dollars are injected into a software project by companies every year. Therefore, it is fatal if one or more of the above factors are overlooked and the project stalls. Basically, someone’s head will be assigned to the chopping-board.

## Steps to a Program Design Blueprint

In the process of writing out a program design blueprint there are a collection of bullet points that you are required to consider, especially if you wish to build a program without too much hassle. To have this put in an old-fashion way, you need some up-front planning involved before one line of code is written. To help you, I have nailed down these steps in an easy-to-remember process.

### Step 1: Define the Problem You Wish to Solve

As a programmer and program designer, you are required to examine the problem you wish to solve, and define it in a sentence or two. Here is a list of problem examples to give you some idea.

| Knowledge: Problem Ideas 
*   I need to design an application that will store all my program ideas in one place, like a cloud system but on my computer.
*   I need to design a program that displays my family and friends photographs on screen and allows me to upload them to chosen social media sites.
*   I need to design a small mathematical game, which will help my children with their homework.

 |

Do you get the idea? It is an obvious step, but one many beginning designers skip for one reason or another. It is a plan and you should never forget to plan.

### Step 2: Define what is involved in solving the Problem

This step focuses on the initial problem you have defined and asks the question "How can this problem be solved?"

There are ways of examining the problem in hand. Three of the biggest questions that are normally asked are:

| Knowledge: Define Ideas 
*   How do I want my program to function?
*   How do I want the user to interact with the program?
*   What tools do I require to complete the program?

 |

These questions might appear easy to answer at first glance, but it is no good at failing to take some time and really concentrate on the methods required to answer each one properly. Consequently, in a less broad term, do not try and "wing it".

### Step 3: Define a List of Events Involved in the Problem

You should have a good notion of how you are going to tackle the problem and design the program. The next step is to define the type of events to help your program operate.

For example, if you were to develop an application to store all your program ideas in one place, then it might be designed with a function to Save, Load, Open and Edit a file that contains data placed in the program. Therefore, you could have the following events to help your program operate effectively:

| Knowledge: Event Ideas 
*   Load File Event
*   Save File Event
*   Open File Event
*   Edit File Event.

 |

In C++, these events are written out as functions filled with the correct code to achieve a specific task. Taking the Load File Event, if the function was opened up, it would be filled with code to help the user load a file needed.

## Reuse Program Code

Most programmers share is the displeasure for rewriting code they already have written in a previous project. Most programmers bask in reusing old program code and implementing it in their current projects.

For example, as a programmer, you might write code to add two numbers and display the result on screen. Then in another program, you may desire to reuse the code. Therefore, instead of rewriting it again, it is far easier to copy the code from the program you previously wrote and paste it into your new one.

| Technical Talk: Software ReuseThe term "software reuse" is the theory of replicating, or copying, a section of code from an existing piece of software and placing it into a new project. |

## Select a Compiler

Throughout the book, you’ll require the use of a compiler to help build the program examples dotted in amongst the pages, and any others you single-handedly wish to code. Without a compiler, you have no method to assemble code and develop programs. The reason for this is because C++ is a statically typed, multi-paradigm and compiled programming language.

| Technical Talk: What Is Multi-Paradigm?A programming paradigm is the method or style that a computer language can understand. It employs this method in order to structure and employ elements in compiled programs. Therefore, a multi-paradigm language, like C++, inhabits the ability for the programmer to use different forms and styles to build programs. A good example of this is the implementation of Object-Oriented Programming in C++. |

A compiler examines written code and links the various libraries included in a program to eventually create an executable file (.exe). During this process, it checks for any errors in the code. If some are found, it reports them to the compiler for you to see. If there are no errors then the compiler shall build the program and run it.

Modern day compilers supply their own Integrated Development Environment (IDE), which is the user-interface platform for programming applications. Basically, a compilers IDE is everything you see on the screen.

## No Compiler? Don’t Worry!

If you have no compiler installed on your machine or don’t possess one, then there are a couple of options available you can download from the internet. Yes, they are also free. My favourite two are listed here:

### Code::Blocks 13.12

Code::Blocks is a programming application that has its own compiler built-in. Developed by the Code::Blocks team, the program is an open-source (free) Integrated Development Environment that is suited for C and C++ programmers.

| Download Link[http://www.codeblocks.org/downloads/](http://www.codeblocks.org/downloads/) |

Code::Blocks is extremely practical to use. It utilizes the GNU GCC compiler, which will run the program examples in this book. On a side note, the Code::Blocks website has its own forums for troubleshooting and a donation link for contributions.

### Dev-C++

Created by Bloodshed, Dev-C++ is another programming application that has its own compiler and Integrated Development Environment. Dev-C++ caters to programmers of C and C++. It can operate in Windows and there are now options available to run it in Linux.

| Download Link[http://www.bloodshed.net/download.html](http://www.bloodshed.net/download.html) |

Again, if you have not acquired a compiler, then Dev-C++ is small and simple to use. The program examples in this book do not have any problems compiling and running on this compiler. Like the Code::Blocks website, there is a forum for troubleshooting and a donation link for contributions.

## The Program Development Cycle

From a programmer’s perspective, when the code is written the initial stage is over, but behind the scenes a process begins of checking, compiling, linking and running the code, so it can build and operate a complete program.

The following diagram illustrates a top-down cycle of the process that a program is required to amble through for its complete creation.

![](Images/image00228.jpeg)

It would be something sensational if programmers were capable of creating programs that carried no compiler, linker, or run-time error. It might seem like they were living in a perfect world, and it would make us authors have less to write about. Unfortunately, the world is not perfect. Due to that fact, a compiler checks through a program at each stage while it attempts to build it, as shown above in the C++ Program Development Cycle.

Using the development process you can monitor every step the program development cycle undergoes and the reasons for it either progressing forward, closer to the finished program, or stalling, due to a certain type of error. During the process of the program being built, if there are any errors discovered then the compiler normally alerts you to them and stops the cycle. Afterwards, looking through the list of errors and fixing them, you can attempt to build the program again and, if everything processes through completely, then the program runs for you to see in action.

Nevertheless, there are some errors called run-time errors. These are only acknowledged by the compiler once the program is in operation and it is discovered because of a line of code not executing properly.

## Your First C++ Program

In the beginning of their coding education, most programmers begin with a simple program called "Hello World!" However, because most programming books have overdone this beginners program, in this book you are not going to start with this example. Instead, you are going to get a tad creative and develop a different style, which is also very simple.

Once you have read through the code and ran the program, continue reading, because the Program Syntax explains how each individual line of code operates.

Listing 1.0 – Hello Programmer.cpp

| // my first C++ program#include <iostream> // includes header file to programusing namespace std; // uses the standard namespaceint main() // starts program{              cout << "Hello Programmer!" << endl; // displays text on screen              cout << "Welcome To The C++ Programming Language Made Simple!" << endl; // more text displayed              return 0; // concludes program} |

Program Syntax: Hello Programmer.cpp

#### The Comment Line

The initial line of the program is a C++ comment, because it begins with two forwards slashes ( // ). When two //’s are entered, the program signals to the compiler that a comment follows suit.

#### The Preprocessor Line

Next, a preprocessor directive symbol ( # ) includes the header file <iostream> by enclosing it in open and close brackets <>. In this example, the header file <iostream> is selected for rendering the program capable of using certain declarations (functions, objects, etc.) Like the cout and endl objects.

| Knowledge: Header FilesA header file is filled with declarations of functions, objects and commands that are capable of being included in programs. To utilize a header file the preprocessor symbol ( # ) is required. |

#### The Namespace Line

The line using namespace std allows for the namespace called std – known as standard – to be used in the program. You can consider namespaces as data capsules that contains other types of data, capable of being used in a program.

#### The main Function

The main function introduces the opening of the program. Every console program begins with int main or variations of int main. In other books this might be written as _tmain or simply int main, followed by a set of parameters between its parentheses. It depends on what compiler is being utilized to develop the program.

The main function is always the opening of a program, no matter the situation. Other functions in a program are not capable of calling main, though they can return values to it.

After the main function there is an opening bracket { and near the end of the program there is a closing bracket }. Between these the program code is typed. Everything that is typed between these brackets are instructions the program is required to follow.

#### The cout and endl Objects

The objects that the program uses are next to show their faces. The cout object (pronounced see-out) displays the text between the double quotes, which follows after the object and the << symbols. The << symbols are output operators that communicate to the compiler that the text following is to be displayed. After the text you have another << with endl (pronounced end-l). This command simply ends the line. The next line down does exactly the same, but displays a different line of text.

#### The return Statement

The return statement concludes the program by returning the value 0\. This means that if everything went smoothly the program successfully reached this point and finished without any errors being reported.

| Technical Talk: BreakpointsWhen building programs with some compilers, like Visual C++, the program you create shall flicker up on screen and disappear in no more than mini seconds. The above program is an example of this. To stop it from immediately terminating, you must utilize breakpoints in the program.In Visual C++ locate the programs closing return statement and press F5\. A red spot appears inside the left border. When the program is ran, it shall halt before being commanded to close. |

## Programming Errors

Did you get any errors when coding the program for the first time? I'm guessing that the answer is yes. Don't worry about it. Compiler errors are normal to occur when programming. When the programs you write become larger with hundreds to thousands of lines of code, you will find that the compiler will discover countless errors. Once these errors are discovered – depending on the compiler being utilized – it will usually tell you what is wrong and suggest a fix.

| Technical Talk: Compiler Step-InThe majority of compilers have a function that is normally accessed on the menu bar, called Step-In. This function allows the programmer to move through a program one line of code at a time, which is practical for the programmer, as it is an efficient method when syphoning out errors or impractical code. |

### Compiler Errors

Compiler errors are probably the easiest type of error to correct when programming. If any of your programs happen to discover compiler errors then they’ll be found whilst the program is being assembled. They’re errors indicating something is wrong with the code inside your program and informs the compiler that it cannot run until the error is dealt with. In the majority of cases, these types of errors are due to incorrect syntax, meaning that somewhere along the line of programming, a typo has been created. When – and it is not the case of "if" – you receive a compiler error in your programs, they should be dealt with pronto.

### Link Errors

These types of errors normally occur because of something in the code that it attempts to link to, but fails. For example, in a program that uses the <iostream> header file, if the <iostream> isn’t typed correctly it can cause the program to send out a linker error, because the program is trying to use objects from a header file that it cannot recognize because of a typo. These errors are not the same as compiler errors and can be a little confusing at first-hand to the programmer learning C++.

### Run-Time Errors

Run-time errors can be the bane for programmers when they begin their quest with the C++ language, or any computer programming language for that matter. Run-time errors are the worst type of errors and one the biggest causes why troubleshooting forums are jammed with demands to fix a broken program. Sometimes run-time errors do not crash a program, but instead make it behave in a particular and unusual way.

| Knowledge: Testers & ErrorsEvery software company that produces programs for the public shall have a department of software testers. These testers are normally underpaid for the amount of work and hours they put in. Their job is to discover any type of error the programmers might’ve missed. |

## A Compile Error Program

Let us now create another program. However, in this we are going to discount a semi-colon so the compiler reads back an error for us to see.

Listing 1.1: Compiler Error.cpp

| #include <iostream>using namespace std;int main(){              cout << "Hello Programmer!" << endl;              cout << "This line delivers a compiler error!" << endl // no semi-colon              return 0;} |

Program Syntax: Compiler Error.cpp

#### No Semi-Colon

Reading through the code, you will notice that the semi-colon has been removed after the second endl object. Because every statement requires a semi-colon at its end, the compiler discovers an error and does not run the program. Instead, it comes back with an explanation of the error. See below.

#### Compiler Error

| &#124;&#124;=== Build: debug in compiler error ===&#124;C:\Chapter 1\Compiler Error\Compiler Error.cpp&#124;&#124;in function 'int main()':&#124;C:\Chapter 1\Compiler Error\Compiler Error.cpp&#124;8&#124;error: expected ';' before 'return'&#124;&#124;&#124;=== Build failed: 1 error(s), 0 warning(s) (0 minute(s), 0 second(s)) ===&#124; |

We are going to move onto the next chapter, where we shall discuss the mechanics of Hello Programmer.cpp.

## Time to Test Yourself

The following four questions are in regards to what you have just learned about programming in C++. Attempt these questions before you move forward to the next chapter.

| Test Yourself 
1.  C++ is a subset of what language?
2.  What does the cout and endl objects achieve in a program?
3.  What are the three types of errors that can occur in a program?
4.  Where should you place a semi-colon in a program?

 |

Chapter 02

# Anatomy of a Program

## Examining Hello Programmer

In the previous chapter you had a taste of programming by creating a simple Hello World style of program, although we called it Hello Programmer. This included several different segments to remember. Every part of the application was a small addition to what makes up a usual C++ program. In fact, even though Hello Programmer did not appear like much, it showed the central fundamentals required for every C++ program you build.

In this chapter we are going to examine Hello Programmer, breaking it down into the parts that formulated it.

### Include the Pre-Processor

When the programmer is finished coding and the build button is pressed, the compiler calls for the pre-processor directives (anything with a # prefixed) to kick in. The programmer does not need to panic at this stage, as the compiler examines the preprocessers automatically and obeys the instructions given to it by the program.

| Technical Talk: PreProcessor DirectivesThe preprocessor directives are individual lines of code in a program that starts with the # symbol. In the previous program the instruction given to the preprocessor was called include. |

When operated, the compiler searches through your code looking for any # symbols and seeing what comes after. In the previous two examples, the word include is attached to the # sign, meaning it incorporates the file written after the keyword include, and in this case this is <iostream>.

| Knowledge: The # SymbolThe # symbol that is used to include preprocessors in C++ is called the “hash tag” or “pound sign”. You might have heard of this when using the social media site Twitter. |

Note that the preprocessor directives that are included in a program do not require a semi-colon at the end. The reason is because the preprocessor directive is not a statement. Here are two examples of including the <iostream> header file. One is coded correct, while the other delivers an error to the compiler.

| #include <iostream> // this is correct#include <iostream>; // this is wrong |

### Header Files

The C++ collection of header files is enormous. When the programs that have been previously coded are examined we see only the header file <iostream>. Every full program in this book includes the <iostream> header file. But what is a header file?

A header file is a collection of declarations, objects and functions that can be employed in a program. By including a header file in a program, it is practically like you are implementing all the objects and functions in the file to the disposal of the program, so it can utilize them. So, when you include the <iostream> header file, it allows for the use of the cin, cout and endl commands to be employed in your programs.

### Comments

The comments in a C++ program are human-readable syntax to understand how certain written code operates. Comments are not read by the compiler at run-time. Instead, they are simply there to help the programmer, and anyone else who checks the programs code, to understand how it operates.

There are two forms of comments used in C++. First is the standard C comment that allows the programmer to divide the comment between multiple lines.

A C comment, which is old style, is written by starting with /* then writing the comment and ending it with */. These comments can fit on multiple lines and everything between the /* and */ is part of the comment.

| /* This is a C commentA C comment can run on multiple linesIt concludes once it reaches */ |

The other variation of a comment is the new C++ style, which runs on a single line. To create a C++ comment, you need to write two forward slashes // followed by the comment. Once a carriage return is initialized and the line breaks, the comment finishes. Therefore, to write another C++ comment, you are require to type // again.

| // This is a C++ comment// This is another C++ comment |

Reading through this book, you shall notice I use the C++ style comment in the program examples. Since the book concentrates on the C++ language, I believe it is correct to use this syntax. Although, as a programmer, you are eligible to employ the comment type that suits your own preference.

| Knowledge: Practise Writing CommentsWriting comments that the programmer understands is an easy job. Although, writing comments that outsiders are going to read and understand is a difficult task and requires practice. Writing a great, understandable comment for another person’s eyes is an art form in itself. Remember to practice commenting in every program you code. |

### Namespaces

The elements inside the standard C++ library are declared within a namespace.  In our previous programs, a namespace called std is employed before the primary function is open. You shall notice the code line using namespace does appear in all the programs written in this book. A namespace is called by the command using namespace followed by the name of the namespace.

### Function Blocks

In chapter 6 the subject of C++ functions are brought to our attention. But for now, I shall give a brief overview of what a function does. Functions are blocks of code that are great for individually separating certain data and keeping your code looking clean. The main function in the previous program is the function that starts the ball rolling for any executable program.

Every program in this book has a main function. It is a programs heart and soul. When you build a program, it runs from a top-down perspective through the code, starting in main, dealing with every line of code it comes across before it reaches a return statement and ends.

### Whitespace

Whitespace are the gaps that are left clear in your programs. These are the spaces, tabs and new-lines that are made so your program will appear cleaner and clearer. Whitespace – alike to comments – does not affect the program and are not read by the compiler. It is wise to use whitespace to format the look of your program code so it is easy to read.

## The Next Stage

Even though programs do get massive with thousands of coded lines, they operate under the same simple standard as our Hello Programmer.

Before we move onto the next stage, take a quick glance at one last program that uses data storage objects called variables and the input object inside the header file <iostream>, called cin. The latter object allows for the user to input their own data at the programs run-time.

Listing 2.0 – See-In and Variables

| #include <iostream>#include <string> // includes new header fileusing namespace std;int main(){              cout << "Please enter your name, programmer: "; // displays text              string yourName; // creates string variable              cin >> yourName; // input data into variable              cout << "Thank you, " << yourName << "." << endl; // displays variable data              return 0;} |

## Time to Test Yourself

The following four questions are in regards to what you have just learned about programming in C++. Attempt these questions before you move forward to the next chapter.

| Test Yourself 
1.  What is the difference between a C and C++ comment?
2.  What direction does program code follow when being read by the compiler?
3.  What is whitespace?
4.  Which keyword is required to place a header file in a program?

 |

Chapter 03

# Data Storage, Variables & Constants

## What is a Variable?

In today’s modern world, there are millions of computers constantly processing data on a daily basis. One question programming-wannabes ask is how a computer stores data it receives. The answer is in variables.

Essentially, variables act as containers that hold different types of data, which C++ can utilize and manipulate. When a variable is created, the computer stores it in memory banks, known as Random Access Memory (RAM). These memory banks have addresses that allocate space for a variable to situate in. However, remembering memory addresses is a difficult task. When variables are created they have a memory address and name. The latter acts like a label for the programmer to use in replace of an elongated address.

## What is Random Access Memory?

Random Access Memory is the main source that is capable of storing a computers actions, like creating a variable or storing a piece of text, which is cut to the computers clipboard. Once this is done, the computer can work with the RAM to access data quick and efficiently. The capacity of memory in a computer is how it dictates the volume amount of data it can potentially hold.

### Bits and Bytes

RAM is created from bits and bytes. A byte is larger than a bit. As a result, a byte is formed from 8 bits. Consider memory as small empty boxes ready to store items for the period of a programs runtime. Inside each of these boxes a program can store a byte of data.

Computer memory is accessed at random, unlike the data on a DVD or hard drive. Due to this purpose, data is capable of being accessed much quicker.

| Warning: Random Access Memory is Not Drive SpaceDon’t confuse the difference between RAM to the capacity of a hard-drive or DVD. To explain the difference, when you load a program it is accessed from a hard-drive, DVD or some other peripheral. When the program is loaded and run, any data the computer is required to know, is stored in RAM for the computer to utilize when required. |

## Dynamic and Static Typed Languages

We are going to examine two styles of typed languages that look at variable data types differently. These are known as:

*   Dynamic Typed Language.
*   Static Typed Language.

### Dynamic Typed Language

In a dynamic typed language, the decision on a variables type depends on the data value it’s assigned. For example, if you have a variable named myVar and it has a data value of an integer number, say 12, then a dynamic typed language will recognise the variable as an integer. Conversely, if you were to alter the value of myVar to something like ‘A’ then the compiler would start to appreciate the variable as a character.

### Static Typed Language

On the flip side, static typed languages have the rule a variable must be declared as a certain type before it can be utilized in a program. Therefore, if myVar is equal to the number 12, then most likely the variable would be declared as an integer, or perhaps some other numerical data type, like a float or short. In essence, static typed languages initially look at the data type to dictate what type of value it can store.

## C++ is a Static Typed Language

C++ is a static typed language because it has a set standard for different types of data that can be read by the compiler. As a programmer, you need to allocate the right data type with the correct data before the variable is used. It is pointless and terrible programming to assign an integer value to a string variable, as this shall come back with a compiler error.

## Learn the Data Types

Most programming languages, C++ included, have a variety of data types that are utilized to declare variables. The range of data types are shown in the table below, along with the individual sizes in memory.

| DATA TYPE | NAME | SIZE(in bytes) |
| int | Integer | 4 |
| short | Short Integer | 4 |
| long | Long Integer | 8 |
| long long | Long Long Integer | 8 |
| float | Float | 4 |
| double | Double | 8 |
| char | Character | 1 (per char) |
| bool | Boolean | 4 |
| string | String | 1 (per char) |

It is clear to see there are a lot of variable data types to learn. Although, you shouldn’t worry about not knowing the data types like off the back of your hand. You’ll gradually learn each one as you progress through this chapter and the rest of the book. Although, to begin, I want to show you how variables are declared and defined in C++.

## Declare Variables

Before a program can utilize different types of variables, a declaration of the desired variable is required. What this entails is coding the variable with its desired data type and user-defined name. To declare a variable the following syntax is required.

| data type | variable name |

Here is a coded example you might see in a program.

| int | myNumber |

In this example the keyword int declares the variable myNumber as an integer. Therefore, when you declare a variable the process of making space in memory begins. Many times a program shall require its variable to have values already initialized before runtime. What this means is variables are defined with values of their data types before the program is ran.

For example, an integer variable requires to equal a whole number, and a char variable requires a character, such as ‘E’ or ‘$’ for its definition. Note the single quotation marks for when declaring a char variable.

The next program demonstrates the concept of declaring and defining variables before run-time of a program.

Listing 3.0 – Declare and Define Variables.cpp

| #include <iostream>using namespace std;int main(){              int number; // declares integer variable              number = 50; // defines integer variable              cout << "The value " << number << " comes from an integer variable.\n" << endl;              char letter; // declares character variable              letter = 'C'; // defines character variable              cout << "The value '" << letter << "' comes from a character variable.\n" << endl;              double decimal; // declares double variable              decimal = 22.5; // defines double variable              cout << "The value " << decimal << " comes from a double variable.\n" << endl;              return 0;} |

Program Syntax: Declare and Define Variables.cpp

#### int Variable

After the opening of the main function, the initial variable – an integer – is declared and then defined with the value of 50.

#### char Variable

The second variable in the program is a char variable, which is declared. A char variable takes the value of a character, and in this program this variable is assigned with the letter 'C'.

#### double Variable

The final variable is a double, which is capable of storing decimal values. After the double is declared, it is then assigned the value of 22.5.

## Define Variables

Once you know how to declare a variable then defining it is a simple stage forward. The next lesson declares variables but leaves them to be defined by the user, using the cin object. The next program represents a telephone address book.

Listing 3.1 – Telephone Address Book.cpp

| #include <iostream>#include <string> // header file for string variablesusing namespace std;int main(){              cout << "Telephone Address Book.\n"; // the \n ends the line              // int and string declared variables              string contactName1; // creates a string variable              int contactNumber1;              cout << "\nEnter contact name: "; // the \n ends the line before text              cin >> contactName1; // input string variable data              cout << "\nEnter contact number: ";              cin >> contactNumber1; // input integer variable data              cout << "\nContact: " << contactName1 << "\t" << contactNumber1 << endl;              return 0;} |

Program Syntax: Telephone Address Book.cpp

#### string Header File

A new header file is added to this program, named <string>. This header file allows for the use of string variables in the program. The reason the file is required is due to the fact that string variables are not a built-in C++ type.

#### string Variable

In this program, the primary variable that is declared is a string variable, called contactName1.

#### The cin Object

A cin object calls the two variables at different points in the program. Each time it goes into action, it waits on data to be typed in from the user. This means the user shall be required to enter data before the program can move on, along through its top-down spiral. In the case of the string variable the user is allowed to type whatever he/she wishes. Then as for the second variable – an integer – the program awaits for the user to input a whole number value.

| Knowledge: Escape SequencesIn the previous programs you saw the code \n. Sequences similar to \n and \t are known as character literals or escape sequences. |

## Signed and Unsigned Variables

In C++ most variables can come under two different categories, which dictates their size and value range. These differences are known as signed and unsigned.

### Unsigned

An unsigned variable, whether an int, char or something other, has the word unsigned prefixed to the variable name, which signifies to the compiler the variable has a non-negative value range attached to it. By non-negative, it means that any unsigned variable cannot decrease below the value of 0\. See the difference in the examples below.

| unsigned int correct = 75; // shall compile properlyunsigned int wrong = -30; // shall cause a compiler error |

Because unsigned variables cannot reach below the value of 0, their maximum positive value is increased by double. In the next section you shall learn about the different data types, their categories and the different value ranges they can hold.

### Signed

Signed variables are the opposite of unsigned, whereby they can decrease their values below 0, and also when a signed variable is being declared it does not require the keyword signed to prefix the variable name. However, for programming clarity, the prefix keyword can be used if the programmer wishes.

For instance, both of the examples below are the same, but one has the word signed prefixed to it.

| int number = -20; // a signed integer valuesigned int number = -20; // an extra signed integer value |

A signed variable is known as a variable with a default value, similar to ones we have coded in the previous listings.

| Knowledge: To Be Signed or Unsigned?While learning the difference of both data type categories, a question arises of when to use a signed and unsigned variable. The answer is simple. When utilizing your variables if there are any that does not decrease below the value of 0, then it is wise to initialize them as unsigned. |

## The Different Data Types

As mentioned earlier, there are different data types you can give to initialize a variable. The following reveals and explains the data types that are utilized in C++. Every type shows the maximum and minimum value they can reach as signed and unsigned.

### Integers

The initial variable data type you’ll examine is the integer, known in C++ as the keyword int. Integers hold whole numbers, like 43, 170 or 2\. They cannot store decimal numbers, like 132.54 or 2.2\. Integers are initially allocated as signed, but can change to unsigned. Also, there are different types of integers, which we shall examine in this section, known as short and long. The diagram below shows the maximum and minimum value ranges for both categories of integers.

signed integer value range

| MIN | MAX |
| 32,768 | 32,767 |

unsigned integer value range

| MIN | MAX |
| 0 | 65,535 |

If you have an unsigned integer and your program attempts to decrease the value pass 0, then the numerical counter shall turn over to 32,767, instead of decreasing to –n and sending out a compiler error. Therefore, if the unsigned variable attempted the opposite and increased passed the point of 65,535 then it would turn over to 0.

### Short Integers

The short integer is also known as int and have a range value of -32,768 to 32,767, due to being identified as signed short. However, a short integer can have unsigned prefixed and it shall act exactly like a normal unsigned integer. You do not need to write out short int every time you want to declare a short integer, but instead just the keyword short.

| // each variable is the same, but declared differentlyshort number = -44;short int number = -44;signed short int number = -44; |

### Long Integers

The long integers have the difference when being declared because they require the prefix keyword long and unless they have the unsigned keyword before long then they are integer with a larger value.

The tables below reveals the different between an unsigned and signed long integer with their maximum and minimum values.

signed long integer value range

| MIN | MAX |
| -21,474,836,48 | 21,474,836,47 |

unsigned long integer value range

| MIN | MAX |
| 0 | 42,949,672,95 |

### Float

The float variable is another data type that uses numerical values, although, it does not just use whole numbers, but also decimal points. The float variable cannot be unsigned, like the different types of integers, although they can prefixed with the type of long and long long.

float value range

| MIN | MAX |
| 1.175494351e-38f | 3.40282347e+38f |

Next we are going to extend the size of a float by replacing it with double. A double has a higher value range.

### Double

The double variable is also a decimal point data type. It’s larger and can hold a higher value range than that of float. Although, the drawback is a double variable acquires twice the amount of bytes in memory then a float or an integer. Hence its name, double.

double value range

| MIN | MAX |
| 2.22507385850720138e-308 | 1.79769313486231571e+308 |

### Char

The char variable is a data type that allows you to use characters from the keyboard, like ‘a’ or ‘b’ or ‘£’ or ‘&’ for the programs. The different is when a number is used in a char variable it does not act like a numerical value, as it does in a integer or float. The reason for this is because it is cased between single quotation marks, which act like a switch that turns off any numerical functionality.

| // examples of char variableschar letter = ‘L’;char number = ‘5’;char sign = ‘$’; |

As shown, the three char variables all use single quotation marks. This means that the value of ‘5’ is not numerical – or at least not completely. The reason I use the term "not completely" is due to the fact that all characters typed from the keyboard have their own set value, which corresponds to the ASCII layout. The ASCII is short for "American Standard Code for Information Interchange" and is a character-encoding scheme, which is originally based on the English alphabet. This encodes 128 specified characters into 7-bit binary integers. The ASCII table designates a value for each character on the keyboard. Therefore, once again, char variables have minimum and maximum value.

Listing 3.2 – Different Types of Characters.cpp

| #include <iostream>using namespace std;int main(){              cout << "The different characters a char variable can hold are shown below:\n" << endl;              // three char variable storing different types of characters              char letter = 'E';              char number = '2';              char symbol = '$';              // displaying text with the three different types of characters              cout << "The char variable can store individual letters like " << letter << ".\n";              cout << "The char variable can store individual numbers as characters like " << number << ".\n";              cout << "The char variable can store individual symbols as characters like " << symbol << "." << endl;              return 0;} |

Program Syntax: The Different Types of Characters.cpp

#### char Variable

There are three char variables in the program that are declared and defined. Once these are created in the program, they are then individually shown on screen using the cout object. Also, you may also see that each of the variables has single quotation marks around them.

## Boolean and String Variables

### Bool

The bool variable only has two values to deal with. These values are true (1) and false (0). Devised by George Boolean, hence the name, the bool value is used in a wild array of programming languages like Java, Visual Basic and especially in C++. You will see this when learning decision making and return statements in C++. All the programs created so far in this book concludes with a Boolean value in their return statements: return 0.

Listing 3.3 – True or False.cpp

| #include <iostream>using namespace std;int main(){              cout << "The difference of true and false." << endl;              bool istrue = true;              bool isfalse = false;              // discovers what is true and false              cout << "The value of true: " << istrue << endl;              cout << "The value of false: " << isfalse << endl;              return 0;} |

Program Syntax: True or False.cpp

#### bool Variable

You see two bool variables in this program, which reveals the two different values the data type can either be.  The bool variables determine whether the data it contains is true (1) or false (0). When you move onto the if and switch statements, you will see the reason why the bool variable is crucial to C++ programming.

bool value range

| MIN | MAX |
| False (0) | True (1) |

### String

The string variable is not a built-in type in C++. Instead, to utilize the use of strings in your programs you have to include the header file <string>. To declare a string variable, it must start with the keyword string followed by the user-defined name. The basic idea for strings is that you can take a number of characters and string them together without any additional code, apart from the header file being included. Examples of a string are shown below, along with the char equivalent.

| #include <string> // remember to include to use stringsstring myName = "Tom";string myAge = "25";char myName[3] = "Tom"; // an array of charchar myAge[2] = "25"; // a smaller array of char |

Listing 3.4 – Full Name, Address and Number.cpp

| #include <iostream>#include <string>using namespace std;int main(){              // three string variables              string fullName;              string address;              string number;              cout << "Enter Your First Full Name: ";              getline(cin, fullName); // can use spaces              cout << "Enter Your Address: ";              getline(cin, address);              cout << "Enter Your Telephone Number ";              getline(cin, number);              cout << "\nHello, " << fullName << "." << endl // displays variable values                            << "You Currently Live At: " << address << "." << endl                            << "Your Telephone Number Is: " << number << "." << endl;              return 0;} |

Program Syntax: Full Name, Address and Number.cpp

#### The getline(...) Function

There is another method of using the cin object in C++ that also has extra features and allows string and char variables to perform more complex tasks. In this program the getline function allows for the user to input spaces into the string of text they write. Whereas, when using the cin object, if you were to write the full name of a person as say, "Abigail Roberts" then some of the string would truncate down to “Abigail”, since the cin object doesn’t allow for spaces. Although the getline function does.

To code a getline function the syntax looks like this:

| getline(input_command, | string/char variable); |

#### The cout Object

In this program the cout object is spaced out on multiple lines. This is allowed as at the end of each line (apart from the final one) there is no semi-colon ( ; ). As discussed earlier, the semi-colon is what concludes a statement. Because if there is no semi-colon C++ allows for the code to be separated on different lines. This is also because of the way in which C++ reads (or should I say doesn’t read) whitespace in a programs code.

| Knowledge: WhitespaceYou will learn more about whitespace in Chapter 5: Statements & Expressions. Although, just consider whitespace much like comments, as it is not read by the compiler at build-time. |

Now you know the basic types of variables that can be created in C++, you will examine how to create multiple variables of the same type.

## Creating Multiple Variables

We will use two data types to show how this works – an integer and the string variable. To write multiple variables of the same type you use the following syntax:

| data type | variable name, | variable name |

Here is an example of three integer variables that are declared using only the data type name once.

| // declare three int variablesint hours, days, months;hours = 24;days = 7;months = 12; |

Along with declaring multiple variables, you can also assign values to them using the same method. The three string variables below assign a string of characters to each one of the variables, which it is equal too. As you can see, the comma operator ( , ), allows for us to place additional variables in the declaration list. You could imagine each variable as a person in a post office with a parcel to post. Then think of the parcel being the data in the variable. After the list is complete you finish it off with a semi-colon.

| string hisName = "Peter",herName = "Ruby",yourName = "Tom"; |

Listing 3.4 – Login Details.cpp

| #include <iostream>#include <string>using namespace std;int main(){              cout << "Welcome back to the C++ Game." << endl;              cout << "Please enter your login details." << endl;              string username, password; // declares two string variables              cout << "\nUsername: ";              cin >> username; // input first string variable data              cout << "\nPassword: ";              cin >> password; // input second string variable data              cout << "\nWelcome back, " << username << endl;              return 0;} |

Program Syntax: Login Details.cpp

#### Multiple Variables

The program shows how to assign multiple variables by only using a data type name once. In this case, the string variable has been used to create two variables called username and password, which will be used in a program that aids in a login system.

## Place Variables in Memory

When variables are created the compiler allocates them into the computers RAM. When this happens they go onto a stack so each one can be used when the program calls for the use of the individual variable. This means that your program will be using a section of your computer’s memory.

## Manipulate Data Type Names

Pretty soon your programs will grow in size. Five lines of code will become twenty-five; twenty-five will turn into fifty and then fifty will be one hundred, etc.

Alongside that, as your programs grow so will the amount of variables and constants you’ll use. With this increase in number it can very tedious to write out such data types as unsigned short int or double float or signed char to initialize as variable or constant.

Instead, what you can do is give the format of a data type a user-defined name, which the compiler will see as equalling to the data type you tell it to equal to. The method of doing this is by using the keyword typedef.

The syntax for using typedef is:

| typedef | data type | new name |

Here is an example:

| typedef | long float | LFT |
| LFT | myFloat | 2364.20 |

Listing 3.5 – Changing Data Types.cpp

| #include <iostream>using namespace std;int main(){              typedef short int NUM; // NUM can be used in place of a short integer data type              typedef double DBL; // DBL can be used in place of a double data type              NUM shortInteger = 2; // assigns 2 to shortInteger using new type              DBL largeDecimal = 3408.43; // assigns 3408.43 to largeFecimal using new type              cout << "Two typedefs\n" << endl;              cout << "NUM replaces short integer with the value: " << shortInteger << endl;              cout << "DBL replaces double with the value: " << largeDecimal << endl;              return 0;} |

Program Syntax: Changing Data Types.cpp

#### typedef Variables

The program treats you to a new concept of declaring and defining variables, by using your user-defined name for a variable in replace for the built-in one.

Two variables are declared using the typedef command, which allows the programmer to assign a particular data type to a user-defined name. For instance, a short int has a user-defined name of NUM. This means instead of using short int each time, the programmer only requires to write NUM and the variable name of the short int, which is shortInteger.

Then another typedef is used to work with a double. This typedef is called DBL and is used with the variable largeDecimal.

| Warning: Too Many typedefsThe typedef is a handy tool to have when coding in C++, although, do not overuse it to an extreme, else you’ll discover you cannot remember what type a user-defined typedef replaces. |

## Using static_cast

What if you want to change the type of variable being used for another? One aspect you would have to consider is whether the value range of the current variable would fit in the new one. For example, an integer with a value of 400 would not fit into a character variable that stores a maximum value of 127\. However, there is a method called the static_cast function that allows you to alter a variable data type, no matter the size of the value it holds.

| int number = 4000;char letter = number; |

If you were to place the following variables in your program, depending on your compiler, you would either experience a compile error or a truncation of the number.

| Knowledge: TruncationTruncation means the number would be squeezed down to the highest value it can go, and in the case of an unsigned char, this would be 255. |

Due to a char not capable of reaching the value of 4000, this is an ineffective method to use when programming and can even crash the program. However, by using static_cast you can alter the use of how the char variable reads the value of 4000.

The syntax for writing a static_cast is:

| data type | variable name = | static_cast | <data type> | variable name |

You can use this syntax with the char and int variables now to show how it would work in a program. This program has been cut down to show the use of static_cast.

Listing 3.6 – Using static_cast.cpp

| #include <iostream>using namespace std;int main(){              char charLetter;              int intNumber = 68;              charLetter = static_cast<char>(intNumber);              cout << "static_cast: " << charLetter << endl;              return 0;} |

Program Syntax: Using static_cast.cpp

#### The static_cast Line

The two variables created in the program both interact with the static_cast command. The command is used to examine the number of the integer and to cast it as a char variable into charLetter. As the value of the integer is 68, this gives the result of the charLetter – once cast – as the letter D.

## What are Constants?

A constant is much similar to a variable. Yet, whereas a variable can alter its value range, a constant is assigned a value and has to stick with that throughout length of the program. Constants cannot change. If a programmer attempts to code a program where a constant alters its value at some point the program will not run or when it gets to the certain line of code where the value attempts to change, it will crash and send out a run-time error.

## Types of Constants

In C++ constants are used a lot. You may think that having a data container that cannot be altered might seem silly at first, but it is extremely handy, especially when it comes to debugging. Let me explain. If you have a constant or a set of them and you have an error that a value is changed and not allowed, then you know it is because it is situated in a constant you created in the program. Or on another example, if you fail to have constants in your program and only variables, it can be tricky to discover errors and bugs.

There are three types of constants that you can create in the C++ language. The three of these follow next:

### Literal

The literal constant is a constant that is assigned directly with a value, as though it is naked, and not concealed, by a constant represented with a name, like say a variable. For instance:

| const int number = 5; |

This is a literal constant, as it does not equal to anything but a direct value.

### Symbolic

When a constant is assigned to a value that is brought with a name, like say a variable called pocketMoney that is assigned 44, then it is known as a symbolic constant, because unlike a literal constant that simply receives a direct value, a symbolic constant is assigned with a representation of a value, not just a direct value.

| int pocketmoney = 44;const int thismonth = pocketMoney; |

I have placed this variable and constant into a program that shows you how they both work. This a small program and I know there are better methods to use constants then this simple demonstration. Yet, it shows the basic concept of a symbolic constant.

Listing 3.7 – Pocket Money.cpp

| # include <iostream>using namespace std;int main(){              int pocketMoney = 14;              const int THISMONTH = pocketMoney; // variable is same as const              cout << "This month the pocket money I received was " << THISMONTH << " pounds." << endl;              return 0;} |

Program Syntax: Constant Values.cpp

#### const Object

The keyword const creates a constant data type of an integer variable. For example, in the program above there is a constant integer called THISMONTH, which is assigned a variable carrying the value of 14\. By assigning a data type as a constant, the value of the data type cannot be altered throughout the program.

#### Variable to Constant

In the program a variable amount is placed into a constant via the assignment operator, which is looked at in the following chapter. The method in which this is accomplished is because C++ reads many of its commands from right to left. Therefore, the variable on the right, pocketMoney, has its value copied into the newly created constant called THISMONTH.

## Enumerated

Enumerated constants are much a foundation, or the building blocks, for a collection of more constants. This may sound mind-bending, but looking at the following example we can see how it works.

| enum COLOURS {red, blue, green, black}; |

In the example, COLOURS is the main constant, must like a parent. The constants in the brackets act like children to the parent. The constants in the brackets also have a value each. These values can be set when writing the enumerated constant out as such.

| enum COLOURS {red = 100, blue = 200, green = 250, black = 500}; |

There is no logical explanation that the values double each time. I have just written them out for the example like that. Instead you could have:

| enum COLOURS {red = 100, blue = 101, green = 20, black = 50}; |

You don’t always need to set values for each constant in the brackets. Instead, they could look like this:

| enum COLOURS {red = 100, blue = 200, green, black = 500}; |

This would mean that only three of the constants have been assigned a value, yet the compiler also automatically sets green a value that is one more than the value of blue as it precedes it in the list.

Below is an example program of using enumerated constants and displaying their values.

Listing 3.8 – Constant Custom.cpp

| #include <iostream>using namespace std;int main(){              // create an enumerated set of constants              enum CUSTOM { MON = 22, TUES = 28, WED = 34, THURS, FRI = 22 };              // displays values of each enumerated constant              cout << "Number of customers shopping each weekday" << endl;              cout << "Monday: " << MON << endl;              cout << "Tuesday: " << TUES << endl;              cout << "Wednesday: " << WED << endl;              cout << "Thursday: " << THURS << endl;              cout << "Friday: " << FRI << endl;              return 0;} |

Program Syntax: Constant Custom.cpp

#### The enum Constant

A set of enumerated constants is created near the beginning of the program. These signify the days of the week and gives information about the amount of customers that enter a shop and purchase something. Each day, apart from THURS, has a value, which is displayed individually a couple of lines down in the program.

## Time to Test Yourself

The following four questions are in regards to what you have just learned about programming in C++. Attempt these questions before you move forward to the next chapter.

| Test Yourself 
1.  Can you name all of the data types talked about in this chapter?
2.  What is the differences between unsigned and signed?
3.  Can a constant change its value?
4.  How many bits in a whole byte?

 |

Chapter 04

# Basic Operators

## What is an Operator?

An operator is a written symbol that aids in helping other forms, like variables and constants, to take action. There are different forms of operators in C++ that have their own sub-groups.

The list of operators are below:

*   Assignment Operator.
*   Mathematical Operators.
*   Increment & Decrement Operators.
*   Pre- & Post-Fix Operators.
*   Logical Operators.
*   Rational Operators.

In this chapter you will learn four types of these operators, which include:

*   Assignment Operator.
*   Mathematical Operators.
*   Increment & Decrement Operators.
*   Pre- & Post-Fix Operators.

## Mathematical Operators

An assignment operator is used for the purpose of defining certain pieces of data, like two variables, and assigning the result they give to another piece of data. The way you write this depends on what type you are defining the data to. When you use a variable to equal a value we look at it from the right to left, meaning that the data that is being equalled to can be on the left side. This is known as an l-value, and an operand on the right side is known as an r-value.

There are a range of mathematical operators in C++, much like any other programming language. There is the addition (+), subtraction (-), multiplication (*), division (/) and modulus (%).

Most of these will be pretty obvious to understand. You must have learnt at least four of these in your school days, yet the modulus operator may allude you a bit.

The modulus operator returns the remainder of a sum. Therefore, the following when return the value of 1.

| int mod = 16 % 5 |

;

Listing 4.0 – The Modulus Operator.cpp

| #include <iostream>using namespace std;int main(){              cout << "Hello Programmer! Time to do some C++ maths." << endl;              int value1 = 11; // assigns a value              int value2 = 2;              int valueTotal = value1 % value2; // modulus operator working with two variables to give another an answer              cout << "The total value of the two sums are: " << valueTotal << endl;              cout << "Now let us multiply that by another 100." << endl;              valueTotal = valueTotal * 100;              cout << "Now the value total is: " << valueTotal << " WOOHOO!!!" << endl;              return 0;} |

Program Syntax: The Modulus Operator.cpp

#### The % Operator

The program uses the modulus operator to find the remainder of two values. After displaying the result for the user to see, the program then multiples the remainder of the modulus result by one hundred, giving the result of 100.

## Problems with Division and Integers

One other aspect that I want to bring attention to is using the division operator with an integer. When you do division athematic it is not always best to use integers. The reason is shown below.

| int firstNumber = 30;float secondNumber = 10.2;int number = firstNumber / secondNumber; // returns inaccurate result |

The result of this would be 2.94, although because the variable number that holds the result is an integer it rounds of the number, as integers cannot hold decimal point numbers. Thus, this gives an inaccurate result.

The best way to do this is by changing the variable number to a float.

| int firstNumber = 30;float secondNumber = 10.2;float number = first / 10.2; // returns accurate result |

Listing 4.1 – Basic Maths.cpp

| #include <iostream>using namespace std;int main(){              cout << "Time for some mathematics." << endl;              int integerValue1 = 15;              int integerValue2 = 45;              cout << "Sum 1: 15 + 45 = " << integerValue1 + integerValue2 << endl;              float floatValue1 = 161.2;              float floatValue2 = 9.23;              cout << "Sum 2: 161.2 - 9.23 = " << floatValue1 - floatValue2 << endl;              int integerValue3 = 2;              int integerValue4 = 12;              cout << "Sum 3: 2 * 12 = " << integerValue3 * integerValue4 << endl;              float floatValue3 = 17.2;              float floatValue4 = 22.2;              cout << "Sum 4: 17.2 / 22.2 = " << floatValue3 / floatValue4 << endl;              return 0;} |

Program Syntax: Basic Maths.cpp

#### The + Operator

Our first operator is the addition operator. This is probably the first operator you learned in school. It simply acts that way in C++. It simply takes two variables and assigns the result to another.

#### The – Operator

The minus operator takes another two integers and assigns them to another. The value of the third integer is then displayed.

#### The * Operator

The multiplication operator is again one of those basic operator you would have used in school. In this program, it takes two integers and assigns the value to another.

#### The / Operator

The final operator to be used is the division operator. This uses float variables as if integer variables are employed in place of float, then the result can be inaccurate.

Most of this program will take you back to those days in the mathematics class – whether you loved or loathed them – and they are pretty easy.

## Mix Assignment Operator with Math Operators

In the previous example I had an example of three variables using the assignment operator. This is a great wait of storing an extra value into your program, but when you need to change one of only two variables in a program it is possible to have that variable equal to itself with another value. Like so:

| firstNumber = firstNumber + secondNumber; |

This means that the two variable are adding together and then the l-value (on the left hand side) variable stores a new value in itself. Furthermore, there is a shorthand version to write the code, which is used by professional programmers.

| firstNumber += secondNumber; |

This simply means the same as the result before. Even though the addition sign and the assignment operator has switched places, it still means the same.

| // this is firstNumber = firstNumber - secondNumber;firstnumber -= secondNumber; |

## Increment and Decrement

Two operators that always use numerical values are the increment and decrement operators. In programming, the most common value to add or subtract to is the number 1\. ++ has a method for accomplishing this.

To increase the value by 1 the method used is the increment operator.

| int number++; |

The other method is decrement, which does the exact opposite and subtracts 1 from the current value.

| int number--; |

## Pre- and Postfix Operators

Along with the increment and decrement operators, another two operators that work with numerical values are the prefix and postfix operators.

The difference between these two is where the increment and decrement symbols are placed on the variable and how they act with it.

The prefix operates by increasing or decreasing the value of the variable first before displaying it. This is why the operator symbols are attached before the name of the variable.

| ++number; |

The postfix operator works the other way around and is placed the opposite way. If we are trying to display the variable on screen and then decrease the value before displaying it again it would look like this.

| cout << number << endl;number--;cout << number << endl; |

The variable name comes initially before the postfix operator. This means that the pre- and postfix operators read from left to right. In the example of the prefix, it reads the operators first (++) then the variable name (number).

Listing 4.2 – Pre- and Postfix.cpp

| #include <iostream>using namespace std;int main(){              int decrementValue = 10;              int incrementValue = 0;              int prefixValue = 5;              int postfixValue = 5;              cout << "When we increase the prefix value from 5 it begins at: " << ++prefixValue << endl; //prefix value              cout << "When we increase the postfix value from 5 it begins at: " << postfixValue++ << endl; // postfix value              cout << "When we increment the value of 0 using a postfix operator it begins at: " << incrementValue++ << endl; // incrementing value              cout << "When we decrement the value of 10 using a prefix operator it begins at: " << --decrementValue << endl; // decrementing value              return 0;} |

Program Syntax: Pre- and Postfix.cpp

#### Prefix Operator

The prefix operator takes a numerical piece of data, like an integer, and either increases or decreases the value of the data by one. To achieve this the operator signs ++ or -- must prefix the name of the variable it is acting upon.

#### Decrement Operator

The decrement operator takes an integer value and decreases the value of that variable by one.

#### Increment Operator

The increment operator takes an integer value and increases the value of that variable by one.

#### Postfix Operator

The postfix operator works with either the increment or decrement operators to determine whether a value is to be changed before it is displayed on the screen or after. Using the increment or decrement operators, it will only alter the value by one.

## Operators and Precedence

In any programming language, one of the biggest aspects that most beginners struggle with is the notion of precedence. This means that the operators that are used in a line of code have a certain order in which they are computed. If we were to take a sum as in:

| sum = 4 + 4 * 3 – 1 % 2; |

The idea C++ has of looking at this figure to give sum its answer is by doing the following:

| Step 1: | 4 * 3 = 12; |
| Step 2: | 12 % 2 = 6; |
| Step 3: | 4 + 6 = 10; |
| Step 4: | 10 – 1 = 9; |

So, at the end of the figure, the answer sum would store in its variable is 9\. However, say you wanted the 4 + 4 to be the first to compute in then subtract by 1.

You would use parentheses around the numbers you wanted the compiler to compute first.

| sum = ((4 + 4) * 3 (– 1)) % 2; |

This changes the sum as it now follows these steps:

| Step 1: | 4 + 4 = 8; |
| Step 2: | 8 – 1 = 7; |
| Step 3: | 7 * 3 = 21; |
| Step 4: | 21 % 2 = 10.5; |

If in the last step the data type of sum was an integer, it would round down to 10\. But as you can see, due to parentheses being used it changes the environment of the precedence being computed.

Listing 4.3 – Precedence with Operators.cpp

| #include <iostream>using namespace std;int main(){              cout << "In C++ operators have an order of precedence." << endl;              int notPrecedence = 4 + 2 * 3 / 2 - 5; // does not use precendence              int isPrecedence = (4 + 2) * 3 / (5 - 2); // does use precendence              // two different results displayed              cout << "Without any precedence the value is: " << notPrecedence << endl;              cout << "With precedence the value is: " << isPrecedence << endl;              return 0;} |

Program Syntax: Precedence with Operators.cpp

#### Precedence

The precedence in this program determines what sums will be challenged first. The brackets around the certain numbers of (4 + 2) and (5 – 2) is what determines that they will be acted upon first.

## Time to Test Yourself

The following four questions are in regards to what you have just learned about programming in C++. Attempt these questions before you move forward to the next chapter.

| Test Yourself 
1.  What does the modulus operator achieve?
2.  How do you increment and decrement a value by 1?
3.  What is precedence?
4.  Can you explain how to use the pre- and postfix operators?

 |

Chapter 5

# Statements and Expressions

## Statements

Statements in C++ are a line of code, which orders the program to take action. Each written statement finishes with a semi-colon. The statement signifies to a compiler to initialize a certain amount of actions in a program. In the following example, the statement orders the compiler to display text and then end the line.

| cout << "A statement!" << endl; // display and end |

## Compound Statements

A group of statements together enclosed between brackets { } is known compound statements. Later in this chapter, you’ll see this in programs when you examine the if statement. Just to add, you have already seen a compound statement in use with the main function. A set of compound statements orders the compiler compute a set of actions, according to the coded instructions given.

## Expressions

An expression is any coded statement, which returns a value. This means expressions are in fact statements. If you look at the following example, you see t an expression that returns a value to the variable Z.

| int Y = 2;int X = 4;int Z;Z = Y + X; // expression returns the value 6 |

Here is another example of an expression, one you’ll have seen at the end of the program examples.

| return 0; |

## Make Decisions in Programs

Up until now you have looked at basic programs. You have looked at a top-down circuit of computer programming and seen how a basic program reads written code.

However, you are about to mix your programming up a little by introducing the concept of decision making. You are going to examine the steps of decision making through the involvement of the if, if  else and switch statements.

## The if Statement

You may have thought that a program that flows from top-down can get tedious. No computer game or application is built on this foundation. The initial method implemented to alter a boring top-down role in a program is to insert an if statement.

The if statement examines a Boolean condition to see whether it is true or false. If the condition is true the if statement will progress onto its own instructions, which can change the dynamics of the program. However, if the condition is false it will continue boringly as before.

Listing 5.0 – Are You Learning.cpp

| #include <iostream>using namespace std;int main(){    bool isProgramming; // if statement requires a bool data type    cout << "Are you learning to program? (type 0(no) or 1(yes)): " << endl;    cin >> isProgramming;    if (isProgramming == true) // if statement condition    {        // if previous condition is true execute program line        cout << "Yes. Then good luck! " << endl;    }    return 0;} |

Program Syntax: Are You Learning.cpp

#### The if Statement

You’ll notice at the beginning of the if statement there is no semi-colon. You should not put a semi-colon here, as it is the start of a new compound statement opening up to compute when the condition is true. In this case, it examines at a bool variable and reads it as true. Therefore, the program travels through the if statement, executing the one statement inside.

Listing 5.1 – A False Condition.cpp

| #include <iostream>using namespace std;int main(){    bool isProgramming; // if statement requires a bool data type    cout << "Are you learning to program? (type 0(no) or 1(yes)): " << endl;    isProgramming = false;    if (isProgramming == true) // if statement condition    {        // if previous condition is true execute program line        cout << "Yes. Then good luck! " << endl;    }    return 0;} |

Program Syntax: A False Condition.cpp

#### Line Does Not Execute

A near replication of the previous program, this one reveals the if statement doesn’t open up to execute the cout object statement, because the if condition is not equal to true.

## The if else Statement

Considering the if statement begins to create decision making in your programs, it still isn’t enough to make a bold and exciting program, which has randomness and the spark of uncertainty. When the if condition is false you have no second option when. So, the program simply skips the compound if statement and continues on its top-down rotation.

However, you can place a second decision maker after the if statement block called else. The else keyword allows for another decision execute when the if condition is equal to false. The else syntax looks like:

| if (condition){    // statements}else{    // statements} |

When the if condition has been tested and found out to equal false it jumps down to the else statement and executes and read from there. If the else condition is true it slips inside its block and executes the statements within.

Listing 5.2 – Are You Programming or Not.cpp

| #include <iostream>using namespace std;int main(){    bool isProgramming;    cout << "Are you learning to program? (Type 0(No) or 1(Yes)): ";    cin >> isProgramming;if (isProgramming == true){    cout << "Yes. Then Good Luck! " << endl;}else // the else statement offers variety{    cout << "Well, try your hand at something else." << endl;}    return 0;} |

Program Syntax: Are You Programming or Not.cpp

#### The else Statement

The else statement is there as a precaution in case the initial if condition is false. If this happens, then the program will jump down to the else statement and display on the screen "Well, try your hand at something else." Understand in some cases the if and else statement can be found out to be false, therefore none of the statements inside them are executed.

## Nested Statements

Along with the normal if and else statements you can attach other if and else statements to them. This is known as nested  statements.

| if (condition){    // statements    if (condition)    {        // more statements    }}    else    {        // statements        if (condition)        {            // more statements        }    }} |

| Warning: Too Many StatementsTry making a program with ten if statements, ten else and five nested if and else statements.When experimenting with the if statement, as a beginner, you will probably come up with something like that. Although, try as you might, there is a better and cleaner way to code such a section of a program. |

## The switch Statement

A switch statement is beneficial when a program is challenged with numerous options to choose from. Therefore, in a program you can implement if and if else statements, perhaps with nested if statements, but soon or later with enough if’s and else’s your program might turn into a wild ride on continuous indentions and dozens of if’s or else’s. Basically, it can read like a complete mess.

The switch statement is a shorter version of the if statement. It acts much like a menu. In advanced programming switch statements are required much of the time. For example, when developing a game, a switch statement is normally used for the game loop. Therefore, switch statements are a good thing for programming and wise to learn about.

Like the if statement, the switch statement takes a condition and determines what value it matches against in its list of cases. Here is the syntax for a switch statement:

| switch(condition) // if condition is true, switch statement opens{    case 1: // statements goes here with semi-colon    break;    case 2: // statements goes here with semi-colon    break;    case 3: // statements goes here with semi-colon    break;    case 4: // statements goes here with semi-colon    break;    default: // statements goes here with a semi-colon} |

It is much like the if statement, in the fact that it takes a condition and makes a decision depending on the result. The difference lies in the cases, where the condition will be true for only one of the cases and not the rest. This is a good statement for only selecting one option to use.

| Technical Talk: The break StatementBetween each case of the switch statements, you may have noticed a keyword called break. The break between each case is there to tell the compile once a selection is then it is to jump out of the switch statement and continue with the rest of the program. If the break statement was left out it would compute each case after the one selected. |

Below is an example of a switch statement, where you need to select a race of character for a computer game.

Listing 5.3 – Select a Character.cpp

| #include <iostream>using namespace std;int main(){    cout << "Select the type of character you wish to play" << endl;    cout << "1\. Human -- 2. Dwarf -- 3\. Dragon -- 4\. Ogre -- 5\. Gnome";    int theCondition;    cin >> theCondition;    switch(condition) // open of switch statement    {        // the condition result decides what case is examined        case 1: cout << "You wish to play as a human" << endl;        break; // break statement stops the switch statement        case 2: cout << " You wish to play as a dwarf" << endl;        break;        case 3: cout << " You wish to play as a dragon" << endl;        break;        case 4: cout << "You wish to play as an ogre" << endl;        break;        case 5: cout << "You wish to play as a gnome" << endl;        break;        default: cout << "Invalid input" << endl;    }    return 0;} |

Program Syntax: Select a Character.cpp

#### switch Statement

The switch statement requires a condition to start the process of deciding which case it will travel along.

#### The cases

The cases are what holds the result of the condition given, either by the program or by user input.

#### break Statements

The break statements in the program order the compiler once a decision has been made and the code executed, the switch statement can stop and the program can drop out The program can then continue the process of running through the rest of the program code.

| Technical Talk: The cases in a switch StatementWhen a switch statement is created and its condition is met with a value, it leaps down to analyse what case is require to execute. The cases inside a switch statement are the locations of executable code. Depending on what condition is met depends on what case is chosen. |

## Mixing Statements

You have seen both switch the if else statements now in operation by themselves. Although. in C++ statements are everywhere and work together. Therefore, it is possible to have a switch statement and an if statement together, or even vice versa.

## Time to Test Yourself

The following four questions are in regards to what you have just learned about programming in C++. Attempt these questions before you move forward to the next chapter.

| Test Yourself 
1.  What is a statement and an expression?
2.  How far can if statements be nested?
3.  When is it good to use a switch statement over an if statement?
4.  What is the break statement for?

 |

Chapter 6

# Functions

## What is a Function?

A function is a block in a program filled with statements and expressions to compute. Functions can be called upon from any other function to process everything inside it. In the essence of it, functions are a sub-program, a small piece of a larger idea, which a program might have.

Functions, therefore, act like building blocks in a program. They help to organise a program more suitably and help to break down the actions a program has, so it can accomplish small but significant tasks.

## Creating a Function

Functions can be hard to grasp, but with a little practice they are easily understood. The difficult part of a function is learning to write a one well. This is where a solid rule comes in handy to remember, especially for programming beginners.

A well written function should only have one task to accomplish. Whether a programmer wishes to add two numbers together, display a graphic on the screen or increase a player’s health in a computer game, the function should be tasked with one job.

| // function to increase a player’s healthint MaxHealthPotion(int playerHealth){    playerHealth = playerHealth + 25;    cout << “Your health is now “ << playerHealth << endl;} |

The MaxHealthPotion code shows a function is created to accomplish one task in a program.

## Declare a Function

In C++ to declare a function you must create a function prototype before main. The function prototype consists of at least three aspects. First you need to have the data type of the function, then the name of the it, which is user defined, then you have parentheses where parameters can be passed into the function. These can consists of literally anything from a variable to another function. In the previous example I have passed in an integer variable called playerHealth, which enables a program to use the variable in the function.

| int myFunction(int theParameter); |

## Define a Function

Once a function is declared it can be defined by writing it out with instructions of code, which you want the function to accomplish.

| // declaring a functionint MaxHealthPotion(int playerHealth); // function prototype//defining a functionint MaxHealthPotion(int playerHealth){    // statements are written here} |

Listing 6.0 – The Second Function.cpp

| #include <iostream>using namespace std;void SecondFunction(); // a user-declared functionint main(){    cout << "This is the main function" << endl;    cout << "Now we are going to jump into a new function." << endl;    SecondFunction(); // program passes into function    return 0;}void SecondFunction() // other function{    cout << "\nNow we are in the second function of the program." << endl;    cout << "When we leave here the program ends." << endl;    cout << "Goodbye!" << endl;} |

Program Syntax: The Second Function.cpp

#### User-Defined Function

The SecondFunction is the other function built in the program. It isn’t like the main function. Instead, it is a function fully built by the programmer. At the top of the program, you have the function prototype, which declares the function, but it doesn’t define it.

Because SecondFunction has already been declared, it can be placed underneath the main function. On the other hand, if the function didn’t have a prototype then its definition would’ve required to be written above the main function.

## No Prototype Function

This next example is a program with the SecondFunction again, but this time the function prototype is omitted and the function moved above main.

Listing 6.1 – The Second Function with No Prototype.cpp

| #include <iostream>using namespace std;void SecondFunction() // function defined and declared{    cout << "\nHello! This is the second function." << endl;    cout << "This time around, the function is built with no prototype." << endl;}int main(){    cout << "We are in the main function" << endl;    cout << "Stepping over to the SecondFunction." << endl;    SecondFunction(); // calls the other function    return 0;} |

Program Syntax: The Second Function with No Prototype.cpp

#### No Function Prototype

Because no coded prototype shows in the program it means SecondFunction is required to be declared and defined above the main function. The reason is due to the fact that the program is required to know what functions are going to be working with the program before the main function is reached – and without a function prototype, it won’t know unless the function is written before main opens up.

| Technical Talk: Write Functions in Header FilesOne of the places a large majority of programmer’s code functions is inside header filed. The header file is then linked to a.cpp file. |

## Working in Scopes

The question of scope in programming languages is large enough that if a programmer makes it a mistake it could cause an error. When talking about scope in functions there are two words required to be addressed: Global and Local.

When working with constants or variables in functions you need to consider scope and the difference between the two methods.

### Global Data

Data like variables and constants coded outside of any function or outside its parentheses, even main, is known as global data and can be employed anywhere in a program.

### Local Data

Variable and constants created inside a function are known as local data. The pieces of data inside a function can only be used inside the function it is created in. Although, you can return the result of the data to main.

Listing 6.2 – Global Variable.cpp

| #include <iostream>using namespace std;int number; // global integer variablevoid SecondFunction(){    // global variable being used in SecondFunction    number = 5;    number += 5;    cout << "The Number Is: " << number << endl;}int main(){    //global variable being used in main    number -= 5;    cout << "The Number Is: " << number << endl;    SecondFunction(); // calls the other function    return 0;} |

Program Syntax: Global Variable.cpp

#### The Global Variable

The one global variable in the program is outside any function, which makes it global. Because it is global, it means any function declared in the program may use it in its definition.

In the example, the variable uses the addition and subtract operator in different functions to show the different results that you can achieve.

## Parameters and Arguments

Functions are capable of carrying across data passed to it from a calling function, like main. The information gets stored as parameters in between the parentheses.

The arguments is the data passed into the functions. An example of this is shown in the follow part as a small program.

Listing 6.3 – Function Arguments.cpp

| #include <iostream>using namespace std;int Printed(int numberofsheets, int sheetsbeingprinted); // function prototypeint main(){Printed(80,22); // parameters inputted for function printed}// function receiving argumentsint Printed(int numberofsheets, int sheetsbeingprinted){    int plainsheets = numberofsheets;    int printedsheets = sheetsbeingprinted;    int sheetsremaining = plainsheets – printedsheets;    cout << “Printer sheets remaining: “ << sheetsremaining << endl;    return sheetsremaining;} |

Program Syntax: Function Arguments.cpp

#### Functions with Arguments

The user-defined function carries two integer arguments inside it. When the function is called in the main function, the argument list is filled out with two values that are passed into the user-defined function. These are then used in the function with code to resolve some arithmetic, then return the end result back to main.

## Calling Functions

The method that C++ and most other programming languages use to tell the programs to work with other functions alongside main() is to write the name of the function with its parameters filled out, if any.

| int main(){    Printed(80,22); // parameters inputted for function printed} |

However, even though this example shows main as the function with the calling function of printed in, it is not always main that is required to have the calling functions inside it.

| int Printed(int numberofsheets, int sheetsbeingprinted){    int plainsheets = numberofsheets;    int printedsheets = sheetsbeingprinted;    int sheetsremaining = plainsheets – printedsheets;    cout << “sheets remaining: “ << sheetsremaining << endl;    insertmoresheets(additionsheets);    return sheetsremaining;} |

As you can see, there is no data type required for the insertmoresheets function when being called in the printed function.

## Return Values

Every function written owns a return value and depending on its data type shall dictate whether the value is null (void) or higher. When the called function (normally main), concludes, it passes whatever value follows the keyword return.

When dealing with the main function, it is usual to end it with a return value of 0\. However, in this case, no matter what value is eventually returned from the main function, the actual value is forwarded to the operating system on the computer so I can obtain the ability of catching any detected errors in a program.

| Technical Talk: Return ValuesA return value is dictated by the function data type. For instance, a function of type int shall return an integer value. |

## Writing Return Statements

A return statement is characterised as an expression. This dictates the line of code returns a value of some type. Therefore, if a return statement simply follows the rule that it requires to return a value then the method to write one is rather flexible. Below is a small list of different return statements.

| return myNumber;return 0;return 5 + 2;return 3 * (4 % 2);return MyFunction(); |

| Knowledge: The Last StatementIf the last statement (MyFunction) returns a value, then every one of the preceding statements are legal and accepted in C++. |

Just to note, it is always possible to have more than one return statement embedded in a function.

## Multiple Return Values

Apart from functions that are declared with type void, each one initialised is required to return a value before it concludes.

Multiple return statements that have different values, but correspond to a functions defined data type – for example, an integer function with an integer variable – can co-exist in a block of code. At the end point of a program is a return value – unless the function is of type void. Therefore, it returns the defined data type to the called function. For example, if a function called FindAge() is integer based, then somewhere throughout the breadth of the function block an integer value is required to return to  the called function.

The program below utilizes multiple return statements and values with the FindAge() function. The value returned to the calling function depends on the outcome from the users input.

## The void Function Type

The void data type is used for a function heading and returns no value. In some previous examples of functions we have seen the function data types range from int to string. However, you will also discover now that there is another data type called void, which is used when a function does not need to return a value.

Listing 6.4 – What is Your Age.cpp

| #include <iostream>using namespace std;int FindAge();int main(){    FindAge();}int FindAge(){    cout << "What is your age? ";    int age;    cin >> age;    if (age < 18)    {        cout << "You are too young to drink." << endl;        return age;    }    else if ((age >= 18) &&  (age <= 68))    {        cout << "You are of working age." << endl;        return age;    }    else    {         cout << "Enjoy your retirement." << endl;        return age;    }    return 0;} |

Program Syntax: What is Your Age.cpp

#### return Statements

Functions return a value by utilizing the keyword return followed by the value. Shown in the previous listing above, the return keyword can appear numerous times in a function. The three return statements above the concluding one, will return a different value depending on what is entered by the user.

## Overloaded Functions

Functions can be created a second or third time using the same name, but with a different combination resting sandwiched between the parentheses. This is known as overloading a function.

Look below at these three player functions. Each one is called the same, but due to the difference between the parentheses they act individually to each other.

| player(string pName);player(string weaponType, int ammoAmount);player(int pLives, float pHealth, float pMana); |

When you have functions like this, the method to call a specific one is to indicate it with the list of parameters needed.

Listing 6.5 – Overloaded a Function.cpp

| #include <iostream>using namespace std;//declared overloaded functionsvoid player (string pName);void player(string weaponType, int ammoAmount);int main(){    // each function below is a different function    player("Peppercorns");    player("Steel Holster Gun", 200);    return 0;}void player(string pName){    string playerName = pName;    cout << playerName << endl;}void player(string weaponType, int ammoAmount){    string weapon = weaponType;    int ammo = ammoAmount;    cout << "Your weapon is " << weapon << " and you have " << ammo << " bullets remaining inside it." << endl;} |

Program Syntax: Overloaded a Function.cpp

#### Overloaded Functions Called player(…)

In this program there are two functions that are overloaded with the equal name of player. The reason both of them can be used and not be interrupted by one another is because their parameters are different.

The first function has one string parameter, while the other has two. One of the parameters is a string variable and the other an integer.

## Inline Functions

When your program calls a function it leaps out of the calling function and into the function itself. The computer then takes those instructions in the functions at it computes them. When doing this, it creates a copy of everything it reads in the function and sets it to memory for when the calling function comes back to it. This is great if you have a large function (5-7 lines or more). Yet, if you have a small function and your programs is like to call that function numerous times then it will slow your program and the processing of it down. The method to avoid this is to prefix the function title with the keyword inline.

| inline int MyInlineFunction(); |

In the C programming language you would declare inline functions using the #define macro. Although, through the development of C++, the inline keyword has taken the place of #define when declaring functions that you want as inline.

## Computer Memory and the Stack

When a function is called in a program its code initializes it to jump from the function to the calling function. Any parameters that are in between the functions parentheses are passed in as arguments as it is being called. When the function reaches the end it looks for a return statement and a value. If the statement exists (void functions have no return statement), the program reads it and jumps back to the calling function.

When a program is compiled and ran it will create a stack. The stack is a certain placement offset in computer memory that has been allocated for the program being run.

In terms of everyday things you can imagine a stack as the queue in your local post office or a pile of plates in your kitchen cupboards. The reason for this is because a stack has the method of last-in and first-out.

This means that whatever is placed on the stack last will be removed first. Look at the example of these mats in the following image.

If you take the idea of these multi-coloured mats as a stack, then each one will have a certain value attached to it. One of these numbers will be the stack pointer. The stack pointer is a small register, which holds the address of the programs last request. Everything that is below that number is considered to be off the stack.

## Time to Test Yourself

The following four questions are in regards to what you have just learned about programming in C++. Attempt these questions before you move forward to the next chapter.

| Test Yourself 
1.  How do you declare a function?
2.  What types of return statements are allowed?
3.  Can you explain how local and global data operates in a program?
4.  What is an overloaded function?

 |

Chapter 7

# Extra Operators

## Logical and Relational Operator Types

In this chapter we are covering the other two types of operators that C++ can operate: logical and relational. Both these can be incorporated into programs by using a method similar to the mathematical operators.

Relational operators determine the size of an object compared to another object. For example, they can determine whether the values given to them are smaller, larger or equal to each other.

### Relational Operators

The first operator types we are going to look at are the relational operators. With the relational operators you are capable of determining whether a value is lower, higher or equal to another value. There are five relational operators C++ uses. The list below shows them all.

*   ==        Equal To
*   >=        Greater Or Equal To
*   <=        Less Or Equal To
*   >=        Greater Than
*   <           Less Than
*   !=          Not Equal To

### Equal To

The equal to takes a set of values and determines whether they are equal to each other. The syntax for the equal to operator is as follows:

| bool variable = value == value;bool isitEqual = 4 == 4; // the two values make isitequal true.bool isitEqual = 8 == 4; // the two values make isitequal false. |

The following program shows how the equal to operator works with an if and else if statement.

Listing 7.0 – Equal To Operator.cpp

| #include <iostream>using namespace std;int main(){    int isitEqual;    int theNumber;    cout << "Type a number between 4 and 8: ";    cin >> isitEqual;    cout << "Type another number between 4 and 8: ";    cin >> theNumber;    if (isitEqual == theNumber) // is variable values equal>    {        cout << "Your two numbers are equal to each other."<< endl;    }    else    {        cout << << "Your two numbers do not equal each other."<< endl;    }    return 0;} |

Program Syntax: Equal To Operator.cpp

#### The if Condition

Before the if statement is open, it checks to see the value of the two variables are equal. If this is not true, as the conditions of an if statement is set as a bool value, then it passes down to the else statement.

### Greater Than

The greater then operator observes whether the initial value is higher than the second. If the value is higher than the program will compute it as true, else it will be false. The syntax for greater then is:

| bool variable = value > value;bool isitGreater = 8 > 4; // the two values make isitGreater truebool isitGreater = 2 > 4; // the two values make isitGreater false |

Listing 7.1 – Greater Than Operator.cpp

| #include <iostream>using namespace std;int main(){    int isitGreater;    int theNumber;    cout << "Type a number between 4 and 8: ";    cin >> isitGreater; // input the first number    cout << "Type another number between 4 and 8: ";    cin >> theNumber; // input the second number    if (isitGreater > theNumber)    {        cout << "Your initial number is greater than the other." << endl;    }    else    {        cout << "Your initial number is not greater than the other." << endl;    }    return 0;} |

### Less Then

The less then operator does the opposite to the greater then. Whereas the greater then checks to see if the initial value is higher than the second value, the less then checks for the opposite by looking for the initial value to be lower.

| bool variable = value < value;bool isitLess = 4 < 8; // the two values make isitLess truebool isitLess = 4 < 2; // the two values make isitLess false |

### Greater Than or Equal To

The greater than or equal to operator is a combination of both greater than and the equal to operator. In this case the initial value can be either greater or equal to the second value for it to return true.

| bool variable = value >= value;bool isitGreaterorEqual = 8 >= 4; // the two values make isitGreaterorEqual truebool isitGreaterorEqual = 2 >= 4; // the two values make isitGreaterorEqual false |

### Less Than or Equal To

The less or equal to operator works on the same method as its counterpart, greater or equal to, only this time the initial value has to be equal or less than the second value.

| bool variable = value <= value;bool isitlessorequal = 4 <= 8; // the two values make isitlessorequal truebool isitlessorequal = 4 <= 2; // the two values make isitlessorequal false |

### Not Equal To

The not equal to operator throws the idea of true and false a tad on its head, or it may seem that way as a beginner programmer.

By using this operator you are clearly stating that you are looking for the initial value to not be equal to its second value. Thus, you don’t want them to match true. If in the case that the operator does find them equal than it returns false.

## Logical Operators

Since we have looked at relational operators, it is time now to move onto logical operators. With logical operators you can ask numerous questions about the differences in your values. For example, the operator AND (&&) allows for the addition of our values to be questioned.

|     if (x == y) && (y < z)    {        // then do something    }    else    {        // do something else    } |

### AND (&&)

What you just read was a snippet of the AND operator in operator with programming code. The AND operator can evaluate two or more expressions and if each one is true then the AND operator returns a result.

### OR (||)

Like the AND operator, the OR operator evaluates two or more values to determine whether they are true or false to each other. If one of them is true then the program will return the value of true. What happens with the OR operator with two expressions is it checks the initial expression and if it’s true then it doesn’t move onto the next expression but instead returns true, as at least one is true. Whereas with the AND operator requires all its expressions to be true, the OR operator only requires one.

| int x = 5, y = 5, z = 2;bool n = (x == y) &#124;&#124; (y < z); // n returns truebool m = (x != y) &#124;&#124; (y < z); // m returns false |

### NOT (!)

The logical operator for NOT (!) Determines true if the expression actually being tested comes back as false. That might be difficult to understand, however, what the operator is saying is if the expression is false then return true. Basically, switch it on its head from all the other operators.

| int x = 5, y = 5, z = 2;bool n = (x != y) && (y >  z); // n returns truebool m = (x != y) && (y < z); // m returns true |

Chapter 8

# Loops

## Programming Loops

Repetition is a crucial factor in the world of programming and something that every developer depends on in their programs.

To create a repetition in your programs you need a type of loop. If it wasn’t for loops your program would eventually play through and then stop, quitting out to the desktop.

There are three types of loops in C++. The while, do while and the for loop. Each does the simple task of repeating over code until it reaches a certain value, but each has its own method of doing this.

### The while Loop

The while loop is the first in the three loops we will examine. The syntax for the while loop is as shown.

| while(condition){    // do something} |

The first aspect that the while loop does is to test to see whether the condition is true or false. If the condition is true then the loop opens up and the code between its brackets is computed. Yet, if the condition is false, then the loop is bypassed and the program carries on.

The loop will carry on until the condition in the loop is met, by which time it will then jump out of the loop to progress with the rest of the program.

### The do while Loop

The do while loop is similar in operation to the normal while loop, because it requires data to examine. However, the do while loop is different due to it does at least one round of testing before coming to the condition. The syntax for the do while is written below.

| do{    // do stuff} while (condition); |

As you can see the loop opens up with the keyword do and then progresses through until it reaches the while keyword, where it tests the condition. If the condition is not met then the do while loops over again.

Here is an example:

Listing 8.0 – do while Loop.cpp

| #include <iostream>using namespace std;int main (){    short x = 7, y =0; // initialise two short variables    do // starts do while loop    {        cout << "Your number is: " << x-- << endl; // displays variable in loop    } while (x > y); // ends do while loop    return 0;} |

Program Syntax: do while Loop.cpp

#### do while Loop

This program takes two integer variables x and y and utilizes them in a do while loop until they eventually match. Once the value of x is 0 it stops running the loop.

### The for Loop

The for loop takes an initial value and tests it against another. If the initial value is not equal to the second statement, the third expression kicks in, which normally tells the program to increment or decrement the value. The syntax for a for loop is:

| for ( i = value; i = value; i++) {    // do something;} |

## Nested Loops and Statements

Because the inside of any loop we’ve examined is a collection of compound statements, it is valid to be capable of placing loops within loops or even if or switch statements. It works on the same basis of nested if statements with other if statements etc.

An example of nested loops with if statements is shown below. In the example we are trying to decide what happens when a player slays a creature in a game.

Listing 8.1 – Nested Loops.cpp

| #include <iostream>using namespace std;int main(){    int creaturehp = 100;    int playerattpwer = 32;    do    {        cout << "Player attacks creature!" << endl;        creaturehp = creaturehp – playerattpwer;            if (creaturehp <= 0)            {                cout << "Player has slayed the creature!" << endl;            }            if (playerttpwer == 32)            {                cout << "You slayed the creature in one hit." << endl;            }            else if           {             cout << "Player strikes the creature for " << playerattpwer << “!” << endl;             cout << "The creature now has " << creaturehp << " points of health remaining! " << endl;         }    } while (creaturehp > 0);    return 0;} |

Program Syntax: Nested Loops.cpp

#### The Nested if Statement

The nested statement in the loop is another if statement that checks to see if the condition of a variable is equal to the value of 32\. If it is then the user receives the message, "You slayed the creature in one hit.".

#### Nesting the Loops and if else Statements

This might be the largest program you have wrote so far, it is the largest in this book. However, I want you to get use to writing large programs so you don’t become complacent and stick with small programs all the time. Programs are thousands, sometimes millions of lines of code, which need to be handled by a programmer or a group of programmers. This last program was over 20 lines of code. As we progress further onto the next part the programs will be much larger, but nothing that you cannot handle.

| Warning: Too Many if’s and else’sNesting loops is a good tactic in programming. Although, it can get out of control if too many if and else statements are written one after each other. The best tactic to use is to have two or three nested statements or change them for a switch statements with numerous cases. |

Chapter 9

# Pointers

## What is a Pointer?

A great piece of toolkit a C++ programmer is handed when they decide to code is the something called a pointer. However, what is a pointer?

The pointer is a variable that indicates a position in memory and nets its address. Therefore, with the memory address in its hands, the pointer can directly manipulate the computer’s source of memory. This makes pointers great to work with, once understood.

## Understanding Pointers

For a beginner to C++, learning the notion behind pointers is the bane of their programming education. When the idea of messing with your computer’s memory is fixed in your head, there is a moment when you begin to become a little too cautious. It is totally understandable. And when using a pointer, essentially you are allowing the program code to mess with your computer’s memory. However, do not panic as it sounds worse than it truly stated.

### Memory Addresses

When the discussion of variables came up in chapter three, you learned when a variable is created it is assigned a memory address.

Well, to understand the full impact of how pointers operator with memory and their addresses, you’ll require a little more knowledge about memory.

Created variables are stored in computer memory. Every integer, float, char, string, etc. is given a memory address location. These locations are sequentially numbered after one another.

Due programs sorting and maintaining addresses of its given variables, the programmer doesn’t need to trouble about such complex matters. I.e. the program, if coded correctly, will do it.

The next part of the program uses the Address of Operator to demonstrate how to obtain the information of a variable address and display it on screen.

The Address of Operator is employed in programs to discover the memory addresses that holds a variable.

Listing 9.0 – Understand Memory Address and Data Pointing.cpp

| #include <iostream>using namespace std;int main(){    int number = 5; // integer variable    int *pPointerToValue = NULL; // initialized pointer to NULL    pPointerToValue = number; // pointer points to integer variable    cout << *pPointerToValue; // dereferencing pointer to show number variable    return 0;} |

Program Syntax: Understand Memory Address and Data Pointing.cpp

#### Pointers and Addresses

When you create a pointer you’ll require to point to something, whether a variable or a NULL value. If you forget to initialize a pointer it can cause problems for the program and may even crash. This is because it produces a memory leak error. Therefore, it’s wise to initialize a pointer, as in the previous example, even as NULL (0) if you have nothing else to assign it too. Take another look at how it’s done.

| // pointers initialized as NULLint *pMyPointer = 0;int *pMyPointer = NULL; |

| Knowledge: Pointer Naming ConventionPointers can be assigned a legal name, just like a normal variable. With initializing pointers it is good programming grammar to prefix the name of with a"p". For example:int pMyPointer = NULL;int pAnotherPointer = 0; |

## The Dereference Operator

When you use a dereference operator * on a pointer, the value stored inside the indicated variables memory address is retrieved. For example, if a program had an integer variable equalling to the value of 33 and a pointer indicated to it, it could use a cout object and the deference operator to display the variables value. Have a look at the following snippet.

| int myAge = 33;int *pMyPointer = myAge;cout << *pMyPointer << endl; |

## Dynamic Memory

### new

The new operator is the method for allocating dynamic memory. You use the new keyword by assigning it with a data type.

| int *pMyPointer = new int; |

To create an array of new types you add an element number after the data type. You will learn about arrays in chapter 11.

Here is how it looks with an array of five elements.

| int *pMyPointer = new int [5]; |

### delete

After you have finished with a pointer you need to delete it from the program so that you don’t get any memory leaks. Leaks in memory can cause your program to crash and even have your memory before corrupted. So, not a good thing.

To delete a pointer you simply use the delete keyword before the name of the pointer.

| int *pMyPointer = new int;delete pMyPointer; |

To delete a pointer that points to a new array you place brackets after the keyword delete.

| int *pMyPointer = new int [5];delete[] pMyPointer; |

Chapter 10

# References

## What is aReference?

In C++ a reference is better known as an alias. This means it can reference that data of another object under its own name. You will see that this is extremely practical when it comes to passing the data objects hold between different functions.

## Create a Reference

A reference in C++ is created by writing out the type of object it accounts to (int, float, char, etc), followed by the reference operator ( & ) and then the name you give the reference. For example, below shows an example of how a reference is initialised and aliases with the data of a variable called target.

| int target = 5;int &targetRef = target; // references target variable |

That is how a reference is coded in C++. Thus, when you initialise a reference you use the name of the object that requires referencing, in this case the object name is target. Now, let’s see what has happened. Once a reference has been initialised by an object it is an alternative name for that target. Thus, if we were to go:

| targetRef++;    cout << target << endl;cout << targetRef << endl; |

They would both equal to 6\. This means that whatever is done to manipulate he reference also changes the initial piece of data, i.e. Target.

Let’s look at a listing example of how the value is changed for both reference and object, no matter what one is being used in the code.

Listing 10.0 – Reference a Object.cpp

| # include <iostream>using namespace std;int main(){   int target = 5;   int &targetRef = target;   cout << "The target number is: " << target << endl;   cout << " The target reference number is: " << targetref << endl;   cout << "Increase target value by 1 = " << ++target << endl;   cout << "Increase target reference value by 1 = " << ++targetref << endl;   return 0;} |

Program Syntax: Reference a Object.cpp

#### Object Reference

The program references an object by first creating a variable called target and assigning it the value of 5. Then a reference, using the Address of Operator ( & ) is brought in to reference the variables value.

| Technical Talk: Reference Name ConventionsReferences are capable of using any type of legal name that a variable or constant is allowed. However, many programmers prefix reference names with the letter r.int rMyRef; // integer reference |

## The Address of Operator for References

When writing programs that include references, you are required to ask for its address. The reason for this is because of the method that references operator with the objects they alias. To accomplish this. The address of operator is required to be employed with any reference.

| Knowledge: The Address Of Operator ( & )Amongst this book, included this chapter, you have seen the & symbol used for different aspects of programming. For references, this is known as the address of operator, which is used to fetch the address of the object that the reference is aliasing |

Listing 10.1 – Address Of Reference.cpp

| #include <iostream>using namespace std;int main(){   float Decimal = 25.5;   int Number = 5;   float &rtodecimal = decimal;   int &rtonumber = number;   cout << "Decimal address: " << &rtodecimal << endl;   cout << "Number address: " << &rtonumber << endl;   return 0;} |

Program Syntax: Address of Reference.cpp

#### The Address of Operator

The & symbol is used in this program to not show the value, but the memory address where the variable is located in the computers RAM.

## What Objects Can Referenced?

No matter what objects you create in your programs, all of them can be used with references. Although, do not go overboard in trying to reference everything that your program has. You should only use references when they are required, else it is bad programming.

Of course, when i say any object can be reference, i mean any. Although, do not try to reference a class, because it shall not work. Instead, you can reference an object that a class has built. We will get into classes soon in the next chapter.

## Keep One Reference for One Object

It is good programming grammar to understand the rule that you shouldn’t reassign a reference to a different target once it is already aliasing an object. If this happens it can get very confusing. Instead it is better to make another reference and assign it to another object. The reason for this is due to the fact that programmers can become very disoriented by what a program does and how it treats references. Once you have a reference is one place, keep it there for the whole of the program.

| int refOne;int objectOne = 6;refOne = objectOne; // reference one object is goodint objectTwo = 12;refOne = objectTwo; // switching objects is not good |

## NULL Unused Pointers

Any pointer that is not initialised or been deleted using the delete keyword, it must be set to null. Doing this allows the pointer to have a default value and saves from your program from crashing at any moment.

## Do Not NULL References

However, when we it comes down to setting null to a reference it is a bad idea, as references cannot be assigned the value of null. When you go to compile your program some good compilers will pick up on this, yet others will not and it can cause a crash of your program and even a corruption in your memory.

| Warning: Do Not Reference Objects with a Value of 0By setting a reference to an object that is equal to 0 you are setting it to null. This can corrupt the program the reference is in and even potentially damage your computer. |

## Passing By Reference

In the chapter on functions you learnt that values can be passed into functions from others as parameters. Then in the pointers chapter you discovered how this is done by using pointers. Now we are going to see how it done by using references. The syntax for this is as such:

| Someref(4,8);// parameters are referencedint SomeRef(&rFirstReference, &rSecondReference); |

When you pass by reference the effect is the same but instead of a copy being made, the actual value is passed through by a reference. Therefore, this demonstrates that you leap over the limitations functions have when passing by value. We know that when you pass by value all that is really happening is a copy of the value is being made and placed into the calling function.

In the C++ language passing by reference means to take the original value and pass – not copy – it into the function. There are two methods in which this can be accomplished – through pointers and references.

Listing 10.2 – Pass By Reference.cpp

| #include <iostream>using namespace std;int SomeReference(int &refOne, char &refTwo);int main(){   int x = 5;   char y = 'y';   SomeReference(x,y); // function call   cout << "\nThe new reference one: " << x << endl;   return 0;}int SomeReference(int &refOne, char &refTwo){   cout << "Reference one: " << refOne << endl;   cout << "Reference two: " << refTwo << endl;   refOne++; // increment refOne   return refOne;} |

Program Syntax: Pass By Reference.cpp

#### Passing References

This program takes two declared variables from main and passing them by reference into a function called SomeReference. In the function they are displayed and then refOne is incremented and passed back to main. Once in main, the new value of the variable is displayed to show how it is not been copied by delivered to and fro between the two functions.

## Pointers and References

In C++ pointers are objects too. This means that references can alias them. Although, as we have seen pointers can be deleted and then set to null, whereas references cannot be set as null, nor can they be reassigned. Below is an example of how a pointer can work with a reference.

Listing 10.3 – Pointers and References.cpp

| #include <iostream>using namespace std;int main(){   // variables, pointers and references   int target = 10;   int *pTargetPtr = new int;   *pTargetPtr = target;   Int &rTargetRef = *pTargetPtr;   cout << "Target: "  << target << endl;   cout << "Target pointer: " << *pTargetPtr << endl;   cout << "Target reference: " << rTargetRef << endl;   delete ptargetptr; // deletes pointer   pTargetPtr = 0; // pointer set to null   cout << "Target new reference: " << rtargetref << endl;   return 0;} |

Program Syntax: Pointers and Refernces.cpp

#### Delete Pointers

In the program, a pointer is deleted and its value is set to 0/NULL to show how references tackle the issue of giving references a value they cannot handle.

#### Pointing to References

This example shows a reference and pointer can work together. Once a pointer is created and assigned to a piece of data, a reference can then alias the pointer. This means that when either the variable, pointers or reference is altered, all of them follow suit.

It also shows what happens when a pointer is deleted and the reference is still the alias to it. Once the value is deleted from the pointer, the reference does not have any data – thus it is null – and because references cannot be null it diisplatys the memory address it is stored at or simply crashes the program.

## References Over Pointers

References have a better preference of use amongst many programmers, generally because they are the simpler method to use, compared to a pointer. However, as already talked about, references cannot be used in some circumstances – remember no null for references. Nor can they be reassigned without creating trouble in a program.

On the flip side of this, pointers are more effective and efficient in a program when they are used. As a beginner programmer, you should not neglect using pointers and replace them with references. It is always good programming practice to use both in your programs.

Chapter 11

# Arrays

What is an Array?

When we declare a variable it is done in the following method:

| <data_type>              <variable_name>;int               myNumbers; |

An array is a collection of created objects, which use the same data type and name. These collections have storage locations named elements, which are numbered from 0.  Depending on the number being called upon depends on what object the programmer wishes to use within the list of elements.

## The Elements Of An Array

The elements that you give your arrays can be accessed by referring to it by its number or an offset. The example below shows this.

| int myarray[X] // replace X with a number |

## Arrays Start at Zero

To a beginner of C++ or any programming language that ha arrays, it might be weird to discover that the computer counts from the value of 0\. Thus, this means that array elements begin at the value of 0 too. So, if you have an array like this theArray[5] then that means theArray has 6 values placed into it. Read below to see how this is done individually.

You can write an array in two ways. These two methods are written below beside each other.

| int myarray[0] = 73;int myarray[1] = 65;int myarray[2] = 28;int myarray[3] = 45;int myarray[4] = 89;int myarray[5] = 53;int myarray[5] = {73,65,28,45,89,53}; |

The two methods here create the exact same array no matter how it is written. The first method is used for when you wish to access a particular element of the array.

| cout <<”Array number: “ << myArray[3]; // displays the value of 45 |

The second method is by creating the whole array in one. This is great for declaring and/or defining the array.

| int myArray[5] = {73,65,28,45,89,53}; |

## Danger in Writing Passed an Arrays End

We've now talked about elements of an array and seen how each can hold a different data value. Yet, what happens when you have an array of 9 elements and discovered actually you want to write to the tenth element?

If you call myArray[10] when there are only really 9 elements in that array then you'll be writing passed the end of it and perhaps overwriting other data in the program.

The effect this can have is a corruption of the other data in your program. If you are lucky your program will simply crash and the compiler will indicate the problem. On the hand, however, you can progress in the program and discover that it isn't doing as you planned it out.

## Initialising Arrays

The method for declaring an array is by writing the data type you want followed by the name along with an open bracket. Before closing the brackets, a number must be entered in the brackets before closing them. The number denotes to the amount of array elements you wish the array to have.

Here is an example:

| short myArray[18]; |

The array example declares an array that contains 18 elements that be filled with data values. This means that the compiler will jump into action and request for the computer memory to reserve up enough of it for the array.

## Multidimensional Arrays

We have learnt that arrays are a collection of objects that can be accessed by your program through the use of their elements. These multidimensional arrays can be known as arrays that has arrays. Thus, multidimensional can have two or more sets of elements to each array.

| int myArray[5][7]; |

The way these work is by using the first element and working through the 5 elements first. Once this done the second element will increment by 1 and the first element will start over again.

The program below shows this and gives you an idea of why programmers may want to use multidimensional arrays.

## How Does Memory Work with the Array?

Just like when we talked about declaring variables and how they reserve memory to be allocated to, the same happens with arrays. Because when an array is declared with say 6 elements then the compiler springs into action and creates the space – if enough is available – to fit the array into. Even if the user of the program at the time does not use all of the array elements, they still need to be placed into memory.

For example, let us look at an array and it stores that in memory.

In this diagram you can see an array of 3 elements. The blue boxes represent the location of different memory addresses. This means that each array element is subjected to its own location in memory.

The first element is the first variable in memory and it stores the value of 23\. The second element is the next variable and stores the value of 24\. The last element and variable stores the value of 25\. Each of these values that are stored in different areas of memory will have alternative memory addresses that are ran by binary numbers.

Chapter 12

# Classes

## What Is A Type?

The simple answer to this question is to say a type is a category of something. The reasons for this is because in life everyone considers and judges things in types. For example, as you are learning C++, you can think of this as a type of programming language. Or another example is to say a television is a type of digital technology.

When writing programs using Object-Oriented Programming and classes, a programmer can create whatever type of something they require for the program. Once a type is created, it is stored in the computers RAM, just like a variable. Then using the types created, the programmer can adapt and flesh them out by installing functionality and power into the type.

The functionality and power that is capable of being placed in a type is constructed by the use of predefined C++ built-in types, like the int, float and bool data types.

If you have read book one of this series, you may remember the topic of program design cropped up in the first chapter. Don’t worry if you cannot remember. In the chapter, I said that every program is designed to solve a problem. One single problem. It doesn’t matter what the problem accounts to. You could build a program to track of a company’s stock or to manage your personal finances. Whatever the problem, no matter how big or complex it is, by employing types to create class objects it makes programming far easier when solving problems.

Types really are not new to you as an intermediate programmer of C++. If you already know how to utilize variables and constants in C++, then you are well along the road to understanding class types. However, if you are estrange to this concept, then stop reading this book, jump onto the Amazon/Kindle website and purchase the previous book in this series.

| Technical Talk: Class TypesWhen a class is created in C++ what is exactly happening is a blueprint of a user-defined data type is being formed. The type does not affect the data that resides inside the class, but it does determine the class name. With a class type created, a programmer can then manage a class to construct a user-defined object, but employing such things as data variables and method functions. |

## Creating a Class

In C++ classes are the primary layer of Object-Oriented Programming and use the capability of encapsulation to conceal data from any section of a program that is not required to know about it. In some respects they are an expanded concept of data structures, which were used in the C language. However, unlike classes in C++, structures do not have the ability to create functions inside themselves.

To create a class you must follow the class definition syntax, which starts with the keyword class and then its type. Afterwards, must like a function, the body of the class is enclosed in brackets ( { } ), which then ends with a semi-colon. The reason for the semi-colon at the end of the class and outside the brackets is due to the class definition being a complete statement.

For example, for a class called Human it would be defined in this way.

| class <class_name> {   // statements}; |

| class Human {}; |

An important not to make about the construction of classes is they are a single entity, in the case that they do not reside in functions, such as main, but instead are written before any function begins. In fact, classes, again like functions, are usually coded in header files. Later on, you shall learn about header files, but for now just code any class you create in the main .cpp file.

Listing 12.0 – A Straightforward Class.cpp

| #include <iostream>using namespace std;// creates a class type named Humanclass Human {// class data goes here};int main(){cout << "Hello Programmer!" << endl;return 0;} |

Program Syntax: A Straightforward Class.cpp

#### The Human Class Type

This program might bring you back to the early days of beginning to learn C++ with the Hello World! style of program. This program is only a blueprint that shall be worked on throughout the chapter to show how a class is built, from the barebones to having functionality.

Inside the program there is the beginning of a Human class type built, but has no functionality connected to it. To give it power and functionality data variables and method functions must be installed into the class.

## Data Variables & Method Functions in Classes

You have covered the basic blueprint of constructing the barebones of a class, by defining a new type and enclosing it inside curly brackets. This is similar to creating a normal function. Although, unlike a function, a class concludes with a semi-colon on the outside of the closing curly bracket.

Still, no class is complete whilst being void of functionality and power. To implement these crucial units into a class, data variables and method functions are required. Look at the previous example written out again, but this time with a method function and data variable.

| class Human {void GetName(); // method functionstring itsName; // class variable}; |

## Class Variables

You understand the concept of a variable by now. Inside a class variables are capable of being declared of any C++ built-in type. Since the class can construct an object, the variables are the pieces that piece the object together.

Taking an example of a Car object, the variables that a class might include offers life to the object so it operates in the correct format. With a Car object, some of the variables might read as:

| double Fuel;double milesDriven;int steeringDirection; |

If these class variables are employed, then when coding a class for a program, it might appear similar to the following:

| class Car {// class variablesdouble Fuel;double milesDriven;int steeringDirection;}; |

## Method Functions

Alike to class variables being just plain simple variables, yet implemented in a class, method functions are functions that are coded in a class. These method functions operate with class variables to give the class object its functionality and power.

A simple way to put this is if the class variables of a Car object are the data measurements that are handled in a program, then the method functions are the levers which operate the action of giving the class variables its data. Therefore, these method functions are pivotal to giving any created class object its power to be used.

| class Car {// method functionsvoid increaseFuel();void Accelerate();int calculateMiles();// class variablesdouble Fuel;double milesDriven;int steeringDirection;}; |

## Create a Class Object

A normal variable is created by writing out the data type and its user-defined name. The variable is capable of also being defined with a value. This routine is similar when creating a class object.

We have already spoken of a Human and Car class object that is employed in classes to operate with class variables and method functions. Now you might wonder what a class object exactly does.

For the majority of classes created in programs – there are some with Abstract Data Types that cannot have objects – an object is required to control and seize the functionality of the class.

To create a class object, much like a variable, the type of the class is required followed by the user-defined name of the object. Of course, as this is a statement in C++ a semi-colon concludes the line. For instance@

| Human programmer;Car fourDoor; |

In this snippet the Human class type has created an object called programmer and the Car type creates an object called fourDoor; Once an object is created, it can take on the role of using class variables and method functions from the class to operate effectively.

## Access Data from Classes

You have learnt how to build an object, but not how to use it in a C++ program. Class objects are built in a function, like main, and that is where they can be used. If you decide to build an object called Keyboard in a function called KeyPresses(…) then that object can operate only in that function.

With a class object in a program, you can start to use to access data from the said class that the object is generated from. The initial aspect that is required to access class data is to know the power of an operator called the scope resolution operator ( :: ). This operator is used to define a method function from a class using the type name of the class. For instance, in the case of the Keyboard class with the method function KeyPresses(…), it would look somewhat like:

| #include <iostream>using namespace std;class Keyboard {public:void Keypresses();};void Keyboard::Keypresses() // class type accesses method function{char key;cout << "Press A Key: ";cin >> key;cout << "The Key You Press Was: " <<  key << endl;}int main(){Keyboard Keys; // object createdKeys.Keypresses(); // Keys object accesses Keypresses method function} |

## Private & Public Accessor’s

When it comes to classes in C++ there are three types of accessor’s that are utilized to determine the scope of the data inside a class. In this part we are going to look at the two main ones that are usually employed in classes.

### Private

The private accessor is the default accessor for any class. When a class is built without any written accessor name, like private or public, then C++ defaults all the data to encapsulating it in a private accessor. This means that it is restricted to anything that is outside the class, like the main function.

| class Human {// no accessor name// accessor default is private} |

### Public

The second accessor in classes is the keyword public. The public accessor allows the method functions and class variables created under it to be accessed anywhere in the class scope. Unlike the private accessor, which needs a third party to access its data, anything can be accessed from the public accessor.

Listing 12.1 – Public and Private.cpp

| #include <iostream>#include <string>using namespace std;class Human {public:void GetName(string); // declaring public method functionprivate:string itsName; // declares private class variable};void Human::GetName(string name) // defining method function{    itsName = name;    cout << "My Name Is: " << itsName << endl;;}int main(){Human programmer; // creates a Human objectstring me; // local string variablecout << "Hello Programmer!" << endl;cout << "What Is Your Name: ";cin >> me;programmer.GetName(me); // object calls method functionreturn 0;} |

Program Syntax: Public and Private.cpp

#### Public

The public accessor is implemented to yield the method function GetName(...), which carries one parameter. That parameter is filled with the data from the string variable is main called me.

#### Private

As the private accessor data requires a method function, it yields a string variable called itsName, which is employed in the GetName(…) function to copy the data from the method function argument and then display it on screen.

## Constructor and Destructor

A constructor and destructor are the opposite ends of a candle where classes are concered. When a class is created by writing its type, i.e. Human or Car, with the curly brackets two method functions are created by default. These functions are hidden from the programmer, although they can be manually written out and employed in a program to do some great stuff.

### Constructor

A class constructor is a special method function that is created once an object is created from the class type. The constructor holds the same name as the class type, so it knows where to access once an object of that type is created. You do not have to define a constructor. The program shall do this for you when an object is created. However, this is not always a good thing as you might need to use a constructor, meaning you will have to declare one. It is normally a good thing then to create one, even if it isn't used.

In the case of the Human class, if you wished to define the constructor method function then you would write it as:

| Human::Human {    // do something} |

Listing 12.2 – Manual Constructor.cpp

| #include <iostream>using namespace std;class Human {public:void GetAge();private:int itsAge;}Human::Human() // called when Human object is created{cout << “You Are In The Human Constructor!” << endl;cout << “Now, We Are Leaping Out!” << endl;GetAge(); // calls method function}Human::GetAge() {itsAge = 21;cout << “What Is To Be “ << itsAge << “ again. Bliss!” << endl;}int main(){Human me; // object createdreturn 0;} |

Program Syntax: Manual Constructor.cpp

#### The Human Constructor

When the Human class type object is created, the program jumps into the Human constructor – Human::Human() – where is runs through a pair of cout commands and jumps into the method function GetAge().

This reveals that whenever a new class object is created or called, then the constructor to that object is active and runs through.

| Knowledge: No Constructor Return ValuesAny class constructor a program has does not have a return value. The reason for this is because it does not have a built in type like int or float or char. |

Chapter 12

# Inheritance

What is Inheritance?

Inheritance is the next stage in your Object-Oriented Programming training. Like a human being inherits features and attitudes from his/her mother and father, or a dog learns that it can bark and has an increased sense of hearing, so C++ uses its concept of inheritance to allow for a class called a derived class to inherit certain qualities from base case.

Let’s look at a diagram that focuses on two derived classes, one called Chicken and the other called Eagle, which derives from a base class called Bird.

As you can see most of the qualities that the Bird class has the Eagle picks up, although, a Chicken cannot fly which gives us the self-defined error message “A Chicken cannot fly”.

The way that C++ manages to represent these linked relationships is from having one class feeding off another for its data. Therefore, this basically means that a class can contribute its functionality to another class to be used separately. This is known as a class deriving from a base class.

## Derivation and Base

So that you know how inheritance works we are going to look at a derive and base classes and see examples of them. To do this we are going to ignore the Bird, Chicken and Eagle classes and look at a program that shows the wages of employees in a company.

When you derive from a base class the class must first be declared else the program will spit out a compile error.

Public and Protected – The Difference

As we are on the second stage of Object-Oriented Programming, we are going to look at the third and last accessor that can be added or even replace the private accessor of a class. The protected keyword is the one that sits in the middle of private and public.

Instead of locking data down or allowing an object to openly use it,  anything under the accessor heading of protected allows for any base class object and any derive class object to use the data.

Thus, if we go back to our bird, chicken and eagle example we can put in everything we want the base class to search in under the protected accessor. If a base class also has a private accessor along with a public accessor then anything underneath the private cannot be searched with derived classes.

## Constructor and Destructor

When a derived class constructor is called by a program it will first will call upon the base class constructor and then the derive constructor. Thus when it comes time to destroy the objects, the program must be told to destroy the derived class object and then the base class one. If it is not done in this way then your program can generate a memory leak, which we know from the chapter on pointers how ineffective that can be to your computer.

## Overriding Data Methods

Overriding data methods is the concept whereby a derived class with a data method equal in type, name and parameters as that in the base method can instead override the base method.

Look at the program below.

## Calling the Base Method

When the base method is overridden  it is still possible to call it from your program.  The method to do this is by writing the derived object and then putting the dot operator followed by the concealed base object and two objects with the method.

Eye.HumanBody::SetSight();

This will allow the HumanBody SetSight method to be called.

Chapter 14

# Polymorphism

## What is Polymorphism?

The notion behind polymorphism can be explained in a simply example. Let's take a 15 inch average television with free cable and teletext. You can use this in a simple example using classes and inheritance.

As all programming books will tell you, poly means more and morphisms means to alter something. This means that you can add more to an object by morphing it with another. So, let's first create a object for the television and also for the DVD.

| Television TV;DVD Player; |

Now with DVD inheriting from Television, you can create an DVD object and use the Television data method channels.

| Player = new *TelevisionPlayer->OnSwitch() |

## Virtual Methods

Now we are going to look at how virtual methods help decide a program whether to use an object from the base class or the derived class. You make a virtual method by prefixing it with the keyword virtual. When this is done virtual functions that are set in base classes are capable of being overridden by their derived class alternatives. If you use a pointer on a derived class and point it to a bass class that is virtual then the derive class can override the methods to use the derive methods. It does by looking up something called the qualified name lookup.

| virtual bool OnSwitch(); |

## Access Cost of Being Virtual

Nothing ever comes free in this world anymore, and the same goes for programming with C++ and handling memory. When an object is created and it employs the use of a virtual method there is a cost – an overhead – in the computers memory. This is where the programmer should make certain that he has created a constructor and destructor for the object/

One word to consider when creating a derived class, whose object will use polymorphism and virtual methods. This is to make sure that the class is being used for a proper reason, i.e. there is no point in creating a class that derives from another if the derive class is tiny. The example below is a bad example of a derived class along with a normal base class:

| class Player {    // a large number of methods and variables};class HealthPotion {    // only 1 method and 2 variables}; |

It is wise to perhaps rewrite the HealthPotion class and instead place it in a Potion class that is filled with others.

| class Potion {float HealthPotion();float ManaPotion();float HealthGain();float ManaGain();float smallHealthPotion;float largeHealthPotion();}; |

## Abstract Data Types

When you code programs utilising the use of classes, you may wish to create a primary class that stands as a hierarchy to other lower level classes. For example, if we took a main class called Food, then we can build a lower classes from it that are assigned to different types of foods.

| class Food {public:virtual Double CalorieAmount(int amount) = 0;virtual Double FatAmount(int amount) = 0;protected:double amount;};class Orange {public:virtual Double CalorieAmount(int amount);virtual Double FatAmount(int amount);protected:double amount;};class Chocolate {public:virtual Double CalorieAmount(int amount);virtual Double FatAmount(int amount) ;protected:double amount;}; |

As we can see, out of the three classes here, two of them derive from the Food class. Thus, this means that they are capable of accessing the functions in the higher class. However, in this example, the higher class has data methods that are pure virtual functions. They are this because at the end of the function declaration, they are made abstract by equalling to 0.

This means that the lower classes have to have there own virtual functions to work with.

| Warning: No abstract objectsWhen creating an abstract class, you are thereby telling the compiler that you cannot create an object of that class. Therefore the following code shall spit out an error.Food pie; // error as Food class is abstract |

However, even though no objects are allowed with abtract classes, you can create program pointers and references that direct to an abstract class. What is the point of this?

Well by referencing or pointing to an abstract class, it allows for run-time polymorphism.

Pure Virtual Function

The concept of pure virtual function is shown in C++ when a virtual function is given the value of 0\. Thus, by giving a virtual function the value of 0, you are making it pure and also it is not capable of being used. Pure Virtual Functions are created in classes that have a hierarchy of functions, For example, the Food class has a CalorieAmount() function and too has the Choclate class. However, the CalorieAmount() function in the Food class is only initialised as a pure virtual function and not used, although, it is used in the Chocolate class for a different purpose.

Encapsulation

Chapter 15

# Templates

What is a Template?

When initially developed, the concept of templates were never featured in C++. It took a couple years further from its release, when the C++03 was released.

Generic programming a term used when we talk about templates in C++. The reason due to this is because templates allow the programmer to create functions and class that operate in a generic type. These generic types can replace the normal types of a function or a variable. Therefore, it is possible to rename a type what you wish – avoiding C++ keywords – and have that type be used for different types of data.

First we need to know how to declare a template. A template declaration will go above the function or class heading.

| // syntax for templatestemplate <typename identifier_name> //uses typenametemplate <class identifier_name> // uses class |

Look at the simple class template example below. It shows how to use a template with a class and and a function variable inside the class.

| template<typename T>class Player{public:T CountLives(); // data method declared using generic type T from template typenameprivate:T Lives; // data variable declared using generic type T from template typename}; |

Within C++ there are actually two main types of templates, the function and class template.

Instances of a Template

Function Templates

Generic templates and much alike to normal functions. They are also known as template functions. It doesn’t matter what name you use for them, as they both mean the same thing. The difference between the two is that template functions can have arguments of different types. This means that through the function, a single argument can be used for different data types. Look below to see how a template is declared.

| Template<typename identifier_name> // templateType function_name(arguments) {//function statements} |

So, if we have two functions that are bool and int and we wish to replace them with a generic type from a template we could write them like this.

| Bool myBoolFunction();Int myIntegerFunction();Template <typename T> T myBoolFunction();Template <typename T> T myIntegerFunction() |

Above you can see the same two functions. One the left is the functions without being generically typed by a template. On the right, both of them have been generically typed. The letter T now acts as a data type for these functions. In the bool function it acts as a bool and in the int function it acts as a integer data type.

Noted that in the template declaration the generic type is passed in as a parameter: <typename T>. The T after the typename is only known as a placeholder that can be used to replace the data type of a function. The trick that C++ does is examines the function and from its return type it will decide to change the placeholder of T to whatever data type T has been put in place for. You can think of the typename T as a substitute for a data type when you are writing your code. You will see in the next chapter on the Standard Template Library that the vast amount of algorithms used in C++ are executed – or written – in the same manner no matter what the type is.

Note: You may have seen the function name on the same line as the template definition. Due to whitespace being void in C++ and the template not having a end-line terminator, i.e. a semi-colon, the function name does not have to be on the same line as the template. It just needs to come after the template declaration.

The two examples are correct:

| Template <typename T> void trialTemplate();Template <typename T>void trialTemplate(); |

In the second example, it is to be noted that you cannot have anything in between the template declaration and the function.

| template <typename T>string myTemplate = “My Template”;void trialTemplate(); |

## Templates of Two or More Generic Types

We have now learnt about template and how they help you make generic types for your functions. Now, we are going to look at how you can have different sets of generic types in one template.

By using the comma operator ‘,’ you can define two or more generic types inside a template to use inside a function template. For example, look at the template definition.

| template <typename T, typename Y>void myFunction(T temp1, Y temp2){cout << “Here are the typnames from the template: “ << temp1 << “ and “ << temp2 << “.\n”;}int main(){myFunction 50, “is the number fifty” );myFunction( true, 18.40f );return 0;} |

## The Magic Behind the Template

On the creation of a template what you are actually allowing the compiler to do is to create as many types of functions that is required for handling the instances of that function.

## Overloading a Generic Function

A generic function does have the ability to overload itself. Although, you can explicitly overload it, which is known as Explicit Specialization.  When a generic function is overloaded the function will override the generic function that is relative to the version in question.

Along with creating explicit overloaded versions of generic functions, it is also possible to create templates that are overloaded in their specifications. To achieve this all you need to do is create another template that is a basic copy of the previous, but it must differ in the size of parameters it has.

## Standard Parameters and Template Parameters

When creating a template you can mix generic types with normal data types like int or char. They are written the same as a parameter is in a function.

| template <class T>;void myFunction(T data, int boo); |

## Working with Generic Classes

Templates can also work with creating and defining generic classes. You write the template in the exactly the same way as you would for a generic function.

| template<class T>class Player {}; |

## Working with Class Objects

When you finally create a generic class, then you will need to put that generic type with your generic class object. The syntax for creating a generic class object is the following:

Class-name <generic type> object_name;

Chapter 16

# Header and Namespaces Files

Topics You Will Learn In This Chapter Includes

## What is a Namespace?

The subject of namespaces has been left late in this book. Although, there is nothing really complex about namespaces that makes programming them any more difficult than the information you have already read.

A namespace is like a box for a function or class, which seals its objects from confusion with other objects outside the namespace that have the same name.

Let me give you an example. Let’s imagine there is a fast-food franchise called Pizza Galore who are in two cities – New York and London – and they serve two types of pizza. One pizza is called the Meat Feast and the other is the Ham and Pineapple. #you can use the names of the cities as the name of our namespaces. They could be called:

| namespace PizzaGaloreNY;namespace PizzaGaloreLdn; |

With these two namespace you can help the program distinguish between the two types of pizza’s that each franchise makes depending on the city. Inside the namespace block, you can have classes or functions with the same name, but can have them do something different.

## Looking at a Namespace

You are going to look at both our namespaces and how we can get different results from each one of their functions.

In the following program, you take the two namespaces previous mentioned and use them to create two types of pizza with different prices (integer value) and a different source of cheese (string value).

Listing 16.0 – Pizza Namespace.cpp

| #include <iostream>using namespace std;namespace PizzaExpressNY { class NewYorkCompany {              public: void MeatFeastPrice(int);              private: int price;              };}namespace PizzaExpressLdn { class LondonCompany {              public: void MeatPrice(int);              private: int price;              };}void PizzaExpressNY::NewYorkCompany::MeatFeastPrice(int  price){cout << "The Price of the Meat Feast at Pizza Express New York is $" << price << endl;}void PizzaExpressLdn::LondonCompany::MeatPrice(int  price){cout << "The Price of the Meat Feast at Pizza Express London is £" << price << endl;}int main(){              PizzaExpressNY::NewYorkCompany NYC;              PizzaExpressLdn::LondonCompany LC;              NYC.MeatFeastPrice(20);              LC.MeatPrice(14);              return 0;} |

Programming Syntax: Pizza Namespace.cpp

#### The Namespaces

As you can see both namespaces have a class each that have a function and a variable of the same name. However, because they are under the different namespaces, the functions and variables act as separate origins.

## Namespaces Make for Good Programming

When writing programs, you can see why the concept of namespaces are a good thing. If you haven’t attempted the previous program, then attempt it and see how it works. They allow you to use the variable or a function in a different method.

| Warning: Duplication Outside namespacesDo not code your program with two or more classes/functions that have equal names, unless you use namespaces to separate them. |

It is normally good programming to store your written namespaces into header files along with class and functions, and then include the header file into the main .cpp file. Later on we will create a header file with a namespace and reveal the difference in how they are included into a .cpp file.

By storing namespaces in different header files you are helping your program to stay clean and not have one file with rows of code that will make it look cluttered. Every header file and every .cpp file should have one purpose.

For instance you could have a header file with a class Player that tells you everything about the Player of a game, from its lives, health, right down to the keys that move it.

## What is a Header File?

As already discussed, and perhaps if you have one of the IDE’s that I stated at the beginning of this book, you might have already seen that the .cpp files are not the only files that can be developed in C++. Inside a header file, you’ll find declarations of variables and functions that are implemented in classes.

## Including Header Files

You include a header file by using the # sign with the word include attached to it, followed by the name of the header file tied in <> brackets. For example:

| # include <iostream>#include <ctime>#include <Windows> |

The header files you have seen so far in this book, are files that are built in to C++, meaning that they are included by using the <> brackets around their name.

However, when you write your own header file, which has the same extension of .h you have to write the header file in a slightly different way. Instead of using the <> brackets between the header file, you replace the <> with double quotes. For example:

| #include “PizzaCompany.h”#include “Player.h”#include “Budget.h” |

As you can see the difference in the “ “ to the <>, one other aspect of including your own or a user-written header file is to add the .h extension to the end.

## Create Namespaces in Header Files

When creating namespaces, a quality of good programming grammar is to place user-defined namespaces in header files and not main C++ files (.cpp). A beneficial reason for this is because you do not want main programming files bogged down with dozens of coded lines representing one or more namespaces. Remember, alongside namespaces, classes and some functions (especially data members tied to classes), are inputted into header files. By representing data of this type in a header file, the single thing that is required for a program to utilize the declarations is to #include the header file. Here is an example of a user-defined header file.

| #include"inProgram.h" |

## Create Multiple Header Files

Programs are normally large with multiple different files created. Whether these files are .exe (executable), .dll (dynamic link-library) or another type, these files are constructed by dozens upon dozens of source and header files.

## Time to Test Yourself

The following questions are concerning the programming concepts you have learned in this chapter. Attempt these questions before you moving on.

| Test Yourself 
1.  Can you explain the concept of a header file?
2.  Can you explain what a namespace is employed for?
3.  What keyword is employed to include a header file?
4.  What benefits are there to having namespaces included in header files?

 |

# Last Words

Thank you for reading this book. Can you please leave a review on your preferred Amazon site of this book?

Thank you

Alexander Harrison

Contents

[Introduction](#part0000.xhtml__Toc407645502)

[Ready for C++ Programming?](#part0000.xhtml__Toc407645503)

[What You’ll Learn in this Book](#part0000.xhtml__Toc407645504)

[How this Book is Laid Out](#part0000.xhtml__Toc407645505)

[Conventions and Practices](#part0000.xhtml__Toc407645506)

[C++ Program Design](#part0000.xhtml__Toc407645507)

[Program and Design Software](#part0000.xhtml__Toc407645508)

[Two Hour Pen and Paper Brainstorm Method](#part0000.xhtml__Toc407645509)

[Why Should I Design Programs Before Writing Code?](#part0000.xhtml__Toc407645510)

[Question the Programs Purpose](#part0000.xhtml__Toc407645511)

[Steps to a Program Design Blueprint](#part0000.xhtml__Toc407645512)

[Step 1: Define the Problem You Wish to Solve](#part0000.xhtml__Toc407645513)

[Step 2: Define what is involved in solving the Problem](#part0000.xhtml__Toc407645514)

[Step 3: Define a List of Events Involved in the Problem](#part0000.xhtml__Toc407645515)

[Reuse Program Code](#part0000.xhtml__Toc407645516)

[Select a Compiler](#part0000.xhtml__Toc407645517)

[No Compiler? Don’t Worry!](#part0000.xhtml__Toc407645518)

[Code::Blocks 13.12](#part0000.xhtml__Toc407645519)

[Dev-C++](#part0000.xhtml__Toc407645520)

[The Program Development Cycle](#part0000.xhtml__Toc407645521)

[Your First C++ Program](#part0000.xhtml__Toc407645522)

[Programming Errors](#part0000.xhtml__Toc407645523)

[Compiler Errors](#part0000.xhtml__Toc407645524)

[Link Errors](#part0000.xhtml__Toc407645525)

[Run-Time Errors](#part0000.xhtml__Toc407645526)

[A Compile Error Program](#part0000.xhtml__Toc407645527)

[Time to Test Yourself](#part0000.xhtml__Toc407645528)

[Anatomy of a Program](#part0000.xhtml__Toc407645529)

[Examining Hello Programmer](#part0000.xhtml__Toc407645530)

[Include the Pre-Processor](#part0000.xhtml__Toc407645531)

[Header Files](#part0000.xhtml__Toc407645532)

[Comments](#part0000.xhtml__Toc407645533)

[Namespaces](#part0000.xhtml__Toc407645534)

[Function Blocks](#part0000.xhtml__Toc407645535)

[Whitespace](#part0000.xhtml__Toc407645536)

[The Next Stage](#part0000.xhtml__Toc407645537)

[Time to Test Yourself](#part0000.xhtml__Toc407645538)

[Data Storage, Variables & Constants](#part0000.xhtml__Toc407645539)

[What is a Variable?](#part0000.xhtml__Toc407645540)

[What is Random Access Memory?](#part0000.xhtml__Toc407645541)

[Bits and Bytes](#part0000.xhtml__Toc407645542)

[Dynamic and Static Typed Languages](#part0000.xhtml__Toc407645543)

[Dynamic Typed Language](#part0000.xhtml__Toc407645544)

[Static Typed Language](#part0000.xhtml__Toc407645545)

[C++ is a Static Typed Language](#part0000.xhtml__Toc407645546)

[Learn the Data Types](#part0000.xhtml__Toc407645547)

[Declare Variables](#part0000.xhtml__Toc407645548)

[Define Variables](#part0000.xhtml__Toc407645549)

[Signed and Unsigned Variables](#part0000.xhtml__Toc407645550)

[Unsigned](#part0000.xhtml__Toc407645551)

[Signed](#part0000.xhtml__Toc407645552)

[The Different Data Types](#part0000.xhtml__Toc407645553)

[Integers](#part0000.xhtml__Toc407645554)

[Short Integers](#part0000.xhtml__Toc407645555)

[Long Integers](#part0000.xhtml__Toc407645556)

[Float](#part0000.xhtml__Toc407645557)

[Double](#part0000.xhtml__Toc407645558)

[Char](#part0000.xhtml__Toc407645559)

[Boolean and String Variables](#part0000.xhtml__Toc407645560)

[Bool](#part0000.xhtml__Toc407645561)

[String](#part0000.xhtml__Toc407645562)

[Creating Multiple Variables](#part0000.xhtml__Toc407645563)

[Place Variables in Memory](#part0000.xhtml__Toc407645564)

[Manipulate Data Type Names](#part0000.xhtml__Toc407645565)

[Using static_cast](#part0000.xhtml__Toc407645566)

[What are Constants?](#part0000.xhtml__Toc407645567)

[Types of Constants](#part0000.xhtml__Toc407645568)

[Literal](#part0000.xhtml__Toc407645569)

[Symbolic](#part0000.xhtml__Toc407645570)

[Enumerated](#part0000.xhtml__Toc407645571)

[Time to Test Yourself](#part0000.xhtml__Toc407645572)

[Basic Operators](#part0000.xhtml__Toc407645573)

[What is an Operator?](#part0000.xhtml__Toc407645574)

[Mathematical Operators](#part0000.xhtml__Toc407645575)

[Problems with Division and Integers](#part0000.xhtml__Toc407645576)

[Mix Assignment Operator with Math Operators](#part0000.xhtml__Toc407645577)

[Increment and Decrement](#part0000.xhtml__Toc407645578)

[Pre- and Postfix Operators](#part0000.xhtml__Toc407645579)

[Operators and Precedence](#part0000.xhtml__Toc407645580)

[Time to Test Yourself](#part0000.xhtml__Toc407645581)

[Statements and Expressions](#part0000.xhtml__Toc407645582)

[Statements](#part0000.xhtml__Toc407645583)

[Compound Statements](#part0000.xhtml__Toc407645584)

[Expressions](#part0000.xhtml__Toc407645585)

[Make Decisions in Programs](#part0000.xhtml__Toc407645586)

[The if Statement](#part0000.xhtml__Toc407645587)

[The if else Statement](#part0000.xhtml__Toc407645588)

[Nested Statements](#part0000.xhtml__Toc407645589)

[The switch Statement](#part0000.xhtml__Toc407645590)

[Mixing Statements](#part0000.xhtml__Toc407645591)

[Time to Test Yourself](#part0000.xhtml__Toc407645592)

[Functions](#part0000.xhtml__Toc407645593)

[What is a Function?](#part0000.xhtml__Toc407645594)

[Creating a Function](#part0000.xhtml__Toc407645595)

[Declare a Function](#part0000.xhtml__Toc407645596)

[Define a Function](#part0000.xhtml__Toc407645597)

[No Prototype Function](#part0000.xhtml__Toc407645598)

[Working in Scopes](#part0000.xhtml__Toc407645599)

[Global Data](#part0000.xhtml__Toc407645600)

[Local Data](#part0000.xhtml__Toc407645601)

[Parameters and Arguments](#part0000.xhtml__Toc407645602)

[Calling Functions](#part0000.xhtml__Toc407645603)

[Return Values](#part0000.xhtml__Toc407645604)

[Writing Return Statements](#part0000.xhtml__Toc407645605)

[Multiple Return Values](#part0000.xhtml__Toc407645606)

[The void Function Type](#part0000.xhtml__Toc407645607)

[Overloaded Functions](#part0000.xhtml__Toc407645608)

[Inline Functions](#part0000.xhtml__Toc407645609)

[Computer Memory and the Stack](#part0000.xhtml__Toc407645610)

[Time to Test Yourself](#part0000.xhtml__Toc407645611)

[Extra Operators](#part0000.xhtml__Toc407645612)

[Logical and Relational Operator Types](#part0000.xhtml__Toc407645613)

[Relational Operators](#part0000.xhtml__Toc407645614)

[Equal To](#part0000.xhtml__Toc407645615)

[Greater Than](#part0000.xhtml__Toc407645616)

[Less Then](#part0000.xhtml__Toc407645617)

[Greater Than or Equal To](#part0000.xhtml__Toc407645618)

[Less Than or Equal To](#part0000.xhtml__Toc407645619)

[Not Equal To](#part0000.xhtml__Toc407645620)

[Logical Operators](#part0000.xhtml__Toc407645621)

[AND (&&)](#part0000.xhtml__Toc407645622)

[OR (||)](#part0000.xhtml__Toc407645623)

[NOT (!)](#part0000.xhtml__Toc407645624)

[Loops](#part0000.xhtml__Toc407645625)

[Programming Loops](#part0000.xhtml__Toc407645626)

[The while Loop](#part0000.xhtml__Toc407645627)

[The do while Loop](#part0000.xhtml__Toc407645628)

[The for Loop](#part0000.xhtml__Toc407645629)

[Nested Loops and Statements](#part0000.xhtml__Toc407645630)

[Pointers](#part0000.xhtml__Toc407645631)

[What is a Pointer?](#part0000.xhtml__Toc407645632)

[Understanding Pointers](#part0000.xhtml__Toc407645633)

[Memory Addresses](#part0000.xhtml__Toc407645634)

[The Dereference Operator](#part0000.xhtml__Toc407645635)

[Dynamic Memory](#part0000.xhtml__Toc407645636)

[new](#part0000.xhtml__Toc407645637)

[delete](#part0000.xhtml__Toc407645638)

[References](#part0000.xhtml__Toc407645639)

[What is aReference?](#part0000.xhtml__Toc407645640)

[Create a Reference](#part0000.xhtml__Toc407645641)

[The Address of Operator for References](#part0000.xhtml__Toc407645642)

[What Objects Can Referenced?](#part0000.xhtml__Toc407645643)

[Keep One Reference for One Object](#part0000.xhtml__Toc407645644)

[NULL Unused Pointers](#part0000.xhtml__Toc407645645)

[Do Not NULL References](#part0000.xhtml__Toc407645646)

[Passing By Reference](#part0000.xhtml__Toc407645647)

[Pointers and References](#part0000.xhtml__Toc407645648)

[References Over Pointers](#part0000.xhtml__Toc407645649)

[Arrays](#part0000.xhtml__Toc407645650)

[What is an Array](#part0000.xhtml__Toc407645651)

[The Elements Of An Array](#part0000.xhtml__Toc407645652)

[Arrays Start at Zero](#part0000.xhtml__Toc407645653)

[Danger in Writing Passed an Arrays End](#part0000.xhtml__Toc407645654)

[Initialising Arrays](#part0000.xhtml__Toc407645655)

[Multidimensional Arrays](#part0000.xhtml__Toc407645656)

[How Does Memory Work with the Array?](#part0000.xhtml__Toc407645657)

[Classes](#part0000.xhtml__Toc407645658)

[What Is A Type?](#part0000.xhtml__Toc407645659)

[Creating a Class](#part0000.xhtml__Toc407645660)

[Data Variables & Method Functions in Classes](#part0000.xhtml__Toc407645661)

[Class Variables](#part0000.xhtml__Toc407645662)

[Method Functions](#part0000.xhtml__Toc407645663)

[Create a Class Object](#part0000.xhtml__Toc407645664)

[Access Data from Classes](#part0000.xhtml__Toc407645665)

[Private & Public Accessor’s](#part0000.xhtml__Toc407645666)

[Private](#part0000.xhtml__Toc407645667)

[Public](#part0000.xhtml__Toc407645668)

[Constructor and Destructor](#part0000.xhtml__Toc407645669)

[Constructor](#part0000.xhtml__Toc407645670)

[Inheritance](#part0000.xhtml__Toc407645671)

[What is Inheritance](#part0000.xhtml__Toc407645672)

[Derivation and Base](#part0000.xhtml__Toc407645673)

[Constructor and Destructor](#part0000.xhtml__Toc407645674)

[Overriding Data Methods](#part0000.xhtml__Toc407645675)

[Calling the Base Method](#part0000.xhtml__Toc407645676)

[Polymorphism](#part0000.xhtml__Toc407645677)

[What is Polymorphism?](#part0000.xhtml__Toc407645678)

[Virtual Methods](#part0000.xhtml__Toc407645679)

[Access Cost of Being Virtual](#part0000.xhtml__Toc407645680)

[Abstract Data Types](#part0000.xhtml__Toc407645681)

[Templates](#part0000.xhtml__Toc407645682)

[Templates of Two or More Generic Types](#part0000.xhtml__Toc407645683)

[The Magic Behind the Template](#part0000.xhtml__Toc407645684)

[Overloading a Generic Function](#part0000.xhtml__Toc407645685)

[Standard Parameters and Template Parameters](#part0000.xhtml__Toc407645686)

[Working with Generic Classes](#part0000.xhtml__Toc407645687)

[Working with Class Objects](#part0000.xhtml__Toc407645688)

[Header and Namespaces Files](#part0000.xhtml__Toc407645689)

[What is a Namespace?](#part0000.xhtml__Toc407645690)

[Looking at a Namespace](#part0000.xhtml__Toc407645691)

[Namespaces Make for Good Programming](#part0000.xhtml__Toc407645692)

[What is a Header File?](#part0000.xhtml__Toc407645693)

[Including Header Files](#part0000.xhtml__Toc407645694)

[Create Namespaces in Header Files](#part0000.xhtml__Toc407645695)

[Create Multiple Header Files](#part0000.xhtml__Toc407645696)

[Time to Test Yourself](#part0000.xhtml__Toc407645697)

[Last Words](#part0000.xhtml__Toc407645698)

Acknowledgements

Thank you Jason and Joanne, for the support offered while I wrote, and for simplifying particular tricky jargon.