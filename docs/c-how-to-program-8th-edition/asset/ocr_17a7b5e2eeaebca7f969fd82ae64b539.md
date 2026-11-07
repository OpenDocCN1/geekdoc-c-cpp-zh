# The pseudocode statement

```
Display a summary of the exam results and decide whether a bonus should be paid
```

can be refined as follows:

```
Display the number of passes
Display the number of failures
If more than eight students passed
    Display “Bonus to instructor”
```

The complete second refinement appears in Fig. 4.15. Blank lines set off the While structure for readability. This pseudocode is now sufficiently refined for conversion to C++.

```
1  Initialize passes to zero
2  Initialize failures to zero
3  Initialize student counter to one

5  While student counter is less than or equal to 10
6      Prompt the user to enter the next exam result
7      Input the next exam result

9      If the student passed
10         Add one to passes
11     Else
12         Add one to failures

14     Add one to student counter

16 Display the number of passes
17 Display the number of failures

19 If more than eight students passed
20     Display “Bonus to instructor”
```

**Fig. 4.15** | Pseudocode for examination-results problem.

# Conversion to Class Analysis

The program that implements the pseudocode algorithm is shown in Fig. 4.16. This example does not contain a class—it contains just a source code file with function main performing all the application’s work. In this chapter and in Chapter 3, you’ve seen examples consisting of one class (including the header and source code files for this class), as well as another source code file testing the class. This source code file contained function main, which created an object of the class and called its member functions. Occasionally, when it does not make sense to try to create a reusable class to demonstrate a concept, we’ll use an example contained entirely within the main function of a single source code file.

Lines 9–12 declare the variables used to process the examination results. We’ve taken advantage of a feature of C++ that allows variable initialization to be incorporated into