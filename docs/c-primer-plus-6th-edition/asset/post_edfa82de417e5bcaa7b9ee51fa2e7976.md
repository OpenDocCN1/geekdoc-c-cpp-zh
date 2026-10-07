
# Introduction

## The Primer Approach

C++ Primer Plus brings several virtues to the task of presenting all this material. It builds on the tradition begun by C Primer Plus nearly two decades ago and embraces its successful philosophy:

- A primer should be an easy-to-use, friendly guide.
- A primer doesn't assume that you are already familiar with all relevant programming concepts.
- A primer emphasizes hands-on learning with brief, easily typed examples that develop your understanding, a concept or two at a time.
- A primer clarifies concepts with illustrations.
- A primer provides questions and exercises to let you test your understanding, making the book suitable for self-learning or for the classroom.

Following these principles, the book helps you understand this rich language and how to use it. For example:

- It provides conceptual guidance about how to use particular features, such as using public inheritance to model what are known as is-a relationships.
- It illustrates C++ programming idioms and techniques.
- It provides a variety of sidebars, including tips, cautions, and notes.

The author and editors of this book do our best to keep the presentation to-the-point, simple, and fun. Our goal is that by the end of the book, you'll be able to write solid, effective programs and enjoy doing so.

## Sample Code Used in This Book

This book provides an abundance of sample code, most of it in the form of complete programs. Like the previous editions, this book brings generic C++ so that it is not tied to any particular kind of computer, operating system, or compiler. The examples were tested on a Windows 7 system, a Macintosh OS system, and a Linux system. Those programs using C++11 features require compilers supporting those features, but the remaining programs should work with any C++99/03-compliant system.

The sample code for the complete programs described in this book is available on this book's website. See the registration link given on the back cover for more information.

## How This Book Is Organized

This book is divided into 18 chapters and 10 appendixes, summarized here:

- Chapter 1: Getting Started with C++—Chapter 1 relates how Bjarne Stroustrup created the C++ programming language by adding object-oriented programming kinds of the C language. You'll learn the distinctions between procedural languages, such as C, and object-oriented languages, as C++. You'll learn about the joint ANSI/ISO work to develop a C++ standard. This chapter discusses the mechanics of creating a C++ program, outlining the approach for several current C++ compilers. Finally, it describes the conventions used in this book.

- Chapter 2: Setting Out to C++—Chapter 2 guides you through the process of creating simple C++ programs. You'll learn about the role of the main() function and some of the kinds of statements that C++ programs use. You'll use the predefined cout and cin objects for program output and you'll learn about creating and using variables. Finally, you'll be introduced to functions, C++ programming modules.

- Chapter 3: Dealing with Data—C++ provides built-in types for storing two kinds of data: integers (numbers with no fractional parts) and floating-point numbers (with fractional parts). To meet the diverse requirements of programs, C++ offers several types in each category: Chapter 3 discusses those types, including variables and writing constructs of various types. You'll also learn how C++ handles implicit and explicit conversions from one type to another.

- Chapter 4: Compound Types—C++ lets you construct more elaborate types from the basic unit types. The most advanced form is the class, discussed in Chapters 9 through 13. Chapter 4 discusses other forms, including arrays, which hold several values of a single type; structures, which hold several values of unlike; pointers, which identify locations in memory. You'll learn how to create and store strings and to handle I/O by C-style arrays and the C++ string class. Finally, you'll learn about the ways C++ handles memory allocation, using the new and delete operators for managing memory explicitly.

- Chapter 5: Loops and Relational Expressions—Programs often perform repetitive actions, and C++ provides three looping structures for purpose: the for loop, the while loop, and the do-while loop. Such loops must know when they should terminate, and the C++ relational operators enable you to create tests to guide such loops. In Chapter 5 you learn how to create loops that read and process input multidimensional arrays and how to use nested loops to process them.

- Chapter 6: Branching Statements and Logical Operators—Programs can behave intelligently if they can tailor their behavior to circumstances. In Chapter 6 you'll learn how to control program flow using the if, else, and switch-statements and the conditional operator. You'll learn how to use logical operators to help express decision-making tests. Also, you'll meet the ctype library of functions for evaluating character relations, such as testing whether a character is a digit or a nonprinting character. Finally, you'll get an introductory view of file I/O.

- Chapter 7: Functions: C++ Programming Modules—Functions are the basic building blocks of C++ programming. Chapter 7 concentrates on features that C++ functions share with C functions. In particular, you will review the general format of function definition and examine how function prototypes increase the reliability of programs. Also, you will investigate how to write functions for arrays, character strings, and structures. Next, you will learn about recursion, which is when a function calls itself, and how it can be used to implement a divide-and-conquer strategy. Finally, you will meet pointers to functions, which enable you to use a function to tell one function to use a specific function.

- Chapter 8: Adventures in Functions—Chapter 8 explores the new features C++ adds to functions. You will learn about inline functions, which can speed program execution at the cost of additional program size. You will work with reference arguments, which provide an alternative way to pass information to functions. Default arguments let you omit supply values for function arguments that define the same name but different arguments. All these features have frequent use in class design. You will also learn about templates, which allow you to specify the design of a family of related functions.

- Chapter 9: Memory Models and Namespaces—Chapter 9 discusses putting together multifile programs. It examines the choices in allocating memory, looking at different methods of managing memory and at scope, linkage, and namespaces, which determine what parts of a program know about a variable.

- Chapter 10: Objects and Classes—A class is a user-defined type, and an object (such as a variable) is an instance of a class. Chapter 10 introduces object-oriented programming and class design. A class declaration describes the information stored in a class object and the operations (class methods) allowed for class objects. Some parts of an object are visible to the outside world (the public portion), and some are hidden (the private portion). Special class methods (constructors and destructors) come into play when objects are created and destroyed. You will learn about all this and other class details in this chapter, and you will see how classes can be used to implement ADTs, such as a stack.

- Chapter 11: Working with Classes—Chapter 11 will further your understanding of classes. First, you will learn about operator overloading, which lets you define how operators such as + work with class objects. You will learn about friend functions, which can access class data that is inaccessible to the world at large. You will see certain constructors and overloaded operator member functions can be used to manage conversion to and from class types.

- Chapter 12: Classes and Dynamic Memory Allocation—Often it is useful to have a class member point to dynamically allocated memory. If you use new in a class constructor to allocate dynamic memory, you will incur the responsibilities of providing an appropriate destructor, of defining an explicit copy constructor, and
