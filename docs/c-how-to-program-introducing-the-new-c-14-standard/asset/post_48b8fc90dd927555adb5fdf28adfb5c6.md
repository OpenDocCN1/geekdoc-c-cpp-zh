
```
Input the 10 exam results, and count passes and failures
```

requires a loop that successively inputs the result of each exam. We know in advance that there are precisely 10 exam results, so counter-controlled looping is appropriate. Inside the loop (i.e., nested within the loop), a double-selection structure will determine whether each exam result is a pass or a failure and will increment the appropriate counter. The refinement of the preceding pseudocode statement is then

```
While student counter is less than or equal to 10
    Prompt the user to enter the next exam result
    Input the next exam result
    If the student passed
        Add one to passes
    Else
        Add one to failures
    Add one to student counter
```

We use blank lines to isolate the If…Else control structure, which improves readability.

The pseudocode statement

```text
Print a summary of the exam results and decide whether a bonus should be paid
```

can be refined as follows:

```text
Print the number of passes

Print the number of failures

If more than eight students passed
    Print "Bonus to instructor!"
```

## 4.11.5 Complete Second Refinement of the Pseudocode

The complete second refinement appears in **Fig. 4.13**. Notice that blank lines are also used to set off the *While* structure for program readability. This pseudocode is now sufficiently refined for conversion to C++.

```
1  Initialize passes to zero
2  Initialize failures to zero
3  Initialize student counter to one

4
5  While student counter is less than or equal to 10
6      Prompt the user to enter the next exam result
7      Input the next exam result

8
9      If the student passed
10         Add one to passes
11     Else
12         Add one to failures

13
14     Add one to student counter

15
16 Print the number of passes
17 Print the number of failures

18
19 If more than eight students passed
20     Print "Bonus to instructor!"
```

Fig. 4.13 Pseudocode for examination-results problem.

## 4.11.6 Program That Implements the Pseudocode Algorithm

The program that implements the pseudocode algorithm and two sample executions are shown in **Fig. 4.14**. Lines 8–10 and 16 of `main` declare the variables that are used to process the examination results.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_471_0.png)

### Error-Prevention Tip 4.4

> Initializing local variables when they’re declared helps you avoid any compilation warnings that might arise from attempts to use uninitialized variables and helps you avoid logic errors from using uninitialized variables.

```cpp
// Fig. 4.14: Analysis.cpp
// Analysis of examination results using nested control statements.
#include <iostream>
using namespace std;

int main() {
    // initializing variables in declarations
    unsigned int passes{0};
    unsigned int failures{0};
    unsigned int studentCounter{1};

    // process 10 students using counter-controlled loop
    while (studentCounter <= 10) {
        // prompt user for input and obtain value from user
        cout << "Enter result (1 = pass, 2 = fail): ";
        int result;
        cin >> result;

        // if...else is nested in the while statement
        if (result == 1) {
            passes = passes + 1;
        }
        else {
            failures = failures + 1;
        }

        // increment studentCounter so loop eventually terminates
        studentCounter = studentCounter + 1;
    }

    // termination phase; prepare and display results
    cout << "Passed: " << passes << "\nFailed: " << failures << endl;

    // determine whether more than 8 students passed
    if (passes > 8) {
        cout << "Bonus to instructor!" << endl;
    }
}
```

```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 9
Failed: 1
Bonus to instructor!
```

```
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 2
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Enter result (1 = pass, 2 = fail): 1
Passed: 6
Failed: 4
```

**Fig. 4.14** Analysis of examination results using nested control statements.

The `while` statement (lines 13–29) loops 10 times. During each iteration, the loop inputs and processes one exam result. Notice that the `if...else` statement (lines 20–25) for processing each result is **nested** in the `while` statement. If the `result` is `1`, the `if...else` statement increments `passes`; otherwise, it assumes the `result` is `2` and increments `failures`. Line 28 increments `studentCounter` before the loop condition is tested again at line 13. After 10 values have been input, the loop terminates and line 32 displays the number of `passes` and `failures`. The `if` statement at lines 35–37 determines whether more than eight students passed the exam and, if so, outputs the message `"Bonus to instructor!"`

**Figure 4.14** shows the input and output from two sample program executions. During the first, the condition at line 35 is *true*—more than eight students passed the exam, so the program outputs a message to bonus the instructor.

## 4.11.7 Preventing Narrowing Conversions with List Initialization

As you learned in **Chapter 2**, C++11 introduced list initialization so that you can use one syntax to initialize a variable of any type. Consider line 10 of **Fig. 4.14**:

```cpp
unsigned int studentCounter{1};
```

You also can write this as

```cpp
unsigned int studentCounter = {1};
```

though the form without `=` is preferred. Prior to C++11, you would have written this as

```cpp
unsigned int studentCounter = 1;
```

For fundamental-type variables, list-initialization syntax *prevents* **narrowing conversions** that could result in *data loss*. For example, previously you could write

```cpp
int x = 12.7;
```

which attempts to assign the `double` value `12.7` to the `int` variable `x`. In this case, C++ converts the `double` value to an `int`, by *truncating* the floating-point part (`.7`), a *narrowing conversion* that loses data. The actual value assigned to `x` is `12`. Many compilers warn you of this, but still allow the statement to compile. However, using list initialization, as in

```cpp
int x{12.7};
```

or

```cpp
int x = {12.7};
```

yields a *compilation* error, thus helping you avoid a potentially subtle logic error. For example, Apple’s Xcode LLVM compiler gives the error

```text
Type 'double' cannot be narrowed to 'int' in initializer list
```

We’ll discuss additional list-initializer features in later chapters.

### *A Look Back at* **Fig. 4.10**

You might think that the following statement from **Fig. 4.10**

```cpp
int average(total / 10); // int division yields int result
```

contains a narrowing conversion, but `total` and `10` are both `int` values, so the initializer value is an `int`. If in the preceding statement `total` were a `double` variable or if we used the `double` literal value `10.0`, then the initializer value would have type `double`. In this case the compiler would issue an error message due to an attempted narrowing conversion.

## 4.12 Compound Assignment Operators

The **compound assignment operators** abbreviate assignment expressions. Statements like

```
variable = variable operator expression;
```

where *operator* is one of the binary operators **+**, **-**, **\***, **/** or **%** (or others we discuss later in the text) can be written in the form

```
variable operator= expression;
```

For example, you can abbreviate the statement

```
c = c + 3;
```

with the **addition compound assignment operator**, **+=**, as
