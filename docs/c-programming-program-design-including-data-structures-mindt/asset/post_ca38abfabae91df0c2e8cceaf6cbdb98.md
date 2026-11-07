
```cpp
else                                      //Line 12
    cout << "The GPA is below the graduation "
         << "requirement. \nSee your "
         << "academic advisor." << endl;    //Line 13
```

Following the rule of pairing an `else` with an `if`, the `else` in Line 12 is paired with the `if` in Line 10. In other words, using the correct indentation, the code is:

```cpp
if (gpa >= 2.0)                         //Line 9
    if (gpa >= 3.9)                      //Line 10
        cout << "Dean's Honor List." << endl;  //Line 11
    else                                 //Line 12
        cout << "The GPA is below the graduation "
             << "requirement. \nSee your "
             << "academic advisor." << endl;     //Line 13
```

Now, we can see that the `if` statement in Line 9 is a one-way selection. Therefore, if the input number is less than 2.0, no action will take place, that is, no warning message will be printed. Now, suppose the input is 3.8. Then, the expression in Line 9 evaluates to `true`, so the expression in Line 10 is evaluated, which evaluates to `false`. This means the output statement in Line 13 executes, resulting in an unsatisfactory result.

In fact, the program should print the warning message only if the GPA is less than 2.0, and it should print the message:

Dean's Honor List.

if gpa is greater than or equal to 3.9.

To achieve that result, the `else` in Line 12 needs to be paired with the `if` in Line 9. To pair the `else` in Line 12 with the `if` in Line 9, you need to use a compound statement, as follows:

```cpp
if (gpa >= 2.0)                         //Line 9
{
    if (gpa >= 3.9)                      //Line 10
        cout << "Dean's Honor List." << endl;  //Line 11
}                                        //Line 12
else
    cout << "The GPA is below the graduation "
         << "requirement. \nSee your "
         << "academic advisor." << endl;    //Line 13
```

The correct program is as follows.

```cpp
//Correct GPA program.

#include <iostream>                     //Line 1

using namespace std;                    //Line 2

int main()                                //Line 3
{
    double gpa;                           //Line 5

    cout << "Enter the GPA: ";        //Line 6
    cin >> gpa;                         //Line 7
    cout << endl;                       //Line 8

    if (gpa >= 2.0)                     //Line 9
    {
        if (gpa >= 3.9)                 //Line 11
            cout << "Dean's Honor List." << endl; //Line 12
    }
    else                                //Line 14
        cout << "The GPA is below the graduation "
             << "requirement. \nSee your "
             << "academic advisor." << endl;        //Line 15

    return 0;                           //Line 16
}                                   //Line 17
```

**Sample Runs:** In these sample runs, the user is shaded.

### Sample Run 1:

```cpp
Enter the GPA: 3.91
Dean's Honor List.
```

### Sample Run 2:

```cpp
Enter the GPA: 3.8
```

### Sample Run 3:

```cpp
Enter the GPA: 1.95
The GPA is below the graduation requirement.
See your academic advisor.
```

In cases such as this one, the general rule is that you cannot look inside of a block (that is, inside the braces) to pair an `else` with an `if`. The `else` in Line 14 cannot be paired with the `if` in Line 11 because the `if` statement in Line 11 is enclosed within braces, and the `else` in Line 14 cannot look inside those braces. Therefore, the `else` in Line 14 is paired with the `if` in Line 9.

In this book, the C++ programming concepts and techniques are presented in a logical order. Understanding a concept or technique completely before using it will save you an enormous amount of debugging time.

## Input Failure and the `if` Statement

In Chapter 3, you saw that an attempt to read invalid data causes the input stream to enter a fail state. Once an input stream enters a fail state, all subsequent input statements associated with that input stream are ignored, and the computer continues to execute the program, which produces erroneous results. You can use `if` statements to check the status of an input stream variable and, if the input stream enters the fail state, include instructions that stop program execution.

In addition to reading invalid data, other events can cause an input stream to enter the fail state. Two additional common causes of input failure are the following:

- Attempting to open an input file that does not exist
- Attempting to read beyond the end of an input file

One way to address the causes of input failure is to check the status of the input stream variable. You can check the status by using the input stream variable as the logical expression in an `if` statement. If the last input succeeded, the input stream variable evaluates to `true`; if the last input failed, it evaluates to `false`.

The statement:

```cpp
if (cin)
    cout << "Input is OK." << endl;
```

prints:

```cpp
Input is OK.
```

if the last input from the standard input device succeeded. Similarly, if `infile` is an ifstream variable, the statement:

```cpp
if (!infile)
    cout << "Input failed." << endl;
```

prints:

```cpp
Input failed.
```

if the last input associated with the stream variable `infile` failed.

Suppose an input stream variable tries to open a file for inputting data into a program. If the input file does not exist, you can use the value of the input stream variable, in conjunction with the `return` statement, to terminate the program.

Recall that the last statement included in the function `main` is:

```cpp
return 0;
```

This statement returns a value of 0 to the operating system when the program terminates. A value of 0 indicates that the program terminated normally and that no error occurred during program execution. Values of type `int` other than 0 can also be returned to the operating system via the `return` statement. The return of any value other than 0, however, indicates that something went wrong during program execution.

The `return` statement can appear anywhere in the program. Whenever a `return` statement executes, it immediately exits the function in which it appears. In the case of the function `main`, the program terminates when the `return` statement executes. You can use these properties of the `return` statement to terminate the function `main` whenever the input stream fails. This technique is especially useful when a program tries to open an input file. Consider the following statements:

```cpp
ifstream infile;

infile.open("inputdat.dat");    //open file inputdat.dat

if (!infile)
{
    cout << "Cannot open the input file. "
         << "The program terminates." << endl;
    return 1;
}
```

Suppose that the file `inputdat.dat` does not exist. The operation to open this file fails, causing the input stream to enter the fail state. As a logical expression, the file stream variable `infile` then evaluates to `false`. Because `infile` evaluates to `false`, the expression `!infile` (in the `if` statement) evaluates to `true`, and the body of the `if` statement executes. The message:

Cannot open the input file. The program terminates.

is printed on the screen, and the `return` statement terminates the program by returning a value of `1` to the operating system.

Let’s now use the code that responds to input failure by including these features in the *Programming Example: Student Grade* from Chapter 3. Recall that this program calculates the average test score based on data from an input file and then outputs the results to another file. The following programming code is the same as the code from Chapter 3, except that it includes statements to exit the program if the input file does not exist.

```cpp
//Program to calculate the average test scores.

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;

int main()
{
    ifstream inFile;    //input file stream variable
    ofstream outFile;   //output file stream variable

    double test1, test2, test3, test4, test5;
    double average;

    string firstName;
    string lastName;
```
