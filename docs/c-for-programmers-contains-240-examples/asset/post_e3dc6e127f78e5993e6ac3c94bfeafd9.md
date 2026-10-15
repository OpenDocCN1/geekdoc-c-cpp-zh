
**Fig. 4.12** | Examination-results problem: Analysis header file. (Part 2 of 2.)

```cpp
8  public:
9      void processExamResults(); // process 10 students' examination results
10 }; // end class Analysis
```

**Fig. 4.13** | Examination-results problem: Nested control statements in Analysis source code file.

```cpp
1  // Fig. 4.13: Analysis.cpp
2  // Member-function definitions for class Analysis that
3  // analyzes examination results.
4  #include <iostream>
5  using std::cout;
6  using std::cin;
7  using std::endl;
8  
9  // include definition of class Analysis from Analysis.h
10 #include "Analysis.h"
11 
12 // process the examination results of 10 students
13 void Analysis::processExamResults()
14 {
15     // initializing variables in declarations
16     int passes = 0; // number of passes
17     int failures = 0; // number of failures
18     int studentCounter = 1; // student counter
19     int result; // one exam result (1 = pass, 2 = fail)
20 
21     // process 10 students using counter-controlled loop
22     while ( studentCounter <= 10 )
23     {
24         // prompt user for input and obtain value from user
25         cout << "Enter result (1 = pass, 2 = fail): ";
26         cin >> result; // input result
27 
28         // if...else nested in while
29         if ( result == 1 )      // if result is 1,
30             passes = passes + 1;    // increment passes;
31         else                    // else result is not 1, so
32             failures = failures + 1; // increment failures
33 
34         // increment studentCounter so loop eventually terminates
35         studentCounter = studentCounter + 1;
36     } // end while
37 
38     // termination phase; display number of passes and failures
39     cout << "Passed " << passes << "\nFailed " << failures << endl;
40 
41     // determine whether more than eight students passed
42     if ( passes > 8 )
43         cout << "Raise tuition " << endl;
44 } // end function processExamResults
```

Lines 16–18 of Fig. 4.13 declare the variables that member function `processExamResults` of class `Analysis` uses to process the examination results. Note that we have taken advantage of a feature of C++ that allows variable initialization to be incorporated into declarations (`passes` is initialized to 0, `failures` is initialized to 0 and `studentCounter` is initialized to 1). Looping programs may require initialization at the beginning of each repetition; such reinitialization normally would be performed by assignment statements rather than in declarations or by moving the declarations inside the loop bodies.

The `while` statement (lines 22–36) loops 10 times. During each iteration, the loop inputs and processes one exam result. Notice that the `if…else` statement (lines 29–32) for processing each result is nested in the `while` statement. If the result is 1, the `if…else` statement increments `passes`; otherwise, it assumes the result is 2 and increments `failures`. Line 35 increments `studentCounter` before the loop condition is tested again in line 22. After 10 values have been input, the loop terminates and line 39 displays the number of passes and the number of failures. The `if` statement in lines 42–43 determines whether more than eight students passed the exam, and, if so, outputs the message "Raise tuition".

## Demonstrating Class Analysis

Figure 4.14 creates an `Analysis` object (line 7) and invokes the object’s `processExamResults` member function (line 8) to process a set of exam results entered by the user. Figure 4.14 shows the input and output from two sample executions of the program. At the end of the first sample execution, the condition in line 42 of member function `processExamResults` in Fig. 4.13 is true—more than eight students passed the exam, so the program outputs a message indicating that the tuition should be raised.

```cpp
// Fig. 4.14: fig04_14.cpp
// Test program for class Analysis.
#include "Analysis.h" // include definition of class Analysis

int main()
{
    Analysis application; // create Analysis object
    application.processExamResults(); // call function to process results
    return 0; // indicate successful termination
} // end main
```

```text
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed 9
Failed 1
Raise tuition
```

**Fig. 4.14** | Test program for class `Analysis`. (Part 1 of 2.)

