
bits the mantissa. In computers that have fixed word length, the proportion of bits for exponents and bits for the mantissa should be appropriate. However, if we want to satisfy requirements both in range and precision, we usually use a double word or even more words to store a floating-point number.

## 1.4.7 Representation of Non-numerical Information

In computers, non-numerical information is also encoded 0 and 1. Here we will focus on the coding schemes for Chinese and Western characters.

The most popular coding scheme for western characters is “American Standard Code for Information Interchange”, shortened as ASCII code. It includes 10 numbers, 95 printable characters including upper and lower English characters and 33 control characters. ASCII code uses 7 bits of a byte to represent a character and can represent most 2¹⁸ characters.

Since ASCII code does not use the most significant bit in a byte, many systems use this as the check bit to improve the transmission reliability.

Aside from ASCII, there is another code called EBCDIC (Extended Binary Decimal Interchange code), which uses 8 bits to represent a character. EBCDIC can then represent most 256 characters.

So how can we represent Chinese characters in computers? There are many Chinese characters (at least thousands of ordinary characters) compared to English characters, and obviously one (of eight digits) is far from enough. Now we have two-byte, three-byte or even four-byte code schemes for Chinese characters and the most popular is “Chinese Standard Code for Information Interchange”(GB2312-80), shortened as GB code. GB code is a two-byte code scheme, and it uses seven bits of each byte to encode a Chinese character.

Chinese coding and Western coding coexists in a computer. How to distinguish them is important, because different types of information have different process modes. One method is to set the most significant bits in each pair of bytes in GB2312-80 as “1”, while keeping the most significant bit in each byte in ASCII code as “0”. Then software (or hardware) can distinguish them.

## 1.5 The Development Process of Programs

Before we start learning programming, let's get a basic understanding of the development process of a program and learn some elementary terms. In the following chapters, readers may gain a deeper comprehension of the knowledge.

### 1.5.1 Elementary Terms

 **Source program:** program written in source language and needing to be translated. It can be an assembler language or high-level programming language (such as C++).

- **Object program:** program translated from source program. It can be represented by machine instructions (thus it is also called 'object code'), assembly instructions, or other intermediate languages.

- **Translator:** program that translates a source program into its equivalent object program. To a translator, source program is the input and object program is the output. There are three kinds of translators: assembler, compiler, and interpreter.

- **Assembler:** assembler translates a source program written in assembly language into the object program formed by machine instructions. Thus, the source program written in assembly language should be processed by the assembler to turn into the equivalent object program.

- **Compiler:** translate a source program written in high-level programming language into the object program. If the object program consists of assembly instructions, it still needs to run the assembler to translate them into machine instructions.

- **Interpreter:** another translator that translates source program written in high-level programming language into machine instructions. Its difference from a compiler is that the interpreter executes programs during translation. That is, it reads a statement, translates it, and executes it. This action sequence is repeated until all statements have been translated and executed. An interpreter does not generate a whole object program. For some statements inside the loop body, the interpreter needs to translate and execute them many times. Therefore, compared with a compiler, it is slower in execution.

## 1.5.2 The Development Process

The process of developing a C++ program includes editing, compiling, linking, running, and debugging. In editing we put the source program into the computer and save the code as a .cpp file. Compiling converts the source program into machine instructions. However, the compiled program cannot be executed directly, and we need to link multiple target files together with some files in the library to create an executable file suffixed with .exe. In the end we also need to run and debug the program.

When a compiler and a linker is linking, they will check the program and show all the errors in the screen. Errors found in the compiling stage are grammar errors and found in the linking stage are link errors. That is the development process of a C++ program.

Figure 1.1 is the development process of a C++ program.

## 1.6 Summary — 23

![](img/5618306d085ac1bac8275d6c4c5bbf2a_40_0.png)

Fig. 1.1: The development process of a C++ program.

## 1.6 Summary

A language is a system with a set of grammars and lexical rules. It is a tool of thinking, and ideas are expressed by languages. Programming languages are languages that can be recognized by a computer and are used for describing the solutions for problems. Programming languages can be classified as machine languages, assembly languages, high-level programming languages and object-oriented programming languages. This book focuses on the C++ programming language, which is the most widely used OO programming language.

Object-oriented software engineering is the application of the object-oriented method in software engineering. It consists of object-oriented analysis (OOA), object-oriented design (OOD), object-oriented programming (OOP), object-oriented test (OOT), and object-oriented software maintenance (OOSM), etc.

## 1 Introduction

Computers can process data information, while their operation is conducted by control information. All the information in computers is encoded using a binary numeral system, while different data types may have different notations, which is also one of the concerns of this book.

## Exercises

+ 1.1 Describe the development process of computer programming languages.

+ 1.2 What are the features of an object-oriented programming language?

+ 1.3 What is structured programming? Describe the advantages and disadvantages.

+ 1.4 What does "object" mean? What is an object-oriented method? Describe the features of this method.

+ 1.5 What does encapsulation mean?

+ 1.6 What does object-oriented software engineering contain?

+ 1.7 Describe the categories of information in computers.

+ 1.8 What is a binary numeral system? Describe the advantages and disadvantages of this numeral system.

+ 1.9 Convert the following decimal values into binary and hexadecimal complement codes.
a) 2 b) 9 c) 93
d) -32 e) 6555 f) -1

+ 1.10 Convert the following decimal representations into decimal values.
a) (1010)_2 b) (10001111)_2 c) (010111111000011)_2
d) (7F)_{16} e) (2DE)_{16} f) (F0E)_{16}

+ 1.11 Make a simple comparison between true code, ones-complement code, and complement code.

## Elementary C++ Programming

The chapter begins with a brief look at the history of C++ the language and its characteristics. Then we look at the basic elements that construct a C++ statement – character sets, keywords, identifiers, operators, etc. Program design mainly includes data structure and algorithm design. Data types, data type conversion, and simple data input/output are the basic elements of data. The chapter introduces C++ data types and user-defined data types. Algorithms consist of a series of control structures. The sequential, case, and loop structures described in this chapter are the most fundamental control structures in program design, and they are also the basis of complex algorithms.

## An Overview of C++ Language

## 2.1.1 Origins of C++

C++ originates from the C language. Thus, to understand C++ better, the history of the C language should be reviewed first. The C language was first realized on a DEC PDP-11 computer in 1972. Dennis Ritchie, working in Bell Laboratory, created it based on the B language. After that, continuous improvements have been made and nowadays the popular C languages are based on ANSI C.

The C language has many advantages, such as its simplicity and agility, its abundant operators and data structures, its structured controlling statements, and its high efficiency when executing programs. It combines the advantages of both high-level languages and assembly language: compared with other high-level languages, the C language can access physical address; while compared with assembly language, it has better readability and portability. Because of all these features, the C language has been widely used by numerous programmers, and there are many library codes and developing environments.

However, since C language is a procedure-oriented programming language, like other procedure-oriented languages, it cannot meet the needs of software development that uses object-oriented methods. C++ was then created from C to support object-oriented programming. It is a general-purpose language. It was created by Bjarne Stroustrup, a doctor at AT&T Bell Labs, in 1980.

Since the primary objective in creating the C++ language was to make it a better, C++ has successfully solved all the problems in C. Another important goal of C++ was to support object-oriented programming, and this class was introduced. The initial name for C++ was “C with Class”, and later in 1983 it was formally renamed as C++. The standardization of C++ began in 1989 and an ANSI C++ standardization draft was made before it in 1994. In the following years, continuous improvements were made before it.
