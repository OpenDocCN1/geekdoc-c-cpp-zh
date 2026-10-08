# Chapter 2. Problem Solving

integer variable stores whole numbers, while a floating-point variable stores numbers with decimals. Variables can only hold one value at a time and we have to give them a value before using them.

# Example

Let us develop an algorithm for calculating the area of a triangle. The algorithm is the following:

```
Ask the user for the length
Store the first number in the variable length
Ask the user for the width
Store the first number in the variable width
Calculate the area as 0.5 x length x width
Store the area in the variable area
Print the value of the area
```

To verify the correctness of the algorithm, we can perform a dry run. This involves manually executing the instructions using sample data. It helps us identify any logic errors before writing the actual program. Make sure the algorithm is correct before starting the program implementation to avoid wasting time and effort with an incorrect approach.

# 2.2.4 Writing the Program

To develop a computer program from an algorithm, consider user interaction and output design. A program prompts users for input, calculates results, and displays outputs in a specific format.

An algorithm and a program differ in language and rules. Algorithms can be written in an informal language, but programs require adherence to specific programming language's syntax rules.

A high-level language program, like C, is called source code. Compilation transforms source code into an executable program, which is object code found in executable files.

# Example

Below is a simple C program that prompts the user to input the length and width of a triangle and calculate its area:

```
#include <stdio.h>

int main() {
    // Declare variables to store the numbers
    int length, width, area;

    // Prompt the user to enter the length of triangle
```