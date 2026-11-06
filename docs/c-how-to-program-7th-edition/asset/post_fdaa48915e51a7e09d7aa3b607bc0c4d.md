
can be refined as follows:

```
Initialize passes to zero
Initialize failures to zero
Initialize student counter to one
```

Notice that only the counters are initialized at the start of the algorithm.

The pseudocode statement

```
Input the 10 exam results, and count passes and failures
```

requires a loop that successively inputs the result of each exam. Here it’s known in advance that there are precisely 10 exam results, so counter-controlled looping is appropriate. Inside the loop (i.e., nested within the loop), an if...else statement will determine whether each exam result is a pass or a failure and will increment the appropriate counter. The refinement of the preceding pseudocode statement is then

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

We use blank lines to isolate the If...Else control structure, which improves readability.

The pseudocode statement

```
Print a summary of the exam results and decide whether tuition should be raised
```

can be refined as follows:

```
Print the number of passes
Print the number of failures
If more than eight students passed
    Print "Bonus to instructor!"
```

The complete second refinement appears in Fig. 4.15. Blank lines are used to set off the While structure for readability. This pseudocode is now sufficiently refined for conversion to C++.

```
1    Initialize passes to zero
2    Initialize failures to zero
3    Initialize student counter to one

5    While student counter is less than or equal to 10
6       Prompt the user to enter the next exam result
7       Input the next exam result

9       If the student passed
10         Add one to passes
11      Else
12         Add one to failures

14      Add one to student counter

16      Print the number of passes
17      Print the number of failures

19      If more than eight students passed
20         Print "Bonus to instructor!"
```

Fig. 4.15 | Pseudocode for examination-results problem.

## Conversion to C++

The program that implements the pseudocode algorithm and two sample executions are shown in Fig. 4.16.

```cpp
  1   // Fig. 4.16: fig04_16.cpp
  2   // Examination-results problem: Nested control statements.
  3   #include <iostream>
  4   using namespace std;

  6   int main()
  7   {
  8      // initializing variables in declarations
  9      int passes = 0; // number of passes
 10      int failures = 0; // number of failures
 11      int studentCounter = 1; // student counter
 12      int result; // one exam result (1 = pass, 2 = fail)

 14      // process 10 students using counter-controlled loop
 15      while ( studentCounter <= 10 )
 16      {
 17         // prompt user for input and obtain value from user
 18         cout << "Enter result (1 = pass, 2 = fail): ";
 19         cin >> result; // input result

 21         // if...else nested in while
 22         if ( result == 1 )           // if result is 1,
 23            passes = passes + 1;      // increment passes;
 24         else
 25            failures = failures + 1;  // increment failures

 27         // increment studentCounter so loop eventually terminates
 28         studentCounter = studentCounter + 1;
 29      } // end while

 31      // termination phase; display number of passes and failures
 32      cout << "Passed " << passes << "\nFailed " << failures << endl;

 34      // determine whether more than eight students passed
 35      if ( passes > 8 )
 36         cout << "Bonus to instructor!" << endl;
 37   } // end main
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
Bonus to instructor!
```

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

Fig. 4.16 | Examination-results problem: Nested control statements.

Lines 9–12 declare the variables used to process the examination results. We’ve taken advantage of a feature of C++ that allows variable initialization to be incorporated into declarations (passes is initialized to 0, failures is initialized to 0 and studentCounter is initialized to 1). Looping programs may require initialization at the beginning of each repetition; such reinitialization normally would be performed by assignment statements rather than in declarations or by moving the declarations inside the loop bodies.

The while statement (lines 15–29) loops 10 times. Each iteration inputs and processes one exam result. The if...else statement (lines 22–25) for processing each result is nested in the while statement. If the result is 1, the if...else statement increments passes; otherwise, it assumes the result is 2 and increments failures. Line 28 increments studentCounter before the loop condition is tested again in line 15. After 10 values have been input, the loop terminates and line 32 displays the number of passes and the number of failures. The if statement in lines 35–36 determines whether more than eight students passed the exam and, if so, outputs the message "Bonus to instructor!".

