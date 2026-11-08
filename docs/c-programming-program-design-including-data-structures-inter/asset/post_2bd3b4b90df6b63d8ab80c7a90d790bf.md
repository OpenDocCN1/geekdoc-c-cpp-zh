
```cpp
if (gpa >= 2.0)                         //Line 9
{
    if (gpa >= 3.9)                     //Line 11
        cout << "Dean’s Honor List." << endl; //Line 12
}                                       //Line 13
else                                    //Line 14
    cout << "The GPA is below the graduation "
         << " requirement. \nSee your "
         << "academic advisor." << endl;       //Line 15

    return 0;                           //Line 16
}                                       //Line 17
```

**Sample Runs:** In these sample runs, the user input is shaded.

- **Sample Run 1:**

  Enter the GPA: `3.91`

  Dean’s Honor List.

- **Sample Run 2:**

  Enter the GPA: `3.8`

- **Sample Run 3:**

  Enter the GPA: `1.95`

  The GPA is below the graduation requirement.  
  See your academic advisor.

In cases such as this one, the general rule is that you cannot look inside of a block (that is, inside the braces) to pair an else with an if. The else in Line 14 cannot be paired with the if in Line 11 because the if statement in Line 11 is enclosed within braces, and the else in Line 14 cannot look inside those braces. Therefore, the else in Line 14 is paired with the if in Line 9.

In this book, the C++ programming concepts and techniques are presented in a logical order. When these concepts and techniques are learned one at a time in a logical order, they are simple enough to be understood completely. Understanding a concept or technique completely before using it will save you an enormous amount of debugging time.

## Input Failure and the if Statement

In Chapter 3, you saw that an attempt to read invalid data causes the input stream to enter a fail state. Once an input stream enters a fail state, all subsequent input statements associated with that input stream are ignored, and the computer continues to execute the program, which produces erroneous results. You can use if statements to check the status of an input stream variable and, if the input stream enters the fail state, include instructions that stop program execution.

In addition to reading invalid data, other events can cause an input stream to enter the fail state. Two additional common causes of input failure are the following:

- Attempting to open an input file that does not exist
- Attempting to read beyond the end of an input file

One way to address these causes of input failure is to check the status of the input stream variable. You can check the status by using the input stream variable as the logical expression in an `if` statement. If the last input succeeded, the input stream variable evaluates to `true`; if the last input failed, it evaluates to `false`.

The statement:

```cpp
if (cin)
    cout << "Input is OK." << endl;
```

prints:

Input is OK.

if the last input from the standard input device succeeded. Similarly, if `inFile` is an `ifstream` variable, the statement:

```cpp
if (!inFile)
    cout << "Input failed." << endl;
```

prints:

Input failed.

if the last input associated with the stream variable `inFile` failed.

Suppose an input stream variable tries to open a file for inputting data into a program. If the input file does not exist, you can use the value of the input stream variable, in conjunction with the `return` statement, to terminate the program.

Recall that the last statement included in the function `main` is:

```cpp
return 0;
```

This statement returns a value of 0 to the operating system when the program terminates. A value of 0 indicates that the program terminated normally and that no error occurred during program execution. Values of type `int` other than 0 can also be returned to the operating system via the `return` statement. The return of any value other than 0, however, indicates that something went wrong during program execution.

The `return` statement can appear anywhere in the program. Whenever a `return` statement executes, it immediately exits the function in which it appears. In the case of the function `main`, the program terminates when the `return` statement executes. You can use these properties of the `return` statement to terminate the function `main` whenever the input stream fails. This technique is especially useful when a program tries to open an input file. Consider the following statements:

```cpp
{
    cout << "Cannot open the input file. "
         << "The program terminates." << endl;
    return 1;
}

outFile.open("testavg.out");  //open the output file

outFile << fixed << showpoint;
outFile << setprecision(2);

cout << "Processing data" << endl;

inFile >> firstName >> lastName;
outFile << "Student name: " << firstName
        << " " << lastName << endl;

inFile >> test1 >> test2 >> test3
       >> test4 >> test5;
outFile << "Test scores: " << setw(4) << test1
        << setw(4) << test2 << setw(4) << test3
        << setw(4) << test4 << setw(4) << test5
        << endl;

average = (test1 + test2 + test3 + test4 + test5) / 5.0;

outFile << "Average test score: " << setw(6)
        << average << endl;

inFile.close();
outFile.close();
return 0;
}
```

## Confusion between the Equality Operator (==) and the Assignment Operator (=)

Recall that if the decision-making expression in the if statement evaluates to true, the statement part of the if statement executes. In addition, the expression is usually a logical expression. However, C++ allows you to use any expression that can be evaluated to either true or false as an expression in the if statement. Consider the following statement:

```cpp
if (x = 5)
    cout << "The value is five." << endl;
```

The expression—that is, the decision maker—in the if statement is x = 5. The expression x = 5 is called an assignment expression because the operator = appears in the expression and there is no semicolon at the end.

This expression is evaluated as follows. First, the right side of the operator = is evaluated, which evaluates to 5. The value 5 is then assigned to x. Moreover, the value 5—that is, the new value of **x**—also becomes the value of the expression in the `if` statement—that is, the value of the assignment expression. Because 5 is nonzero, the expression in the `if` statement evaluates to true, so the statement part of the `if` statement outputs: The value is five.

No matter how experienced a programmer is, almost everyone makes the mistake of using `=` in place of `==` at one time or another. One reason why these two operators are often confused is that most programming languages use `==` as an equality operator. Thus, experience with other programming languages can create confusion. Sometimes the error is merely typographical, another reason to be careful when typing code.

Despite the fact that an assignment expression can be used as an expression, using the assignment operator in place of the equality operator can cause serious problems in a program. For example, suppose that the discount on a car insurance policy is based on the insured’s driving record. A driving record of 1 means that the driver is accident-free and receives a 25% discount on the policy. The statement:

```cpp
if (drivingCode == 1)
    cout << "The discount on the policy is 25%." << endl;
```

outputs:

The discount on the policy is 25%.

only if the value of `drivingCode` is 1. However, the statement:

```cpp
if (drivingCode = 1)
    cout << "The discount on the policy is 25%." << endl;
```

always outputs:

The discount on the policy is 25%.

because the right side of the assignment expression evaluates to 1, which is nonzero and so evaluates to true. Therefore, the expression in the `if` statement evaluates to true, outputting the following line of text: The discount on the policy is 25%. Also, the value 1 is assigned to the variable `drivingCode`. Suppose that before the `if` statement executes, the value of the variable `drivingCode` is 4. After the `if` statement executes, not only is the output wrong, but the new value assigned replaces the old driving code.

The appearance of `=` in place of `==` resembles a silent killer. It is not a syntax error, so the compiler does not warn you of an error. Rather, it is a logical error.

> Using `=` in place of `==` can cause serious problems, especially if it happens in a looping statement. Chapter 5 discusses looping structures.

The appearance of the equality operator in place of the assignment operator can also cause errors in a program. For example, suppose x, y, and z are `int` variables. The statement:

```cpp
x = y + z;
```
