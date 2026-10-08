
## 5.13 Increment and Decrement Operators

```
Console.WriteLine(); // skip a line
// demonstrate prefix increment operator
c = 5; // assign 5 to c
Console.WriteLine("c before preincrement: {c}"); // displays 5
Console.WriteLine("c preincrementing: {++c}"); // displays 6
Console.WriteLine("c after postincrement: {c}"); // displays 6
```

| c before postincrement: 5 |
| postincrementing: c: 5 |
| after postincrement: 6 |
| c before preincrement: 5 |
| preincrementing: c: 6 |
| c after preincrement: 6 |

![](img/57baed2319be0bb1b5f98674846f2711_215_0.png)

Line 10 initializes the variable c to 5, and line 11 outputs c's initial value. Line 12 outputs the value of the c++. This expression postincrements the variable c, so c's original value (5) is output, then c is incremented (to 6). Thus, line 12 outputs c's initial value (5) again. Line 13 outputs c's new value (6) to prove that the variable's value was incremented in line 12.

Line 18 resets c's value to 5, and line 19 outputs c's preincrements. Line 20 outputs the value of the expression c++. This expression preincrements c, so its value is incremented; the new value (6) is output. Line 21 outputs c's value again to show that the value of c is still 6 after line 20 executes.

### 5.13.2 Simplifying Increment Statements

The arithmetic compound assignment operators and the increment and decrement operators can be used to simplify statements. For example, the three assignment statements in Fig. 5.13 (lines 24, 28 and 32)

```
passes += 1;
failures = failures + 1;
studentCounter = studentCounter + 1;
```

can be written more concisely with compound assignment operators

```
passes += 1;
failures += 1;
studentCounter += 1;
```

and even more concisely with prefix-increment operators

```
++passes;
++failures;
++studentCounter;
```

or with postfix-increment operators as

```
passes++;
failures++;
studentCounter++;
```

When incrementing or decrementing a variable in a statement by itself, the prefix increment and postfix increment forms have the same effect, and the prefix decrement and postfix decrement forms have the same effect. It's only when a variable appears in the context of a larger expression that the prefix increment and postfix increment have different results (and similarly for prefix decrement and postfix decrement).

## Common Programming Error 5.5

Attempting to use the increment or decrement operator on an expression other than one to a value which can be assigned is a syntax error. For example, ++(x + 1) is a syntax error, where (x+1) is not an expression to which a value can be assigned.

## 5.13.3 Operator Precedence and Associativity

Figure 5.17 shows the precedence and associativity of the operators introduced to this point. The operators are shown from top to bottom in decreasing order of precedence. The second column describes the associativity of the operators at each level of precedence. The conditional operator (?); the unary operators prefix increment (++), prefix decrement (-), plus (+) and minus (-); the cast operators; and the assignment operators, +=, -=, /= from right to right. All the other operators in the operator precedence chart in Figure 5.17 associate from left to right. The third column names the group of operators.

| Operators | Associativity | Type |
| :--- | :--- | :--- |
| new ++(postfix) --(postfix) | left to right | highest precedence |
| ++ - + (type) | right to left | unary prefix |
| * / % | left to right | multiplicative |
| < >= | left to right | additive |
| < <= | left to right | relational |
| ! = | left to left | equality |
| ?: | right to left | conditional |
| = += -= *= /= % | right to left | assignment |

**Figure 5.17** Precedence and associativity of the operators discussed so far.

## 5.14 Simple Types

The table in Appendix B lists C#'s 13 simple types. Like its predecessor languages C and C++, C# requires all variables to have a type.

In C and C++, you frequently have to write separate versions of apps to support different computer platforms, because the simple types are not guaranteed to be identical from computer to computer. For example, an int value on one machine might be represented by 16 bits (2 bytes) of storage, while an int value on another machine might be represented by 32 bits (4 bytes) of storage. In C#, int values are always 32 bits (4 bytes). In fact, all C numeric types have fixed sizes, as is shown in Appendix B.