Figure 4.16 shows the input and output from two sample executions of the program. At the end of the first sample execution, the condition in line 35 is true—more than eight students passed the exam, so the program outputs a message indicating that the instructor should receive a bonus.

## 4.11 Assignment Operators

C++ provides several assignment operators for abbreviating assignment expressions. For example, the statement

```
c = c + 3;
```

can be abbreviated with the addition assignment operator += as

```
c += 3;
```

The += operator adds the value of the expression on the right of the operator to the value of the variable on the left of the operator and stores the result in the variable on the left of the operator. Any statement of the form

```
variable = variable operator expression;
```

in which the same variable appears on both sides of the assignment operator and operator is one of the binary operators +, −, *, /, or % (or others we’ll discuss later in the text), can be written in the form

```
variable operator= expression;
```

Thus the assignment c += 3 adds 3 to c. Figure 4.17 shows the arithmetic assignment operators, sample expressions using these operators and explanations.

| Assignment operator | Sample expression | Explanation | Assigns |
|---|---|---|---|
| *Assume: int c = 3, d = 5, e = 4, f = 6, g = 12* |  |  |  |
| += | c += 7 | c = c + 7 | 10 to c |
| -= | d -= 4 | d = d - 4 | 1 to d |
| *= | e *= 5 | e = e * 5 | 20 to e |
| /= | f /= 3 | f = f / 3 | 2 to f |
| %= | g %= 9 | g = g % 9 | 3 to g |

Fig. 4.17  |  Arithmetic assignment operators.

## 4.12 Increment and Decrement Operators

In addition to the arithmetic assignment operators, C++ also provides two unary operators for adding 1 to or subtracting 1 from the value of a numeric variable. These are the unary increment operator, ++, and the unary decrement operator, --, which are summarized in Fig. 4.18. A program can increment by 1 the value of a variable called c using the increment operator, ++, rather than the expression c = c + 1 or c += 1. An increment or decrement operator that is prefixed to (placed before) a variable is referred to as the **prefix increment** or **prefix decrement operator**, respectively. An increment or decrement operator that is postfixed to (placed after) a variable is referred to as the **postfix increment** or **postfix decrement operator**, respectively.

| Operator | Called | Sample expression | Explanation |
|---|---|---|---|
| ++ | preincrement | ++a | Increment a by 1, then use the new value of a in the expression in which a resides. |
| ++ | postincrement | a++ | Use the current value of a in the expression in which a resides, then increment a by 1. |
| -- | predecrement | --b | Decrement b by 1, then use the new value of b in the expression in which b resides. |
| -- | postdecrement | b-- | Use the current value of b in the expression in which b resides, then decrement b by 1. |

Fig. 4.18 | Increment and decrement operators.

Using the prefix increment (or decrement) operator to add (or subtract) 1 from a variable is known as preincrementing (or predecrementing) the variable. Preincrementing (or predecrementing) causes the variable to be incremented (decremented) by 1, then the new value of the variable is used in the expression in which it appears. Using the postfix increment (or decrement) operator to add (or subtract) 1 from a variable is known as postincrementing (or postdecrementing) the variable. Postincrementing (or postdecrementing) causes the current value of the variable to be used in the expression in which it appears, then the variable’s value is incremented (decremented) by 1.

> **Good Programming Practice 4.9**
> 
> *Unlike binary operators, the unary increment and decrement operators should be placed next to their operands, with no intervening spaces.*

![](img/023f159fdd47d944d48e08843cea732d_181_0.png)

Figure 4.19 demonstrates the difference between the prefix increment and postfix increment versions of the ++ increment operator. The decrement operator (--) works similarly. This example does not contain a class—it contains just a source code file with function main performing all the application’s work. In this chapter and in Chapter 3, you’ve seen examples consisting of one class (including the header and source code files for this class), as well as another source code file testing the class. This source code file contained function main, which created an object of the class and called its member functions. In this example, we simply want to show the mechanics of the ++ operator, so we use only one source code file with function main. Occasionally, when it does not make sense to try to create a reusable class to demonstrate a simple concept, we’ll use a mechanical example contained entirely within the main function of a single source code file.
