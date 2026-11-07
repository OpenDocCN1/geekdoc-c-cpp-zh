
- Functions remove and replace ........................................ 1295
- Functions search, sort, and binary_search .................... 1297

## APPENDIX I: ANSWERS TO ODD-NUMBERED EXERCISES ................................ 1301

- Chapter 1 .................................................................... 1301
- Chapter 2 .................................................................... 1304
- Chapter 3 .................................................................... 1306
- Chapter 4 .................................................................... 1307
- Chapter 5 .................................................................... 1309
- Chapter 6 .................................................................... 1311
- Chapter 7 .................................................................... 1312
- Chapter 8 .................................................................... 1313
- Chapter 9 .................................................................... 1314
- Chapter 10 .................................................................. 1316
- Chapter 11 .................................................................. 1317
- Chapter 12 .................................................................. 1318
- Chapter 13 .................................................................. 1321
- Chapter 14 .................................................................. 1322
- Chapter 15 .................................................................. 1323
- Chapter 16 .................................................................. 1324
- Chapter 17 .................................................................. 1325
- Chapter 18 .................................................................. 1326
- Chapter 19 .................................................................. 1327

## INDEX ........................................................................ 1331

![](img/1fbe55537254baeb2b5b7dbaf64956ae_27_0.png)

## PREFACE

Welcome to the Fifth Edition of *C++ Programming: From Problem Analysis to Program Design*. Designed for a first Computer Science (CS1) C++ course, this text provides a breath of fresh air to you and your students. The CS1 course serves as the cornerstone of the Computer Science curriculum. My primary goal is to motivate and excite all CS1 students, regardless of their level. Motivation breeds excitement for learning. Motivation and excitement are critical factors that lead to the success of the programming student. This text is a culmination and development of my classroom notes throughout more than fifty semesters of teaching successful programming to Computer Science students.

> **Warning:** This text can be expected to create a serious reduction in the demand for programming help during your office hours. Other side effects include significantly diminished student dependency on others while learning to program.

*C++ Programming: From Problem Analysis to Program Design* started as a collection of brief examples, exercises, and lengthy programming examples to supplement the books that were in use at our university. It soon turned into a collection large enough to develop into a text. *The approach taken in this book is, in fact, driven by the students’ demand for clarity and readability.* The material was written and rewritten until the students felt comfortable with it. Most of the examples in this book resulted from student interaction in the classroom.

As with any profession, practice is essential. Cooking students practice their recipes. Budding violinists practice their scales. New programmers must practice solving problems and writing code. This is not a C++ cookbook. We do not simply list the C++ syntax followed by an example; we dissect the “why” behind all the concepts. The crucial question of “why?” is answered for every topic when first introduced. This technique offers a bridge to learning C++. Students must understand the “why?” in order to be motivated to learn.

Traditionally, a C++ programming neophyte needed a working knowledge of another programming language. This book assumes no prior programming experience. However, some adequate mathematics background, such as college algebra, is required.

### Changes in the Fifth Edition

The fifth edition contains more than 50 new programming exercises, and more than 150 new exercises. Each of the Chapters 2 to 7 include a programming exercise which contains a solution of a problem, however, the statements are in the incorrect order. So the student is asked to rewrite the program with statements in the correct order. This will allow the students to learn how to read and debug programs written by someone else. Another major change in this edition is the inclusion of debugging sections in the chapters 2 to 7. In these sections, a program with errors is included. The program is compiled and syntax errors, if any, are shown. We then show how to interpret the syntax errors and correct them. Some sections also show how to find and correct logical errors. This edition also includes various new examples, such as Examples 5–8, 7–8, 12–6, and 12–8. Various sections of Chapters 4, 5, 6, and 7 have been rewritten. Chapter 8 includes additional string functions, and the virtual functions section of Chapter 14 is rewritten with new examples.

### Approach

The programming language C++, which evolved from C, is no longer considered an industry-only language. Numerous colleges and universities use C++ for their first programming language course. C++ is a combination of structured programming and object-oriented programming, and this book addresses both types.