Each type in Appendix B is listed with its size in bytes (there are eight bits to a byte) and its range of values. Because the designers of C# want it to be portable, they used internationally recognized standards for both character formats (Unicode: http://unicode.org) and floating-point numbers (IEEE 754; http://grouper.ieee.org/754/).

Recall that variables of simple types declared outside of a method as instance variables of a class are automatically assigned default values unless initialized. Instance variables of types char, byte, short, ushort, int, uint, long, float, double, and decimal are all given the value 0 by default. Instance variables of type bool are given the value false by default. Similarly, reference-type instance variables are initialized by the value null.

## 5.15 Wrap-Up

This chapter presented basic problem-solving techniques that you will use in building classes and developing methods for these classes. We demonstrated how to construct an algorithm, then how to refine the algorithm through several phases of pseudocode development, resulting in C# code that can be executed as part of a method. The chapter showed how to use top-down, stepwise refinement to plan out the specific actions that a method must perform and the order in which the method must perform these actions.

Only three types of control statements—sequence, selection and iteration—are needed to develop any algorithm. Specifically, we demonstrated the if and if...else selection statements and the while iteration statement. These are some of the building blocks used to construct apps. We used control-statement stacking to compute the total and the average of a set of students with grade counter and sentinel-controlled iteration, and we used control-statement nesting to analyze and make decisions on a set of exam results. We introduced C#'s compound assignment, unary cast, conditional (?), increment and decrement operators. Finally, we discussed the simple types. In Chapter 6, we continue our discussion of control statements, introducing the for, do...while and switch statements.

## Summary

## Section 5.2 Algorithms

- An algorithm is a procedure for solving a problem in the actions to execute and the order in which these actions execute.
- Specifying the order in which statements (actions) execute in an app is called program control.

## Section 5.3 Pseudocode

Pseudocode is an informal language that helps you develop algorithms without having to worry about the strict details of C# language syntax.

- Carefully prepared pseudocode can be converted to a corresponding C# app.

## Section 5.4 Control Structures

- There are three types of control structures—sequence, selection, and iteration.

### 5.4.1 Sequence Structure

- The sequence structure is built into C#. Unless otherwise, the computer executes C# statements one after the other in the order which they are written.
- Activity diagrams are part of the UML. An activity diagram models the workflow of a portion of software system.
- Activity diagrams are composed of special-purpose symbols, such as action-state symbols, diamonds and small circles. These symbols are connected by transition arrows, which represent the flow of the activity.
- Like pseudocode, activity diagrams help you develop and represent algorithms. Activity diagrams clearly show how control structures operate.
- Action-state symbols (rectangles with their left and right sided with arcs outward) represent actions to perform.
- The arrows in an activity diagram represent transitions, which indicate the order in which the actions represented by the state occurs.
- The solid circle in activity diagram represents the activity's initial state. The solid circle surrounded by a hollow circle represents the final state.
- Rectangles with the upper-right corners folded over are UML notes (like comments in C#)—explanatory remarks that describe the purpose of symbols.

### 5.4.2 Selection Statements

- C# has three types of selection statements: the if, if...else statement and the switch statement.
- The if statement is called a single-selection statement because it selects or ignores a single action (or group of actions).
- The if...else statement is called a double-selection statement because it selects between two different actions (or groups of actions).
- The switch statement is called a multiple-selection statement because it selects among many different actions (or groups of actions).

### 5.4.3 Iteration Statements

- C provides four iteration statements: the while, do...while, and for foreach statements.
- The while, and for foreach statements perform the actions in their bodies zero or more times.
- The do...while statement performs the actions in its body one or more times.

### 5.4.4 Summary of Control Statements

- Control statements may be connected in two ways: control-state stacking and control-state-nesting.

## 5.5 if Single-Selection Statement

- The if-selection statement performs an indicated action (or group of actions) only when the condition is true; otherwise, the action is skipped.
