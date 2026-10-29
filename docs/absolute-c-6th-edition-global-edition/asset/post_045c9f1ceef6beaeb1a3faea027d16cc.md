
## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂版面中提取结构化信息。

## 2. 方法概述

- 步骤一：图像预处理
- 步骤二：版面分析
- 步骤三：内容提取
- 步骤四：结构化输出

其中，版面分析是核心环节，它决定了后续提取的准确率。

![](img/c76bba8c1d927f399768ffe2ab5f5bee_643_0.png)

| 方法 | 准确率 | 速度 |
|------|--------|------|
| A    | 95%    | 快   |
| B    | 90%    | 中   |
| C    | 85%    | 慢   |

> 注意：以上数据基于标准测试集。

```python
print("Hello, World!")
```

of handshakes that would be made in a room of two people, or a total of three handshakes.

If a fourth person enters the room, he or she must shake hands with each of the three people already there. This is three handshakes in addition to the number of handshakes that would be made in a room of three people, or six handshakes.

If you can generalize this to n handshakes, you should be able to write the recursive solution.

### 10. Consider a frame of bowling pins, where each * represents a pin:

*
  * *
* * *
* * * *
* * * * * *

There are five rows and a total of fifteen pins. If we had only the top four rows, there would be a total of ten pins. If we had only the top three rows, there would be a total of six pins. If we had only the top two rows, there would be a total of three pins. If we had only the top row, there would be a total of one pin.

Write a recursive function that takes as input the number of rows, n, and outputs the total number of pins that would exist in a pyramid with n rows. Your program should allow for values of n that are larger than 5.

### 11. Write a recursive function named contains with the following header:

```
bool contains (char *haystack, char *needle)
```

The function should return true if the C-string needle is contained within the C-string haystack and false if needle is not in haystack. For example,

```
contains("C++ programming", "ogra") should return true
contains("C++ programming", "grammy") should return false
```

You are not allowed to use the string class substr or find functions to determine a match.

### 12. The following diagram is an example of a deterministic finite state automaton, or DFA. This particular DFA describes an algorithm to determine if a sequence of characters is a properly formatted monetary amount with commas. For example, "$1,000" and "$25" and "$551,323,991,391" are properly formatted but "1,000" (no initial $) and "$1000" (missing comma) and "$5424,132" (missing comma) are not.

![](img/c76bba8c1d927f399768ffe2ab5f5bee_645_0.png)

The DFA works by starting in the oval labeled IsMoney. This is the initial state. If the first character of the string is $, then we advance to the second character and move to state 0. Otherwise we conclude the string is not a proper monetary amount. In state 0, if the second character is a digit between 1 and 9, then we advance to the third character and move to state 1. Otherwise we conclude the string is not a proper monetary amount. In state 1, if we have no more characters left in the string, then we conclude that the string is a monetary amount. This is called a final state and is indicated by a bold oval. If the third character is a digit between 0 and 9, then we advance to the fourth character and move to state 2. Otherwise if the third character is a comma then we advance to the fourth character and move to state 4. Otherwise we conclude the string is not a proper monetary amount. The rest of the DFA behaves in a similar manner.

Write a program that uses recursion to implement the DFA. Your program should have a separate function for each state in the DFA. Each function should invoke the function corresponding to the next state indicated by the arrows in the diagram. There is mutual recursion because of the loop from state 7 to state 4. Test your solution with several strings and output whether each string is a properly formatted monetary amount.

This solution calls a function for every character in the string. However, the solution may be written in a tail-recursive manner, so it is possible that long strings will not exhaust the stack if your compiler is efficient.

### 13. A popular word game involves finding words from a grid of randomly generated letters. Words must be at least three letters long and formed from adjoining letters. Letters may not be reused and it is valid to move across diagonals. As an example, consider the following 4×4 grid of letters:

| A | B | C | D |
| E | F | G | H |
| I | J | K | L |
| M | N | O | P |

