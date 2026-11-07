
- 23.2 Deitel Online C++ and Related Resource Centers — 937
- 23.3 Boost Libraries — 937
- 23.4 Boost Libraries Overview — 938
- 23.5 Regular Expressions with the regex Library — 941
  - 23.5.1 Regular Expression Example — 942
  - 23.5.2 Validating User Input with Regular Expressions — 944
  - 23.5.3 Replacing and Splitting Strings — 947
- 23.6 Smart Pointers — 950
  - 23.6.1 Reference Counted shared_ptr — 950
  - 23.6.2 weak_ptr: shared_ptr Observer — 954
- 23.7 Technical Report 1 — 960
- 23.8 C++0x — 961
- 23.9 Core Language Changes — 962
- 23.10 Wrap-Up — 967

## 24 Other Topics — 974

- 24.1 Introduction — 975
- 24.2 const_cast Operator — 975
- 24.3 mutable Class Members — 977
- 24.4 namespaces — 979
- 24.5 Operator Keywords — 982
- 24.6 Pointers to Class Members (`.*` and `->*`) — 984
- 24.7 Multiple Inheritance — 986
- 24.8 Multiple Inheritance and virtual Base Classes — 991
- 24.9 Wrap-Up — 996

## Chapters on the Web — 1001

- A Operator Precedence and Associativity — 1002
- B ASCII Character Set — 1004
- C Fundamental Types — 1005
- D Number Systems — 1007
  - D.1 Introduction — 1008
  - D.2 Abbreviating Binary Numbers as Octal and Hexadecimal Numbers — 1011
  - D.3 Converting Octal and Hexadecimal Numbers to Binary Numbers — 1012
  - D.4 Converting from Binary, Octal or Hexadecimal to Decimal — 1012
  - D.5 Converting from Decimal to Binary, Octal or Hexadecimal — 1013
  - D.6 Negative Binary Numbers: Two’s Complement Notation — 1015

## E Preprocessor — 1020

- E.1 Introduction — 1021
- E.2 `#include` Preprocessor Directive — 1021
- E.3 `#define` Preprocessor Directive: Symbolic Constants — 1022
- E.4 `#define` Preprocessor Directive: Macros — 1022
- E.5 Conditional Compilation — 1024
- E.6 `#error` and `#pragma` Preprocessor Directives — 1025
- E.7 Operators `#` and `##` — 1026
- E.8 Predefined Symbolic Constants — 1026
- E.9 Assertions — 1027
- E.10 Wrap-Up — 1027

## Appendices on the Web — 1033

## Index — 1035

Chapters 25–26 and Appendices F–I are PDF documents posted online at the book’s Companion Website, which is accessible from www.pearsonhighered.com/deitel.

## 25 ATM Case Study, Part 1: Object-Oriented Design with the UML — 25-1

- 25.1 Introduction — 25-1
- 25.2 Introduction to Object-Oriented Analysis and Design — 25-2
- 25.3 Examining the ATM Requirements Document — 25-3
- 25.4 Identifying the Classes in the ATM Requirements Document — 25-10
- 25.5 Identifying Class Attributes — 25-17
- 25.6 Identifying Objects’ States and Activities — 25-21
- 25.7 Identifying Class Operations — 25-25
- 25.8 Indicating Collaboration Among Objects — 25-32
- 25.9 Wrap-Up — 25-39

## 26 ATM Case Study, Part 2: Implementing an Object-Oriented Design

| Section | Title | Page |
| --- | --- | --- |
| 26.1 | Introduction | 26-2 |
| 26.2 | Starting to Program the Classes of the ATM System | 26-2 |
| 26.3 | Incorporating Inheritance into the ATM System | 26-8 |
| 26.4 | ATM Case Study Implementation | 26-15 |
| 26.4.1 | Class ATM | 26-16 |
| 26.4.2 | Class Screen | 26-23 |
| 26.4.3 | Class Keypad | 26-25 |
| 26.4.4 | Class CashDispenser | 26-26 |
| 26.4.5 | Class DepositSlot | 26-28 |
| 26.4.6 | Class Account | 26-29 |
| 26.4.7 | Class BankDatabase | 26-31 |
| 26.4.8 | Class Transaction | 26-35 |
| 26.4.9 | Class BalanceInquiry | 26-37 |
| 26.4.10 | Class Withdrawal | 26-39 |
| 26.4.11 | Class Deposit | 26-44 |
| 26.4.12 | Test Program ATMCaseStudy.cpp | 26-47 |
| 26.5 | Wrap-Up | 26-47 |

