
## CHAPTER 12 Streams and File I/O

As an example, given the following input file:

```cpp
#include <iostream>

int main() {
    int x=4;
    if (x < 3) x++;
    cout << x << endl;
}
```

the program should produce a text file with the following contents:

```cpp
#include <iostream>
int main() {
    int x=4;
    if (x < 3) x++;
    cout << x << endl;
}
```

You can test your output file by opening it with a web browser. The contents should appear identical to the original source code.

- 20. Write a class that tracks the five highest scores for a game. The scores should be stored in a file and include the player's name as a string and the player's score as an integer. The list of top scores initially consist of the name Anonymous and scores of 0. The class should support the following functions:

    - A way to output to the screen the name and score of the five players. The scores should be listed in order, with the highest score first and the lowest score last.

    - A function that takes a new name and score. If the score is higher than any of the top five scores it should be added to the file and the lowest score discarded. Otherwise, the top list should remain unchanged.

Include an appropriate constructor or destructor if necessary, along with helper functions. Write a main function that tests your list by simulating several entries and outputting the high score list.

- 21. The text file words.txt, which is included in the source code for this book, contains an alphabetically sorted list of English words. Note that the words are in mixed upper and lowercase.

Write a program to read each word, one line at a time, and help find the word that has the most consecutive vowels. Use only the letters a, e, i, o, and u as vowels.

For example, the word “aqueous” has four consecutive vowels. However, there is a word in the list with five consecutive vowels. What is it?

## Programming Projects

- 22. Re-do or instead of hard-coding the trivia data, your program Project 9.10 from Chapter 9. However, your program should read the questions in from a text file named `trivia.txt`. The format of the text file should be

```
<number of questions, N>
<question 1>
<answer 1>
<dollar amount for 1>
<question 2>
<Answer 2>
<dollar amount for 2>
..
<question N>
<answer N>
<dollar amount for N>
```

For example, here is a very short file with two questions:

```
2
Creator of the C++ programming language?
Bjarne Stroustrup
10.00
The geometric figure most like a lost parrot?
Polygon
20.00
```

- 23. This Programming Project requires that you complete Programming Project 9.11, which asked you to write a function to determine if two strings are anagrams. The text file words.txt, which is included in the source code on this book's website, contains an alphabetically sorted list of English words. Write a program that reads each word into an array or vector. Next, input a word from the console and output every word in the array or vector that is an input of the project.

- 24. A comma-separated values or CSV file is a simple text format to store a list of records. A comma is used as a delimiter to separate the fields for each record. This format is commonly used to transfer data to a spreadsheet or database. In this Programming Project, consider a store that sells products abbreviated as A, B, C, D, E. Customers rate each product from 1–5 where 1 is poor and 5 is excellent. The ratings are stored in a CSV file where each row contains the customer's ratings for each product. Here is a sample file with three customer ratings and five products:

```
A,B,C,D,E
3,0,5,1,2
1,1,4,2,1
0,0,5,1,3
```

The first line in this file format lists the products. The digit 0 indicates that a customer did not rate a product. In this case the first customer rated A as 3, C as 5, D as 1, and E as 2. Product B was not rated. The third customer rated C as 5, D as 1, and E as 3. The third customer did not rate A or B.

Create a text file in this format with sample ratings. Then write a program that reads in the text file and uses the first line to determine the number of products. The program should output the average rating for each product. Customers that did not rate a product should not be considered when computing the average rating for that product. The easiest solution to process the data may be to use the getline function with the comma as a delimiter and to create vectors or dynamic arrays to store the count and sum of the ratings.

- 25. One problem using cin to read directly into a variable such as an int is if the user enters non-integer data then the program will continue with erroneous data and usually crash. A solution to this problem is to input data as a string, perform input validation, and then convert the string to an integer. Write a function that prompts the user to enter an integer. The program should use getline to read the user's input into a string. Then use the stringstream class to extract an integer from the string. If an integer cannot be extracted the user should be prompted to try again. The function should return the extracted integer.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_599_0.png)

VideoNote
Solution to Programming Project 12.25

## CHAPTER 13 Recursion

### 13.1 RECURSIVE VOID FUNCTIONS

- Example: Vertical Numbers 573
- Tracing a Recursive Call 576
- A Closer Look at Recursion 579
- Pitfall: Infinite Recursion 580
- Stacks for Recursion 582
- Pitfall: Stack Overflow 583
- Recursion versus Iteration 584

### 13.3 THINKING RECURSIVELY

- Recursive Design Techniques 593
- Binary Search 594
- Coding 596
- Checking the 600

### 13.2 RECURSIVE FUNCTIONS THAT RETURN A VALUE

- General Form for a Function That Returns a Value 585
- Example: Another Function 586
- Recursion 600

## Introduction

In C++ a function definition may contain a call to the function being defined. In such cases the function is said to be recursive.

> In C++ a function definition may contain a call to the function being defined. In such cases the function is said to be recursive.

When you are writing a function to solve a task, one basic design technique is to break the task into subtasks. Sometimes it turns out that at least one of the subtasks is a smaller example of the same task. For example, if the task is to search a list for a particular value, you might divide this into the subtask of searching the first half of the list and subtask of searching the second half of the list. The subtasks of the halves are "smaller" versions of the original task. Whenever one subtask is a smaller version of the original task, you can solve the original task using a recursive function. We begin with a simple example to illustrate this technique.

## EXAMPLE: Vertical Numbers

Example 13.1 contains a demonstration program for a recursive function named writeVertical that takes one (nonnegative) argument and writes to the screen, with the digits going down the screen one per line. For example, the invocation

```
writeVertical(1234);
```

would produce the output

+
1
2
3
4

The task to be performed by writeVertical may be broken down into the following cases:

- Simple case: If n < 10, then we write the number n to the screen. After all, if the number is only one digit, the task is trivial.
