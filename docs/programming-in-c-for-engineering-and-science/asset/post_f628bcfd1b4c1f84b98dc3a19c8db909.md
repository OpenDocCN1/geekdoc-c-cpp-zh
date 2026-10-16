
the guidance software produced an inaccurate calculation of the time since system start-up due to accumulated roundoff errors that result from inexact binary representations of real numbers. And this time calculation was a key factor in determining the exact location of the incoming missile. The sad epilogue is that corrected software arrived in Dharan on February 26, the next day.

These are but a few examples of program errors that are more than just a nuisance and can lead to very serious and even tragic results. In such cases, careful software design, coding, and extensive and thorough testing are mandatory. In safety-critical situations where errors cannot be tolerated, relying on the results of test runs may not be sufficient because *testing can show only the presence of errors, not their absence.* It may be necessary to give a deductive proof that the program is correct and that it will always produce the correct results (assuming no system malfunction).

## 2.2.5 Maintenance

In contrast to student programs that are often run once or twice and then discarded, real-world programs may represent a significant investment of a company’s resources and be used for many years, during which time new features or enhancements may be added to upgrade the program. To illustrate, users of the program in Example 2.2 might find it more useful to be able to choose between Celsius-to-Fahrenheit and Fahrenheit-to-Celsius conversions and perhaps to add the Kelvin scale also. Because a program that offers these alternatives uses more advanced programming features, we will defer it until the next chapter.

## CHAPTER SUMMARY

Key Terms

| #include | debugger |
| algorithm | debugging |
| behavior | design |
| C++ | generalization |
| cin | input (>>) |
| class | library |
| coding | logic error |
| comment (/*, */, //) | main function |
| compiler | maintenance |
| compiler directive | namespace |
| cout | object-centered design (OCD) |
| curly braces ({ and }) | object-oriented design |

3. Three resistors are arranged in parallel in the following circuit:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_51_0.png)

For given values of R1, R2, and R3, calculate and display the combined resistance

1 / (1/R1 + 1/R2 + 1/R3)

4. The half-life of polonium is 140 days, which means that because of radioactive decay, the amount of polonium that remains after 140 days is one-half of the original amount. For a given initial amount of polonium and number of days, calculate the amount remaining after that many days.

# PROGRAMMING PROBLEMS

1. Enter and execute the following C++ program on your computer system:

```
/* This program adds the values of variables x and y.

Output: The value x + y
--------------------------------------------------------------- */

#include <iostream>
using namespace std;

int main()
{
    int x = 214,   // the first value
        y = 2057,  // the second value
        sum = x + y;
    // output the resulting value
    cout << "\nThe sum of " << x << " and " << y
         << " is " << sum << endl;
}
```

2. Make the following changes in the program in Problem 1 and execute the modified program:

- a. Change 214 to 1723 in the statement that gives x a value.
- b. Change the variable names x and y to alpha and beta throughout.

c. Add the comment

```
// find their sum
```

following the declaration of sum.

d. Change the variable declarations to

```
int alpha = 214,      // the first value
    beta = 2057,      // the second value
    difference = alpha - beta,  // find their difference
    sum = alpha + beta;          // find their sum
```

and add the following statement before the output statement:

```
cout << "\nThe difference of " << alpha << " and "
    << beta << " is " << difference << endl;
```

3. Using the program in this chapter as a guide, write a C++ program to solve the problem in Exercise 1.

4. Using the program in this chapter as a guide, write a C++ program to solve the problem in Exercise 2.

5. Using the program in this chapter as a guide, write a C++ program to solve the problem in Exercise 3.

## Types in C++

## CONTENTS

- 3.1 Introductory Example: Radioactive Decay 40
- 3.2 Types, Literals, Variables, and Constants 42
- 3.3 Data Representation 51
- Chapter Summary 55
- Test Yourself 58
- Exercises 60
- Programming Problems 61

There are three types of people in this world: Those who can count, and those who can’t.