## F C Legacy Code Topics

| Section | Title | Page |
| --- | --- | --- |
| F.1 | Introduction | F-2 |
| F.2 | Redirecting Input/Output on UNIX/Linux/Mac OS X and Windows Systems | F-2 |
| F.3 | Variable-Length Argument Lists | F-3 |
| F.4 | Using Command-Line Arguments | F-5 |
| F.5 | Notes on Compiling Multiple-Source-File Programs | F-7 |
| F.6 | Program Termination with exit and atexit | F-9 |
| F.7 | Type Qualifier volatile | F-10 |
| F.8 | Suffixes for Integer and Floating-Point Constants | F-10 |
| F.9 | Signal Handling | F-11 |
| F.10 | Dynamic Memory Allocation with calloc and realloc | F-13 |
| F.11 | Unconditional Branch: goto | F-14 |
| F.12 | Unions | F-15 |
| F.13 | Linkage Specifications | F-18 |
| F.14 | Wrap-Up | F-19 |

## G UML 2: Additional Diagram Types

| Section | Title | Page |
| --- | --- | --- |
| G.1 | Introduction | G-1 |
| G.2 | Additional Diagram Types | G-2 |

![](img/bfd978e7e9b192bab46ec2a89e481263_22_0.png)

## Preface

> “The chief merit of language is clearness . . .”
>
> —Galen

### For the Student

Welcome to the C++ computer programming language and *C++ How to Program, Eighth Edition*! This book presents leading-edge computing technologies, and is particularly appropriate for introductory course sequences based on the curriculum recommendations of two key professional organizations—the ACM and the IEEE.

The new Chapter 1 presents intriguing facts and figures. Our goal is to get you excited about studying computers and programming. The chapter includes a table of some of the research made possible by computers; current technology trends and hardware discussions; the data hierarchy; social networking; a table of business and technology publications and websites that will help you stay up-to-date with the latest technology news, trends and career opportunities; additional Making a Difference exercises and more.

We focus on software engineering best practices. At the heart of the book is our signature “live-code approach”—programming concepts are presented in the context of complete working programs, rather than in code snippets. Each C++ code example is accompanied by live sample executions, so you can see exactly what each program does when it’s run on a computer. All the source code is available at www.deitel.com/books/cpphtp8/ and www.pearsonhighered.com/deitel/.

Much of this Preface is addressed to instructors. Please be sure to read the sections entitled Pedagogic Features; Teaching Approach; Software Used in *C++ How to Program, 8/e*; C++ IDE Resource Kit and CourseSmart Web Books.

We believe that this book and its support materials will give you an informative, interesting, challenging and entertaining C++ educational experience. As you read the book, if you have questions, send an e-mail to deitel@deitel.com—we’ll respond promptly. For updates on this book, visit www.deitel.com/books/cpphtp8/, follow us on Facebook (www.deitel.com/deitelfan) and Twitter (@deitel), and subscribe to the *Deitel Buzz Online* newsletter (www.deitel.com/newsletter/subscribe.html). Good luck!

### New and Updated Features

Here are the updates we’ve made for *C++ How to Program, 8/e*:

#### Impending New C++ Standard

- **Optional sections.** We cover various features of the new standard (sometimes called C++0x and due late in 2011 or early in 2012) in *optional modular sections* in Chapter 23. These are *easy to include or omit*. Popular compilers such as Microsoft Visual C++ 2010 and GNU C++ 4.5 already implement many of these features. To
