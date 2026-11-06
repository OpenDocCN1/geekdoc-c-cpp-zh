
minutes. Use the Internet to investigate the causes of this crash and discuss the issues it raises.

### Making a Difference Resources

The *Microsoft Imagine Cup* is a global competition in which students use technology to try to solve some of the world’s most difficult problems, such as environmental sustainability, ending hunger, emergency response, literacy and more. For more information about the competition and to learn about previous winners’ projects, visit [https://www.imaginecup.com/Custom/Index/About](https://www.imaginecup.com/Custom/Index/About). You can also find several project ideas submitted by worldwide charitable organizations. For additional ideas for programming projects that can make a difference, search the web for “making a difference” and visit the following websites:

- [http://www.un.org/millenniumgoals](http://www.un.org/millenniumgoals)
  
  The United Nations Millennium Project seeks solutions to major worldwide issues such as environmental sustainability, gender equality, child and maternal health, universal education and more.
- [http://www.ibm.com/smarterplanet](http://www.ibm.com/smarterplanet)
  
  The IBM® Smarter Planet website discusses how IBM is using technology to solve issues related to business, cloud computing, education, sustainability and more.
- [http://www.gatesfoundation.org](http://www.gatesfoundation.org)
  
  The Bill and Melinda Gates Foundation provides grants to organizations that work to alleviate hunger, poverty and disease in developing countries.
- http://nethope.org
  
  NetHope is a collaboration of humanitarian organizations worldwide working to solve technology problems such as connectivity, emergency response and more.
- http://www.rainforestfoundation.org
  
  The Rainforest Foundation works to preserve rainforests and to protect the rights of the indigenous people who call the rainforests home. The site includes a list of things you can do to help.
- http://www.undp.org
  
  The United Nations Development Programme (UNDP) seeks solutions to global challenges such as crisis prevention and recovery, energy and the environment, democratic governance and more.
- http://www.unido.org
  
  The United Nations Industrial Development Organization (UNIDO) seeks to reduce poverty, give developing countries the opportunity to participate in global trade, and promote energy efficiency and sustainability.
- http://www.usaid.gov/
  
  USAID promotes global democracy, health, economic growth, conflict prevention, humanitarian aid and more.

### Answers to Self-Review Exercises

- **1.1**
  - A. programs.
  - B. input unit, output unit, memory unit, central processing unit, arithmetic and logic unit, secondary storage unit.
  - C. machine languages, assembly languages, high-level languages.
  - D. compilers.
  - E. Android.
  - F. Release candidate.
  - G. accelerometer.
- **1.2**
  - A. editor.
  - B. preprocessor.
  - C. linker.
  - D. loader.
- **1.3**
  - A. information hiding.
  - B. classes.
  - C. object-oriented analysis and design (OOAD).
  - D. inheritance.
  - E. The Unified Modeling Language (UML).
  - F. attributes.

## 2 Introduction to C++ Programming, Input/Output and Operators

### Objectives

In this chapter you’ll:

- Write basic computer programs in C++.
- Write input and output statements.
- Use fundamental types.
- Learn computer memory concepts.
- Use arithmetic operators.
- Understand the precedence of arithmetic operators.
- Write decision-making statements.

### Outline

- **2.1 Introduction**
- **2.2 First Program in C++: Printing a Line of Text**
- **2.3 Modifying Our First C++ Program**
- **2.4 Another C++ Program: Adding Integers**
- **2.5 Memory Concepts**
- **2.6 Arithmetic**
- **2.7 Decision Making: Equality and Relational Operators**
- **2.8 Wrap-Up**

- **Summary**
- **Self-Review Exercises**
- **Answers to Self-Review Exercises**
- **Exercises**
- **Making a Difference**

### 2.1 Introduction

We now introduce C++ programming, which facilitates a disciplined approach to program development. Most of the C++ programs you’ll study in this book process data and display results. In this chapter, we present five examples that demonstrate how your programs can display messages and obtain data from the user for processing. The first three examples display messages on the screen. The next obtains two numbers from a user at the keyboard, calculates their sum and displays the result. The accompanying discussion shows you how to perform *arithmetic calculations* and save their results for later use. The fifth example demonstrates *decision making* by showing you how to *compare* two numbers, then display messages based on the comparison results. We analyze each program one line at a time to help you ease into C++ programming.

### Compiling and Running Programs

We’ve posted videos that demonstrate compiling and running programs in Microsoft Visual C++, GNU C++ and Xcode Clang/LLVM at

[http://www.deitel.com/books/cpphtp10](http://www.deitel.com/books/cpphtp10)

### 2.2 First Program in C++: Printing a Line of Text

Consider a simple program that prints a line of text (Fig. 2.1). This program illustrates several important features of the C++ language. The text in lines 1–10 is the program’s source code (or code). The line numbers are not part of the source code.

```cpp
// Fig. 2.1: fig02_01.cpp
// Text-printing program.
#include <iostream> // enables program to output data to the screen

// function main begins program execution
int main() {
    std::cout << "Welcome to C++!\n"; // display message

    return 0; // indicate that program ended successfully
} // end function main
```

```text
Welcome to C++!
```

**Fig. 2.1 Text-printing program.**

### Comments

### Lines 1 and 2

```cpp
// Fig. 2.1: fig02_01.cpp
// Text-printing program.
```

Each begins with `//`, indicating that the remainder of each line is a **comment**. You insert comments to *document* your programs and to help other people read and understand them. Comments do not cause the computer to perform any action when the program is run—they’re *ignored* by the C++ compiler and do *not* cause any machine-language object code to be generated. The comment `Text-printing program` describes the purpose of the program. A comment beginning with `//` is called a **single-line comment** because it terminates at the end of the current line. You also may use comments containing one or more lines enclosed in `/*` and `*/`, as in

```cpp
/*
 * Fig. 2.1: fig02_01.cpp
 * Text-printing program. */
```

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_209_0.png)

### Good Programming Practice 2.1

*Every program should begin with a comment that describes the purpose of the program.*

### `#include` *Preprocessing Directive*

Line 3

```cpp
#include <iostream> // enables program to output data to the screen
```

is a **preprocessing directive**, which is a message to the C++ preprocessor (introduced in **Section 1.9**). Lines that begin with `#` are processed by the preprocessor *before* the program is compiled. This line notifies the preprocessor to include in the program the contents of the **input/output stream header** `<iostream>`. This header is a file containing information the compiler uses when compiling any program that outputs data to the screen or inputs data from the keyboard using C++’s stream input/output. The program in **Fig. 2.1** outputs data to the screen, as we’ll soon see. We discuss headers in more detail in **Chapter 6** and explain the contents of `<iostream>` in **Chapter 13**.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_210_0.png)

### Common Programming Error 2.1

> *Forgetting to include the `<iostream>` header in a program that inputs data from the keyboard or outputs data to the screen causes the compiler to issue an error message.*

### Blank Lines and White Space

Line 4 is simply a *blank line*. You use blank lines, *space characters* and *tab characters* (i.e., “tabs”) to make programs easier to read.
