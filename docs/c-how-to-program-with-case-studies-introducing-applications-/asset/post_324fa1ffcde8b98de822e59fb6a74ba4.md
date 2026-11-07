
c) Read an integer from the keyboard and store the value in integer variable a.
d) If number is not equal to 7, display "number is not equal to 7."
e) Display "This is a C program." on one line.
f) Display "This is a C program." on two lines so the first line ends with C.
g) Display "This is a C program." with each word on a separate line.
h) Display "This is a C program." with the words separated by tabs.

## 2.4 Write a statement (or comment) to accomplish each of the following:

- a) State that a program will calculate the product of three integers.
- b) Prompt the user to enter three integers.
- c) Define the variable x to be of type int and initialize it to 0.
- d) Define the variable y to be of type int and initialize it to 0.
- e) Define the variable z to be of type int and initialize it to 0.
- f) Read three integers from the keyboard and store them in variables x, y and z.
- g) Define the variable result, compute the product of the integers in the variables x, y and z, and use that product to initialize the variable result.
- h) Display "The product is" followed by the value of the int variable result.

## 2.5 Using the statements you wrote in Exercise 2.4, write a complete program that calculates the product of three integers.

## 2.6 Identify and correct the errors in each of the following statements:

```
a) printf("The value is %d\n", &number);
b) scanf("%d", &number1, number2);
c) if (c < 7);{
       puts("C is less than 7");
   }
d) if (c >= 7) {
       puts("C is greater than or equal to 7");
   }
```

## Answers to Self-Review Exercises

- 2.1 a) main. b) left brace ({), right brace (}), c) semicolon. d) printf. e) newline. f) scanf. g) %. h) destructive. i) nondestructive. j) if.

## 2.2 See the answers below:

- a) *False.* Function printf always begins printing where the cursor is positioned, and this may be anywhere on a line of the screen.
- b) *False.* Comments do not cause any action to be performed when the program is executed. They're used to document programs and improve their readability.
- c) *True.*
- d) *True.*
- e) *True.*
- f) *False.* C is case sensitive, so these variables are different.
- g) *True.*

## 2.6 See the answers below:

- a) Error: &number.
  Correction: Eliminate the &. We discuss exceptions to this later.
- b) Error: number2 does not have an ampersand.
  Correction: number2 should be &number2. Later in the text, we discuss exceptions to this.
- c) Error: Semicolon after the right parenthesis of the condition in the if statement. The puts will execute whether or not the if statement's condition is true. The semicolon after the right parenthesis is an empty statement that does nothing.
  Correction: Remove the semicolon after the right parenthesis.
- d) Error: => is not an operator in C.
  Correction: The relational operator => should be changed to >= (greater than or equal to).

## Exercises

## 2.7 Identify and correct the errors in each of the following statements. (Note: There may be more than one error per statement.)

- a) `scanf("d", value);`
- b) `printf("The product of %d and %d is %d\n", x, y);`
- c) `firstNumber + secondNumber = sumOfNumbers`
- d) `if (number => largest) { largest == number; }`
- e) `/* Program to determine the largest of three integers */`
- f) `Scanf("%d", anInteger);`
- g) `printf("Remainder of %d divided by %d is\n", x, y, x % y);`
- h) `if (x = y); { printf("%d is equal to %d\n", x, y); }`
- i) `print("The sum is %d\n," x + y);`
- j) `Printf("The value you entered is: %d\n, &value);`

## 2.8 Fill-In the blanks in each of the following:

- a) ______ are used to document a program and improve its readability.
- b) The function used to display information on the screen is ______.
- c) A C statement that makes a decision is ______.
- d) Calculations are normally performed by ______ statements.
- e) The ______ function inputs values from the keyboard.

## 2.9 Write a single C statement or line that accomplishes each of the following:

- a) Display the message "Enter two numbers."
- b) Assign the product of variables b and c to variable a.

## 2.15 State the order of evaluation of the operators in each of the following C statements and show the value of x after each statement is performed.

- a) x = 7 + 3 * 6 / 2 - 1;
- b) x = 2 % 2 + 2 * 2 - 2 / 2;
- c) x = (3 * 9 * (3 + (9 * 3 / (3)))));

