# Chapter 5 Algorithm Development and Control Statements: Part I

```
While student counter is less than or equal to 10
Prompt the user to enter the next exam result
Input the next exam result
```

```
If the student passed
Add one to passes
Else
Add one to failures
Add one to student counter
```

We use blank lines to isolate the if...else control statement, which improves readability. The pseudocode statement

```
Display a summary of the exam results and decide if the instructor should receive a bonus
```

can be refined as follows:

```
Display the number of passes
Display the number of failures
If more than eight students passed
Display "Bonus to instructor!"
```

# 5.11.5 Complete Second Refinement of the Pseudocode

The complete second of the pseudocode appears in Fig. 5.12. Notice that blank lines are used to set off the while statement for readability. This pseudocode is now sufficiently refined for conversion to C#. The program that implements the pseudocode algorithm and sample outputs are shown in Fig. 5.13.

```
1 Initialize passes to zero
2 Initialize failures to zero
3 Initialize student counter to one
4
5 While student counter is less than or equal to 10
6 Prompt the user to enter the next exam result
7 Input the next exam result
8
9 If the student passed
10 Add one to passes
11 Else
12 Add one to failures
13
14
15 Add one to student counter
```

> Fig. 5.12 | Pseudocode for the examination-results problem. (Part 1 of 2.)