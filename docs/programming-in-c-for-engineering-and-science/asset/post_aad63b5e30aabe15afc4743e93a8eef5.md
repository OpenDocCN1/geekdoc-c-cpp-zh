
characterizes sequential execution and indicates clearly that the statements are executed in the order in which they are given with each statement being executed exactly once.

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_123_0.png)

Although sequence is a fundamental control structure, it is not powerful enough to solve all problems. Some problems require selecting one of several alternative actions, which means that programs for solving them will need a selection structure. In this chapter we will consider one selection structure that C++ provides: the if statement. Another, the switch statement, is described in Chapter 8.

For some problems, however, another control structure besides sequence and selection is needed, one that makes it possible to execute one or more statements repeatedly—a repetition structure. We will consider two such repetition structures provided in C++, the for and while statements, in the last part of this chapter.

Sequence, selection, and repetition are the only control structures needed. A fundamental result of theoretical computer science states that any problem solvable by a computer program can be solved by one that is made up of sequence, selection, and repetition structures.¹

> ¹ This theorem is usually credited to a 1966 paper by Corrado Böhm and Giuseppe Jacopini.

## 5.1 INTRODUCTORY EXAMPLE: AIR QUALITY INDEX (AQI)

### 5.1.2 Problem

Pollution levels are measured at three locations in a city and the Air Quality Index (AQI), also known as the Air-Pollution Index (API), is the integer average of these three readings. An index of less than 50 parts per million indicates a safe condition, whereas indexes of 50 parts per million or greater indicate a hazardous condition.² The city’s environmental statistician would like a program that calculates these air quality indexes and determines the appropriate pollution condition, safe or hazardous.

> ² Here we are considering a simplified AQI that has only two categories, but in practice, there are usually more than two. For example, as we will see in Chapter 8 where we consider selection structures with more than two alternatives, there are 6 categories for the United States AQI.

### 5.1.3 Object-Centered Design

#### 5.1.3.1 Behavior

The program should display on the screen a prompt for three pollution readings (parts per million). It will then read these values from the keyboard and calculate the air quality index, which is the average of the readings rounded to the nearest integer. The program should display the air quality index to the screen, compare it with the cutoff value that separates hazardous and safe conditions, and display the corresponding condition.

#### 5.1.3.2 Objects

From our behavioral description, we can identify the following objects:

| Problem Objects | Software Objects |  |  |
| --- | --- | --- | --- |
|  | Type | Kind | Name |
| screen | output device | variable | cout |
| prompt | text string | constant | none |
| keyboard | input device | variable | cin |
| pollution levels | double | variables | level1, level2, level3 |
| air quality index | int | variable | index |
| cutoff value | int | constant | CUTOFF |

#### 5.1.3.3 Operations

Again, from our behavioral description, we have the following operations:

- i. Output a string (prompt, descriptive label)
- ii. Read real values (level1, level2, level3) from the keyboard
- iii. Compute index from level1, level2, level3: add the levels, divide by 3, and round by adding 0.5
- iv. Output a numeric value (index) and a string (pollution condition) on the screen

#### 5.1.3.4 Algorithm

The next step is to organize these objects and operations into an algorithm:

- 1. Define the constant CUTOFF.
- 2. Display to cout a prompt for the three pollution levels.
- 3. Read three real values from cin into level1, level2, level3.
- 4. Compute index = (level1 + level2 + level3) / 3 + 0.5.

> ³ A real number can be rounded to the nearest integer by adding 0.5 and truncating the decimal part. In general, to round to the nearest nth decimal place, multiply by 10^n, add 0.5, truncate the decimal part, and divide by 10^n.

- 5. Output to cout a descriptive label and index.
- 6. Output to cout "Safe" if index < CUTOFF and "Hazardous" otherwise.

The program in Example 5.1 implements the preceding algorithm. Note the rounding of the average pollution reading in the computation of index.

### Example 5.1 Air Quality Indexes—Version 1

```
/* This program reads three pollution levels, calculates an air quality index (AQI) as their integer average, and then displays an appropriate air-quality message.

Input: the three pollution levels
Constant: the cutoff value (parts per million)
Output: the air quality index and a "safe condition" message if this index is less than the cutoff value, otherwise a "hazardous condition" message
*/

#include <iostream> // cin, cout, <<, >>
using namespace std;

int main()
{
const int CUTOFF = 50; // safe pollution level cutoff
double level1, level2, level3;
cout << "Enter 3 pollution readings (parts per million): ";
cin >> level1 >> level2 >> level3; // get pollution levels
int index = (level1 + level2 + level3) / 3 + 0.5; // compute AQI
cout << "AQI: " << index << " -- "; // display AQI
// display condition
if (index < CUTOFF)
cout << "Safe condition\n";
else
cout << "Hazardous condition\n";
}
```

```
Enter 3 pollution readings (parts per million): 30 40 50
AQI: 40 -- Safe condition

Enter 3 pollution readings (parts per million): 40 50 60
AQI: 50 -- Hazardous condition
```

```
Enter 3 pollution readings (parts per million): 44.5 53.8 61
AQI: 53 -- Hazardous condition
```

```
Enter 3 pollution readings (parts per million): 39.2 52 54.5
AQI: 49 -- Safe condition
```

The expression index < CUTOFF used in the if statement of the preceding program to determine which pollution condition to display is known as a boolean expression. Because they form such an essential part of selection and repetition structures, we will look next at boolean expressions in detail.

## 5.2 BOOLEAN EXPRESSIONS

In the mid-1800s, George Boole, a British mathematician and philosopher, developed a system of algebraic logic, which has since come to be known as boolean logic and is the basis for modern digital computer logic. The logical expressions in this system, which have either the value true or the value false, have thus come to be known as boolean expressions. In computing, they are also often called conditions.

All modern programming languages provide boolean expressions, and in this section we consider them in C++. We will consider simple boolean expressions first and then compound expressions constructed by applying logical operators to modify or to combine other boolean expressions.

### 5.2.1 Simple Boolean Expressions

The bool type has two literals, false and true, and boolean expressions have these as their values.⁴ The simplest boolean expressions test some relationship between two values such as whether one of them is less than the other. For example, the program in Example 5.1 contains the boolean expression

```
index < CUTOFF
```

which compares the operands index and CUTOFF using the less-than relationship, and produces the value true if the value of index is less than CUTOFF and the value false otherwise. Similarly, the boolean expression

```
count == 5
```

tests the equality relationship between the (variable) operand count and the (literal) operand 5, producing the value true if the value of count is 5 and the value false if it is not. Note: Be sure to use the == operator for equality comparisons and not = (assignment) because an error will almost surely result otherwise.⁵

> ⁴ For upward compatibility with C, integers may also be used as boolean values: 0 in place of false and any nonzero value for true, with 1 being the most common.

> ⁵ For example, in an if statement of the form if (x = 1) something, the "condition" x = 1 is actually an assignment expression and thus has the value 1, which represents true. Consequently, something will always be executed.