```text
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Passed 6
Failed 4
```

**Fig. 4.14** | Test program for class `Analysis`. (Part 2 of 2.)

## 4.9 Assignment Operators

C++ provides several *assignment operators* for abbreviating assignment expressions. For example, the statement

```cpp
c = c + 3;
```

can be abbreviated with the *addition assignment operator +=* as

```cpp
c += 3;
```

The += operator adds the value of the expression on the right of the operator to the value of the variable on the left of the operator and stores the result in the variable on the left of the operator. Any statement of the form

```
variable = variable operator expression;
```

in which the same *variable* appears on both sides of the assignment operator and *operator* is one of the binary operators `+`, `-`, `*`, `/`, or `%` (or others we'll discuss later in the text), can be written in the form

```
variable operator= expression;
```

Thus the assignment `c += 3` adds 3 to c. Figure 4.15 shows the arithmetic assignment operators, sample expressions using these operators and explanations.

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: `int c = 3, d = 5, e = 4, f = 6, g = 12;`* |  |  |  |
| `+=` | `c += 7` | `c = c + 7` | 10 to c |
| `-=` | `d -= 4` | `d = d - 4` | 1 to d |
| `*=` | `e *= 5` | `e = e * 5` | 20 to e |
| `/=` | `f /= 3` | `f = f / 3` | 2 to f |
| `%=` | `g %= 9` | `g = g % 9` | 3 to g |

**Fig. 4.15** | Arithmetic assignment operators.

## 4.10 Increment and Decrement Operators

In addition to the arithmetic assignment operators, C++ also provides two unary operators for adding 1 to or subtracting 1 from the value of a numeric variable. These are the unary increment operator, `++`, and the unary decrement operator, `--`, which are summarized in Fig. 4.16. A program can increment by 1 the value of a variable called `c` using the increment operator, `++`, rather than the expression `c = c + 1` or `c += 1`. An increment or decrement operator that is prefixed to (placed before) a variable is referred to as the prefix increment or prefix decrement operator, respectively. An increment or decrement operator that is postfixed to (placed after) a variable is referred to as the postfix increment or postfix decrement operator, respectively.

Using the prefix increment (or decrement) operator to add (or subtract) 1 from a variable is known as preincrementing (or predecrementing) the variable. Preincrementing (or predecrementing) causes the variable to be incremented (decremented) by 1, then the new value of the variable is used in the expression in which it appears. Using the postfix increment (or decrement) operator to add (or subtract) 1 from a variable is known as postincrementing (or postdecrementing) the variable. Postincrementing (or postdecrementing) causes the current value of the variable to be used in the expression in which it appears, then the variable’s value is incremented (decremented) by 1.

Figure 4.17 demonstrates the difference between the prefix increment and postfix increment versions of the `++` increment operator. The decrement operator (`--`) works similarly. Note that this example does not contain a class, but just a source code file with function `main` performing all the application’s work. In this chapter and in Chapter 3, you have seen examples consisting of one class (including the header and source code files for this class), as well as another source code file testing the class. This source code file contained function `main`, which created an object of the class and called its member functions. In this example, we simply want to show the mechanics of the `++` operator, so we use only one source code file with function `main`. Occasionally, when it does not make sense to try to create a reusable class to demonstrate a simple concept, we’ll use a mechanical example contained entirely within the `main` function of a single source code file.

| Operator | Called | Sample expression | Explanation |
|---|---|---|---|
| `++` | preincrement | `++a` | Increment `a` by 1, then use the new value of `a` in the expression in which `a` resides. |
| `++` | postincrement | `a++` | Use the current value of `a` in the expression in which `a` resides, then increment `a` by 1. |
| `--` | predecrement | `--b` | Decrement `b` by 1, then use the new value of `b` in the expression in which `b` resides. |
| `--` | postdecrement | `b--` | Use the current value of `b` in the expression in which `b` resides, then decrement `b` by 1. |

**Fig. 4.16** | Increment and decrement operators.