## 2.16 (Arithmetic) Write a program that reads two integers from the user then displays their sum, product, difference, quotient and remainder.

## 2.17 (Displaying Values with printf) Write a program that displays the numbers 1 to 4 on the same line. Write the program using the following methods.

- a) Using one printf statement with no conversion specifications.
- b) Using one printf statement with four conversion specifications.
- c) Using four printf statements.

## 2.18 (Comparing Integers) Write a program that reads two integers from the user then displays the larger number followed by the words "is larger." If the numbers are equal, display the message "These numbers are equal." Use only the single-selection form of the if statement you learned in this chapter.

## 2.19 (Arithmetic, Largest Value and Smallest Value) Write a program that inputs three different integers from the keyboard, then displays the sum, the average, the product, the smallest and the largest of these numbers. Use only the single-selection form of the if statement you learned in this chapter. The screen dialogue should appear as follows:

```
Enter three different integers: 13 27 14
Sum is 54
Average is 18
Product is 4914
Smallest is 13
Largest is 27
```

## 2.20 (Circle Area, Diameter and Circumference) For a circle of radius 2, display the diameter, circumference and area. Use the value 3.14159 for π. Use the following formulas (r is the radius): diameter = 2r, circumference = 2πr and area = πr². Perform each of these calculations inside the printf statement(s) and use the conversion specification %f. This chapter discussed only integer constants and variables. Chapter 3 will discuss floating-point numbers—that is, values that can have decimal points.

## 2.21 What does the following code display?

```
printf(" %s", " %n%*%n%***%n****%n");
```

## 2.22 (Odd or Even) Write a program that reads an integer and determines and displays whether it is odd or even. Use the remainder operator. An even number is a multiple of two. Any multiple of two leaves a remainder of zero when divided by 2.

## 2.23 (Multiples) Write a program that reads two integers and determines and displays whether the first is a multiple of the second. Use the remainder operator.

target heart rates may vary based on the health, fitness and gender of the individual. Always consult a physician or qualified healthcare professional before beginning or modifying an exercise program.

## 2.29 (Sort in Ascending Order) Write a program that inputs three different numbers from the user. Display the numbers in increasing order. Recall that an if statement's body can contain more than one statement. Prove that your script works by running it on all six possible orderings of the numbers. Does your script work with duplicate numbers? [This is challenging. In later chapters you'll do this more conveniently and with many more numbers.]

## Outline

- 3.1 Introduction
- 3.2 Algorithms
- 3.3 Pseudocode
- 3.4 Control Structures
- 3.5 The if Selection Statement
- 3.6 The if...else Selection Statement
- 3.7 The while Iteration Statement
- 3.8 Formulating Algorithms Case Study 1: Counter-Controlled Iteration
- 3.9 Formulating Algorithms with Top-Down, Stepwise Refinement Case Study 2: Sentinel-Controlled Iteration
- 3.10 Formulating Algorithms with Top-Down, Stepwise Refinement Case Study 3: Nested Control Statements
- 3.11 Assignment Operators
- 3.12 Increment and Decrement Operators
- 3.13 Secure C Programming

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

### 3.1 Introduction

Before writing a program to solve a problem, you must have a thorough understanding of the problem and a carefully planned solution approach. Chapters 3 and 4 discuss developing structured computer programs. In Section 4.11, we summarize the structured programming techniques developed here and in Chapter 4.

### 3.2 Algorithms

The solution to any computing problem involves executing a series of actions in a specific order. An algorithm is a procedure for solving a problem in terms of

- 1. the actions to execute, and
- 2. the order in which these actions should execute.

The following example shows that correctly specifying the order in which the actions should execute is important.

Consider the "rise-and-shine algorithm" followed by one junior executive for getting out of bed and going to work:

- 1. Get out of bed,
- 2. take off pajamas,
- 3. take a shower,
- 4. get dressed,
- 5. eat breakfast, and
- 6. carpool to work.

This routine gets the executive to work well prepared to make critical decisions. Suppose that the same steps are performed in a slightly different order:
