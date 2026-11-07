
## 14 Exception Handling

In this chapter we concentrate on *exception handling*, which is the C++ terminology for error handling. We define the concept and then show how it can be implemented using classes. We also discuss library exception classes, which can be used in our programs.

**Objectives**

After you have read and studied this chapter, you should be able to:

- Discuss traditional approaches to error handling.
- Discuss exception handling in a function using three different patterns that use *try-catch* block and *throw* statements.
- Discuss exception specifications to define what type of an exception a function can throw, including any exception, predefined exceptions, and no exception.
- Discuss the process of stack unwinding and its effect on catching exceptions.
- Discuss exceptions in classes and how exceptions should be handled in constructors using a version of *try-catch* block called *function-try* block.
- Emphasize that we should avoid exceptions in destructors because they undermine the process of stack unwinding.
- Discuss the general layout and format of standard exception classes in C++, and discuss their public interfaces and their purposes.
- Show how we can create our own exception classes that are inherited from the standard exception classes.

### 14.1 INTRODUCTION

When we write source code, we expect that there could be some errors during the compilation. Many new programmers, however, think that if a program compiles successfully, everything is fine. Experienced programmers, on the other hand, are not happy until they test each program with a predetermined set of test data. Even when a complete scheduled testing phase is used, an occasional error can occur when the program is run. An error like this is referred to as an exception because it is rare. The subject of this chapter is how to handle these exceptions.

#### 14.1.1 Traditional Approaches to Error Handling

Run-time errors are problematic. If there are no syntactical errors, the program will be compiled, but a run-time error occurs that prevents the continuation of the program with the result that the program must be aborted. There are several approaches that are often used to deal with run-time errors. We discuss four here.

##### Let Run-Time Environment Abort the Program

The first approach is to do nothing and let the program terminate when there is an exception.

**EXAMPLE 14.1**

In this example we write a simple program that takes two integers from the user, divides the first by the second, and prints the result. The program repeats the calculations up to five times, as shown in Program 14.1.

The program compiles with no errors because there are no compile-time errors. When we run the program, the loop is supposed to repeat five times, taking five pairs of integers, dividing the first by the second, and printing the result. Everything goes well with the first and second iterations, but in the third iteration, the program aborted (without an error message) because we entered 0 for the second integer and the C++ run-time system does not allow division by 0. The loop is prematurely terminated and the program is aborted.

**Program 14.1** Dividing two integers

```cpp
/************************************************************
 * The program shows how division by zero aborts the program. *
 ************************************************************/
#include <iostream>
using namespace std;

int main ()
{
    int num1, num2, result;
    for (int i = 0; i < 5; i++)
    {
        cout << "Enter an integer: ";
        cin >> num1;
        cout << "Enter another integer: ";
        cin >> num2;
        result = num1 / num2;   // The statement that may create exception.
        cout << "The result of division is: " << result << endl;
    }
    return 0;
}
```

```text
Run:
Enter an integer: 12
Enter another integer: 5
The result of division is: 2
Enter an integer: 10
Enter another integer: 3
The result of division is: 3
Enter an integer: 6
Enter another integer: 0
```

After two iterations, the program is aborted, but we print a message that explains what happened. Again the program is aborted by the run-time environment, but we told the run-time system to abort it by using the *assert* macro.

##### Use Error Checking

A third approach is to check the value of the second number in each iteration and skip the division if it is zero. This is preferred to the previous two methods because we can skip the cases in which the second number is zero and continue with the other cases.

**EXAMPLE 14.3**

Since we know that the program will be aborted if the divisor is zero, we can use an *if/else* statement and perform the division only if the divisor is not zero. Program 14.3 shows this approach.

**Program 14.3** A traditional error-checking program

```cpp
/*********************************************************
 * A program that uses traditional error checking to prevent        *
 * program abortion                                                 *
 *********************************************************/
#include <iostream>
using namespace std;

int main( )
{
    int num1, num2, result;
    for (int i = 0; i < 4; i++)
    {
        cout << "Enter an integer: ";
        cin >> num1;
        cout << "Enter another integer: ";
        cin >> num2;
        if (num2 == 0)
        {
            cout << "Division cannot be done in this case." << endl;
        }
        else
        {
            result = num1 / num2;
            cout << "The result of division is: " << result << endl;
        }
    }
    return 0;
}
```

```text
Run:
Enter an integer: 8
Enter another integer: 2
The result of division is: 4
Enter an integer: 7
Enter another integer: 1
The result of division is: 7
Enter an integer: 8
Enter another integer: 0
Division cannot be done in this case.
Enter an integer: 9
Enter another integer: 7
The result of division is: 1
```

The calculation is done in the highlighted section of the program (lines 17 to 25). If the calculation cannot be done, it is skipped. The loop continues with the rest of the data.

##### Using Function Return Value for Error Checking

A fourth approach involves functions. Execution of a statement in a C++ program always occurs in a function, not outside of a function. We may initialize variables outside a function (in the global area), but initialization is not execution; if there is a problem with the initialization, it is detected by the compiler. Since execution always occurs in a function, we can say that the run-time error always occurs in a function. In procedural programming in the past, it was customary to perform each calculation in a function and to check for errors by checking the return value of the function. An example is the *main* function, which returns 0 if there is no problem and returns other values if there is a problem. Programmers in the past used this idea and designed programs in which each function returned a specific value if there was an error.

**EXAMPLE 14.4**

In this example we rewrite our previous program using the return value of a function for error checking, as shown in Program 14.4.

**Program 14.4** Error checking using a function

```cpp
/*
 * A program that uses the return value of a function to show
 * the occurrence of a run-time error
 */
#include <iostream>
using namespace std;

// Function declaration
int quotient (int first, int second);

11 int main ()
12 {
13     int num1, num2, result;
14     for (int i = 0; i < 3; i++)
15     {
16         cout << "Enter an integer: ";
17         cin >> num1;
18         cout << "Enter another integer: ";
19         cin >> num2;
20         result = quotient (num1, num2);
21         if (result == -1)
22         {
23             cout << "Error, division by zero." << endl;
24         }
25         else
26         {
27             cout << "Result of division is: " << result << endl;
28         }
29     }
30     return 0;
31 }
32
33 // Function definition
34 int quotient (int first, int second)
35 {
36     if (second == 0)
37     {
38         return -1;
39     }
40     return (first / second);
41 }
```

```text
Run:
Enter an integer: 6
Enter another integer: 5
The result of division is: 1
Enter an integer: 7
Enter another integer: 0
Error, division by zero.
Enter an integer: 8
Enter another integer: 2
The result of division is: 4
```

Note that when the quotient is zero, the program prints an error message instead of printing the result of the calculation.