This book can be easily divided into two parts: structured programming and object-oriented programming. The first 11 chapters form the structured programming part; Chapters 12 through 19 form the object-oriented part. However, only the first seven chapters are essential to move on to the object-oriented portion.

In July 1998, ANSI/ISO Standard C++ was officially approved. This book focuses on ANSI/ISO Standard C++. Even though the syntax of Standard C++ and ANSI/ISO Standard C++ is very similar, Chapter 8 discusses some of the features of ANSI/ISO Standard C++ that are not available in Standard C++.

Chapter 1 briefly reviews the history of computers and programming languages. The reader can quickly skim through this chapter and become familiar with some of the hardware components and the software parts of the computer. This chapter contains a section on processing a C++ program. This chapter also describes structured and object-oriented programming.

Chapter 2 discusses the basic elements of C++. After completing this chapter, students become familiar with the basics of C++ and are ready to write programs that are complicated enough to do some computations. Input/output is fundamental to any programming language. It is introduced early in Chapter 3, and is covered in detail.

Chapters 4 and 5 introduce control structures to alter the sequential flow of execution. Chapters 6 and 7 study user-defined functions. It is recommended that readers with no prior programming background spend extra time on Chapters 6 and 7. Several examples are provided to help readers understand the concepts of parameter passing and the scope of an identifier.

Chapter 8 discusses the user-defined simple data type (enumeration type), the namespace mechanism of ANSI/ISO Standard C++, and the string type. The earlier versions of C did not include the enumeration type. Enumeration types have very limited use; their main purpose is to make the program readable. This book is organized such that readers can skip the section on enumeration types during the first reading without experiencing any discontinuity, and then later go through this section.

Chapter 9 discusses arrays in detail. Chapter 10 describes various searching and sorting algorithms as well as an introduction to the vector class. Chapter 11 introduces records (structs). The introduction of structs in this book is similar to C structs. This chapter is optional; it is not a prerequisite for any of the remaining chapters.

Chapter 12 begins the study of object-oriented programming (OOP) and introduces classes. The first half of this chapter shows how classes are defined and used in a program. The second half of the chapter introduces abstract data types (ADTs). This chapter shows how classes in C++ are a natural way to implement ADTs. Chapter 13 continues with the fundamentals of object-oriented design (OOD) and OOP and discusses inheritance and composition. It explains how classes in C++ provide a natural mechanism for OOD and how C++ supports OOP. Chapter 13 also discusses how to find the objects in a given problem.

Chapter 14 studies pointers in detail. After introducing pointers and how to use them in a program, this chapter highlights the peculiarities of classes with pointer data members and how to avoid them. Moreover, this chapter also discusses how to create and work with dynamic two-dimensional arrays. Chapter 14 also discusses abstract classes and a type of polymorphism accomplished via virtual functions.

Chapter 15 continues the study of OOD and OOP. In particular, it studies polymorphism in C++. The chapter specifically discusses two types of polymorphism—overloading and templates.

Chapter 16 discusses exception handling in detail. Chapter 17 introduces and discusses recursion. Moreover, this is a standalone chapter, so it can be studied anytime after Chapter 10.

Chapters 18 and 19 are devoted to the study of data structures. Discussed in detail are linked lists in Chapter 18 and stacks and queues in Chapter 19. The programming code developed in these chapters is generic. These chapters effectively use the fundamentals of OOD.

Appendix A lists the reserved words in C++. Appendix B shows the precedence and associativity of the C++ operators. Appendix C lists the ASCII (American Standard Code for Information Interchange) and EBCDIC (Extended Binary Coded Decimal Interchange Code) character sets. Appendix D lists the C++ operators that can be overloaded.

Appendix E has three objectives. First, we discuss how to convert a number from decimal to binary and binary to decimal. We then discuss binary and random access files in detail. Finally, we describe the naming conventions of the header files in both ANSI/ISO Standard C++ and Standard C++. Appendix F discusses some of the most widely used library routines, and includes the names of the standard C++ header files. The programs in Appendix G show how to print the memory size for the built-in data types on your system as well as how to use a random number generator. Appendix H gives an introduction to
