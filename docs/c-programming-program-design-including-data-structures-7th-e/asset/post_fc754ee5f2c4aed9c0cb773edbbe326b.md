
## How to Use the Book

This book can be used in various ways. Figure 1 shows the dependency of the chapters.

![](img/d0be7fc6d804b63484835c6c8bc67a07_41_0.png)

**FIGURE 1** Chapter dependency diagram

### FEATURES OF THE BOOK

![](img/d0be7fc6d804b63484835c6c8bc67a07_42_0.png)

```cpp
do {
    int guess = 0;
    cout << "Number? You guessed the correct number."
         << endl;
    isGuessed = true;
} else {
    cout << "Your guess is lower than the number.\n";
    cout << "Guess again!" << endl;
    cout << "Your guess is higher than the number.\n";
}
// end while
```

You also need the following code to be included after the while loop in case the user cannot guess the correct number in five tries:

```cpp
if (isGuessed)
{
    cout << "You lost! The correct number is " << num << endl;
}
```

Programming Exercise 15 at the end of this chapter asks you to write a complete C++ program to implement the Number Guessing Game in which the user has, at most, five tries to guess the number.

As you can see from the preceding while loop, the expression in a while statement can be complex. The main objective of a while loop is to repeat certain statement(s) until certain conditions are met.

### PROGRAMMING EXAMPLE: Fibonacci Number

![](img/d0be7fc6d804b63484835c6c8bc67a07_42_1.png)

So far, you have seen several examples of loops. Recall that in C++, while loops are used when certain statements must be repeated repeatedly until certain conditions are met. Next, following is a C++ program that uses a while loop to find a Fibonacci number.

- Consider the following sequence of numbers:
- 1, 1, 2, 3, 5, 8, 13, 21, 34, …

This sequence is called the Fibonacci sequence. Given the first two numbers of the sequence (say, a₁ and a₂), the nth number aₙ, n ≥ 3, of this sequence is given by:

_aₙ = aₙ₋₁ + aₙ₋₂_

Thus:

a₃ = a₂ + a₁ = 1 + 1 = 2,

a₄ = a₃ + a₂ = 2 + 1 = 3,

and so on.

Four-color interior design shows accurate C++ code and related comments.

One video is available for each chapter on the optional CourseMate that accompanies this text. Each video is designed to explain how a program works.

## Control Structures

Chapter 2 defined a program as a sequence of statements whose objective is to accomplish some task. The programs you have examined so far were simple and straightforward. To process a program, the computer begins at the first executable statement and executes the statements in order until it comes to the end. In this chapter and Chapter 5, you will learn how to tell a computer that it does not have to follow a simple sequential order of statements; it can also make decisions and follow certain statements over and over until certain conditions are met.

A computer can process a program in one of the following ways: in sequence; selectively, by making a choice, which is also called a branch; repetitively, by executing a statement over and over, using a structure called a loop, or by calling a function. Figure 4-1 illustrates the first three types of program flow. (In Chapter 6, we will show how functions work.) The programming examples in Chapters 2 and 3 included simple sequential programs. With a program, the computer starts at the beginning and follows the statements in order to the end. No choices are made; there is no repetition. Control structures provide alternatives to sequential program execution and are used to alter the sequential flow of execution. The two most common control structures are selection and repetition. In selection, the program executes particular statements depending on some condition(s). In repetition, the program repeats particular statements a certain number of times based on some condition(s).

![](img/d0be7fc6d804b63484835c6c8bc67a07_43_0.png)

Figure 4-1 – Flow of execution

More than 400 visual diagrams, both extensive and exhaustive, illustrate difficult concepts.

In C++, identifiers can be of any length.

### EXAMPLE 2-2

The following are legal identifiers in C++:

- first
- conversion
- payRate
- counter1

TABLE 2-1 Examples of Illegal Identifiers and explains why they are illegal and also gives a correct identifier.

| Illegal Identifier | Reason | A Correct Identifier |
|---|---|---|
| `employee Salary` | There can be no space between employee and Salary. | `employeeSalary` |
| `Hello!` | The exclamation mark cannot be used in an identifier. | `Hello` |
| `one+two` | The symbol + cannot be used in an identifier. | `onePlusTwo` |
| `2nd` | An identifier cannot begin with a digit. | `second` |

> **NOTE** Compiler vendors usually begin certain identifiers with an underscore (_). When the linker links the object program with the system resources provided by the integrated development environment (IDE), certain errors could occur. Therefore, it is advisable that you should not begin identifiers in your program with an underscore (_).

### Whitespaces

Every C++ program contains whitespaces. Whitespaces include blanks, tabs, and newline characters. In C++, however, whitespaces are used to separate special symbols, reserved words, and identifiers. Whitespaces are nonprintable in the sense that when they are printed on a white sheet of paper, the space between special symbols, reserved words, and identifiers is white. Proper utilization of whitespaces in a program is important. They can be used to make the program more readable.

> Numbered Examples illustrate the key concepts with their relevant code. The programming code in these examples is followed by a Sample Run. An explanation then follows that describes what each line in the code does.

> Notes highlight important facts about the concepts introduced in the chapter.

Programming Examples are where everything in the chapter comes together. These examples teach problem-solving skills and include the concrete stages of input, output, problem analysis and algorithm design, class design, and a program listing. All programs are designed to be methodical, consistent, and user-friendly. Each Programming Example starts with a problem analysis that is followed by the algorithm design and/or class design, and every step of the algorithm is coded in C++. In addition to helping students learn problem-solving techniques, these detailed programs show the student how to implement concepts in an actual C++ program. We strongly recommend that students study the Programming Examples carefully in order to learn C++ effectively. Students typically learn much from completely worked-out programs. Further, programming examples considerably reduce students’ need for help outside the classroom and bolster students’ self-confidence.

### PROGRAMMING EXAMPLE: Convert Length

![](img/d0be7fc6d804b63484835c6c8bc67a07_45_0.png)

Write a program that takes as input given lengths expressed in feet and inches. The program should then convert and output the lengths in centimeters. Assume that the given lengths in feet and inches are integers.

**Input:** Length in feet and inches.

**Output:** Equivalent length in centimeters.

**PROBLEM ANALYSIS**

The input is the length in feet and inches. The output is the equivalent length in centimeters. One inch is equal to 2.54 centimeters. The first thing the program needs to do is convert the length given in feet and inches to all inches. Then, you can use the conversion formula, 1 inch = 2.54 centimeters, to find the equivalent length in centimeters. To convert the length from feet and inches to inches, you multiply the number of feet by 12, as 1 foot is equal to 12 inches, and add the given inches.

For example, suppose the input is 5 feet and 3 inches. You then find the total inches as follows:

```cpp
totalInches = (12 * feet) + inches
            = 12 * 5 + 3
            = 67
```

You can then apply the conversion formula, 1 inch ≈ 2.54 centimeters, to find the length in centimeters.

```cpp
centimeters = totalInches * 2.54
             = 67 * 2.54
             = 170.18
```

Based on this analysis of the problem, you can design an algorithm as follows:

- 1. Get the length in feet and inches.
- 2. Convert the length into total inches.
- 3. Convert total inches into centimeters.
- 4. Output centimeters.

**Variables:** The input for the program is two numbers: one for feet and one for inches. Thus, you need two variables: one to store feet and the other to store inches. Because the program will first convert the given length into inches, you need another variable to store the total inches. You also need a variable to store the equivalent length in centimeters. In summary, you need the following variables:

```cpp
int feet;              // variable to hold given feet
int inches;            // variable to hold given inches
int totalInches;       // variable to hold total inches
double centimeters;    // variable to hold length in centimeters
```
