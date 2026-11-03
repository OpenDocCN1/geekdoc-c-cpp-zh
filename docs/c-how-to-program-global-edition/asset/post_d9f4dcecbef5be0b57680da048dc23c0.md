
Your program must use only three output statements, one of each of the following forms:

```
printf("%s", "a ");
printf("%s", "b");
puts(" "); // outputs a newline
```

3.40 (Powers of 3 with an Infinite Loop) Write a program that keeps printing the powers of the integer 3, namely 3, 9, 27, 81, 243, and so on. Your loop should not terminate (i.e., you should create an infinite loop). What happens when you run this program?

3.41 (Diameter, Circumference and Area of a Circle) Write a program that reads the radius of a circle (as a float value) and computes and prints the diameter, the circumference and the area. Use the value 3.14159 for π.

3.42 What’s wrong with the following statement? Rewrite it to accomplish what the programmer was probably trying to do.

```
printf("%d", --(x * y));
```

3.43 (Sides of a Triangle) Write a program that reads three nonzero integer values and determines and prints whether they could represent the sides of a triangle.

3.44 (Sides of a Right Triangle) Write a program that reads three nonzero integers and determines and prints whether they could be the sides of a right triangle.

3.45 (Factorial) The factorial of a nonnegative integer n is written n! (pronounced "n factorial") and is defined as follows:

n! = n · (n - 1) · (n - 2) · ... · 1 (for values of n greater than or equal to 1)

and
n! = 1 (for n = 0).

For example, 5! = 5 · 4 · 3 · 2 · 1, which is 120.

- a) Write a program that reads a nonnegative integer and computes and prints its factorial.
- b) Write a program that estimates the value of the mathematical constant e by using the formula:
  e = 1 + 1/1! + 1/2! + 1/3! + ...
- c) Write a program that computes the value of e^x by using the formula
  e^x = 1 + x/1! + x^2/2! + x^3/3! + ...

## Making a Difference

3.46 (World-Population-Growth Calculator) Use the web to determine the current world population and the annual world population growth rate. Write an application that inputs these values, then displays the estimated world population after one, two, three, four and five years.

3.47 (Target-Heart-Rate Calculator) While exercising, you can use a heart-rate monitor to see that your heart rate stays within a safe range suggested by your trainers and doctors. According to the American Heart Association (AHA), the formula for calculating your maximum heart rate in beats per minute is 220 minus your age in years. Your target heart rate is a range that's 50-85% of your maximum heart rate. [Note: These formulas are estimates provided by the AHA. Maximum and target heart rates may vary based on the health, fitness and gender of the individual. Always consult a physician or qualified health-care professional before beginning or modifying an exercise program.] Create a program that reads the user's birthday and the current day (each consisting of the month, day and year). Your program should calculate and display the person's age (in years), the person's maximum heart rate and the person's target-heart-rate range.

## C Program Control

### Objectives

In this chapter, you'll learn:

- The essentials of counter-controlled iteration.
- To use the for and do...while iteration statements to execute statements repeatedly.
- To understand multiple selection using the switch selection statement.
- To use the break and continue statements to alter the flow of control.
- To use the logical operators to form complex conditional expressions in control statements.
- To avoid the consequences of confusing the equality and assignment operators.

### Outline

- 4.1 Introduction
- 4.2 Iteration Essentials
- 4.3 Counter-Controlled Iteration
- 4.4 for Iteration Statement
- 4.5 for Statement: Notes and Observations
- 4.6 Examples Using the for Statement
- 4.7 switch Multiple-Selection Statement
- 4.8 do...while Iteration Statement
- 4.9 break and continue Statements
- 4.10 Logical Operators
- 4.11 Confusing Equality (==) and Assignment (=) Operators
- 4.12 Structured Programming Summary
- 4.13 Secure C Programming

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Making a Difference*

### 4.1 Introduction

You should now be comfortable with writing simple, complete C programs. In this chapter, iteration is considered in greater detail, and additional iteration control statements, namely the for and the do...while, are presented. The switch multiple-selection statement is introduced. We discuss the break statement for exiting immediately from certain control statements, and the continue statement for skipping the remainder of the body of an iteration statement, then proceeding with the next iteration of the loop. The chapter discusses logical operators used for combining conditions, and summarizes the principles of structured programming as presented in Chapter 3 and this chapter.

### 4.2 Iteration Essentials

Most programs involve iteration, or looping. A loop is a group of instructions the computer executes repeatedly while some loop-continuation condition remains true. We’ve discussed two means of iteration:

- 1. Counter-controlled iteration
- 2. Sentinel-controlled iteration

Counter-controlled iteration is sometimes called *definite iteration* because we know *in advance* exactly how many times the loop will be executed. Sentinel-controlled iteration is sometimes called *indefinite iteration* because it’s *not known* in advance how many times the loop will be executed.

In counter-controlled iteration, a control variable is used to count the number of iterations. The control variable is incremented (usually by 1) each time the group of instructions is performed. When the value of the control variable indicates that the correct number of iterations has been performed, the loop terminates and execution continues with the statement after the iteration statement.

Sentinel values are used to control iteration when:

- 1. The precise number of iterations isn’t known in advance, and
- 2. The loop includes statements that obtain data each time the loop is performed.

The sentinel value indicates “end of data.” The sentinel is entered after all regular data items have been supplied to the program. Sentinels must be distinct from regular data items.

The statement

```
++counter; // increment
```

increments the loop counter by 1 each time the loop is performed. The loop-continuation condition in the while statement tests whether the value of the control variable is less than or equal to 10 (the last value for which the condition is true). The body of this while is performed even when the control variable is 10. The loop terminates when the control variable exceeds 10 (i.e., counter becomes 11).

You could make the program in Fig. 4.1 more concise by initializing counter to 0 and by replacing the while statement with

```
while (++counter <= 10) {
    printf("%d\n", counter);
}
```

This code saves a statement because the incrementing is done directly in the while condition before the condition is tested. Coding in such a condensed fashion takes some practice. Some programmers feel that this makes the code too cryptic and error prone.

> **Common Programming Error 4.1**
> 
> *Floating-point values may be approximate, so controlling counting loops with floating-point variables may result in imprecise counter values and inaccurate termination tests.*

> **Error-Prevention Tip 4.1**
> 
> *Control counting loops with integer values.*

> **Good Programming Practice 4.1**
> 
> *Too many levels of nesting can make a program difficult to understand. As a rule, try to avoid using more than three levels of nesting.*

> **Good Programming Practice 4.2**
> 
> *The combination of vertical spacing before and after control statements and indentation of the bodies of control statements within the control-statement headers gives programs a two-dimensional appearance that greatly improves program readability.*

### 4.4 for Iteration Statement

The for iteration statement handles all the details of counter-controlled iteration. To illustrate its power, let's rewrite the program of Fig. 4.1. The result is shown in Fig. 4.2. The program operates as follows. When the for statement begins executing, the control variable counter is defined and initialized to 1. Then, the loop-continuation condition counter <= 10 is checked. Because the initial value of counter is 1, the condition is satisfied, so the printf statement (line 10) prints the value of counter, namely 1. The control variable counter is then incremented by the expression ++counter, and the loop begins again with the loop-continuation test. Because the control variable is now equal to 2, the final value is not exceeded, so the program performs the printf statement again. This process continues until the control variable counter is incremented to its final value of 11—this causes the loop-continuation test to fail, and iteration terminates. The program continues by performing the first statement after the for statement (in this case, the program simply ends).