> SEEN ON A BUMPER STICKER

Kindly enter them in your notebook.
And, in order to refer to them conveniently, let’s call them A, B, and Z.

> LEWIS CARROLL, “WHAT THE TORTOISE SAID TO ACHILLES”

For, contrary to the unreasoned opinion of the ignorant, the choice of a system of numeration is a mere matter of convention.

> BLAISE PASCAL

IN THIS CHAPTER, WE look at some of the data types that are provided in C++, focusing on the simplest ones, called fundamental types. We also show how values of these types are represented in such a way that they can be stored in memory.

## 3.1 INTRODUCTORY EXAMPLE: RADIOACTIVE DECAY

### 3.1.1 Problem

A scientist at Uranium University is conducting research with the radioactive element polonium. The half-life of polonium is 140 days, which means that because of radioactive decay, the amount that remains after 140 days is one-half of the original amount. He would like to know how much polonium will remain after running the experiment for 180 days if 10 milligrams are present initially.

### 3.1.2 Object-Centered Design

#### 3.1.2.1 Behavior

The program should output to the screen a prompt for the name of the radioactive element, its half-life, the initial amount, and a time period. It will then read these values from the keyboard. The program should then compute the amount remaining after the specified time period and output the input values along with this value to the screen.

#### 3.1.2.2 Objects

From our behavioral description, we can identify the following objects:

| Problem Objects | Type | Kind | Name |
|---|---|---|---|
| screen | output device | variable | cout |
| prompt | text string | constant | none |
| name of element | text string | variable | element |
| half-life | real number | variable | halfLife |
| initial amount | real number | variable | initialAmount |
| time period | real number | variable | time |
| keyboard | input device | variable | cin |
| amount remaining | real number | variable | amountRemaining |

#### 3.1.2.3 Operations

Again, from our behavioral description, we have the following operations:

- i. Output a string (the prompts, descriptive labels, element’s name).
- ii. Read a string (element).
- iii. Read numeric values (halfLife, initialAmount, time).
- iv. Compute amountRemaining = initialAmount × (0.5)^(time/halfLife).
- v. Output numeric values.

C++ provides operations for each of these operations.

#### 3.1.2.4 Algorithm

Next, we organize these objects and operations into an algorithm:

- 1. Output a prompt for the element’s name and it’s half-life to cout.
- 2. Read a string from cin to store in element and a real value to store in halfLife.
- 3. Output a prompt for the initial amount and the time period.
- 4. Read real values from cin to store in initialAmount and time.
- 5. Compute amountRemaining = initialAmount × (0.5)^(time/halfLife).
- 6. Output element, halfLife, initialAmount, time, and amountRemaining with appropriate labels to cout.

#### 3.1.2.5 Coding, Execution, and Testing

In the preceding chapter we outlined a procedure for translating the algorithm into code:

- 1. Create a program stub that contains opening documentation, compiler directives that add items in libraries needed for some of the objects and operations, and a main function that contains only the steps of the algorithm as comments.
- 2. Convert each step of the algorithm into code, adding a declaration statement to specify an object’s type and name for any software object not already declared.

Space restrictions prevent doing this for each example in this text, but you may find that this procedure helps with developing programs like that in Example 3.1, which shows the finished product and a sample run to find how much of 10 mg of polonium with a half-life of 140 days will remain after 180 days. You are encouraged to enter this program in the version of C++ that you are using, compile and execute it, and experiment with it, making various changes and seeing what happens.

# Example 3.1 Radioactive Decay

```
/* This program computes the amount of a radioactive substance
remaining after an initial amount decays for some time period.

Written by John Doe for CS 104 -- Project #1 -- Feb. 5, 2012

Input:  element's name, its half-life, the initial amount,
        and a time period
Output: the input items and the amount of the substance
        remaining at the end of the time period
------------------------------------------------------------*/
#include <iostream>    // cin, cout, <<, >>
#include <string>      // string
#include <cmath>       // pow()
using namespace std;
```