The word "FAB" is valid (letters in the upper left corner) and the word "KNIFE" is valid. The word "BABE" is not valid because the "B" may not be reused. The word "MINE" is not valid because the "E" is not adjacent to the "N".

Write a program that uses a 4 * 4 two-dimensional array to represent the game board. The program should randomly select letters for the board. You may wish to select vowels with a higher probability than consonants. You may also wish to always place a "U" next to a "Q" or to treat "QU" as a single letter. The program should read the words from the text file words.txt (included on the website with this book) and then use a recursive algorithm to determine if the word may be formed from the letters on the game board. The program should output all valid words from the file that are on the game board.

### 14.

The word ladder game was invented by Lewis Carroll in 1877. The idea is to begin with a start word and then change one letter at a time until you arrive at an end word. Each word along the way must be an English word.

For example, starting from FISH, you can arrive at MAST through the following word ladder:

FISH, WISH, WASH, MASH, MAST

Write a program that uses recursion to find the word ladder given a start word and an end word, or that determines no word ladder exists. Use the file words.txt that is available online with the source code for the book as your dictionary of valid words. This file contains 87,314 words. Your program does not need to find the shortest word ladder between words; any word ladder will do if one exists.

## Inheritance 14

### 14.1 INHERITANCE BASICS 648

- Derived Classes 648
- Constructors in Derived Classes 658
- Pitfall: Use of Private Member Variables from the Base Class 660
- Pitfall: Private Member Functions Are Effectively Not Inherited 662
- The protected Qualifier 662
- Redefinition of Member Functions 665
- Redefining versus Overloading 666
- Access to a Redefined Base Function 668
- Functions That Are Not Inherited 669

- Example: Partially Filled Array with Backup 672
- Pitfall: Same Object on Both Sides of the Assignment
- Operator 681
- Example: Alternate Implementation of PFArrayDBak 681
- Tip: A Class Has Access to Private Members of All Objects of the Class 684
- Tip: "Is a" versus "Has a" 684
- Protected and Private Inheritance 685
- Multiple Inheritance 686

### 14.2 PROGRAMMING WITH INHERITANCE 670

- Assignment Operators and Copy Constructors in Derived Classes 670
- Destructors in Derived Classes 671

## 14 Inheritance

> *Like mother, like daughter*
> 
> _Common saying_

### Introduction

Object-oriented programming is a popular and powerful programming technique. Among other things, it provides for a dimension of abstraction known as *inheritance*. This means that a very general form of a class can be defined and compiled. Later, more specialized versions of that class may be defined and can inherit the properties of the general class. This chapter covers inheritance in general and, more specifically, how it is realized in C++.

This chapter does not use any of the material presented in Chapter 12 (file I/O) or Chapter 13 (recursion). It also does not use the material in Section 7.3 of Chapter 7, which covers vectors. Section 14.1 also does not use any material from Chapter 10 (pointers and dynamic arrays).

### 14.1 Inheritance Basics

> *If there is anything that we wish to change in the child, we should first examine it and see whether it is not something that could better be changed in ourselves.*
> 
> CARL GUSTAV JUNG, *The Integration of the Personality: Trans.*
> 
> Stanley M. Dell. New York City: Farrar & Rinehart, Incorporated, 1939

Inheritance is the process by which a new class—known as a **derived class**—is created from another class, called the **base class**. A derived class automatically has all the member variables and all the ordinary member functions that the base class has and can have additional member functions and additional member variables.

### Derived Classes

Suppose we are designing a record-keeping program that has records for salaried employees and hourly employees. There is a natural hierarchy for grouping these classes. These are all classes of people who share the property of being employees.

Employees who are paid an hourly wage are one subset of employees. Another subset consists of employees who are paid a fixed wage each month or week. Although the program may not need any type corresponding to the set of all employees, thinking in terms of the more general concept of employees can be useful. For example, all employees have names and Social Security numbers, and the member functions for
