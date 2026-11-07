
## PROGRAMMING EXAMPLE: Student Grade

Write a program that reads a student name followed by five test scores. The program should output the student name, the five test scores, and the average test score. Output the average test score with two decimal places.

The data to be read is stored in a file called test.txt. The output should be stored in a file called testavg.out.

**Input** A file containing the student name and the five test scores. A sample input is:

```text
Andrew Miller 87.50 89 65.75 37 98.50
```

**Output** The student name, the five test scores, and the average of the five test scores, saved to a file.

### PROBLEM ANALYSIS AND ALGORITHM DESIGN

To find the average of the five test scores, you add the five test scores and divide the sum by 5. The input data is in the following form: the student name followed by the five test scores. Therefore, you must read the student name first and then read the five test scores. This problem analysis translates into the following algorithm:

- 1. Read the student name and the five test scores.
- 2. Output the student name and the five test scores.
- 3. Calculate the average.
- 4. Output the average.

You output the average test score in the fixed decimal format with two decimal places.

**Variables**

The program needs to read a student's first and last name and five test scores. Therefore, you need two variables to store the student name and five variables to store the five test scores.

To find the average, you must add the five test scores and then divide the sum by 5. Thus, you need a variable to store the average test score. Furthermore, because the input data is in a file, you need an ifstream variable to open the input file. Because the program output will be stored in a file, you need an ofstream variable to open the output file. The program, therefore, needs at least the following variables:

```cpp
ifstream inFile;       //input file stream variable
ofstream outFile;      //output file stream variable

double test1, test2, test3, test4, test5; //variables to
                                          //read the five test scores

double average;        //variable to store the average test score
string firstName;      //variable to store the first name
string lastName;       //variable to store the last name
```

### MAIN ALGORITHM

In the preceding sections, we analyzed the problem and determined the formulas to perform the calculations. We also determined the necessary variables and named constants. We can now expand the previous algorithm to solve the problem given at the beginning of this programming example:

- 1. Declare the variables.
- 2. Open the input file.
- 3. Open the output file.
- 4. To output the floating-point numbers in a fixed decimal format with a decimal point and trailing zeros, set the manipulators `fixed` and `showpoint`. Also, to output the floating-point numbers with two decimal places, set the precision to two decimal places.
- 5. Read the student name.
- 6. Output the student name.
- 7. Read the five test scores.
- 8. Output the five test scores.
- 9. Find the average test score.
- 10. Output the average test score.
- 11. Close the input and output files.

Because this program reads data from a file and outputs data to a file, it must include the header file `fstream`. Because the program outputs the average test score to two decimal places, you need to set the precision to two decimal places. Therefore, the program uses the manipulator `setprecision`, which requires you to include the header file `iomanip`. Because `firstName` and `lastName` are string variables, we must include the header file `string`. The program also includes the header file `iostream` to print a message on the screen so that you will not stare at a blank screen while the program executes.

### COMPLETE PROGRAM LISTING

```cpp
//***************************************************************
// Author: D. S. Malik
//
// Program to calculate the average test score.
// Given a student's name and five test scores, this program
// calculates the average test score. The student's name, the
// five test scores, and the average test score are stored in
// the file testavg.out. The data is input from the file
// test.txt.
//***************************************************************
```

### Sample Run

```text
Input File (contents of the file test.txt):
Andrew Miller 87.50 89 65.75 37 98.50

Output File (contents of the file testavg.out):
Student name: Andrew Miller
Test scores: 87.50 89.00 65.75 37.00 98.50
Average test score: 75.55
```

> **NOTE**
>
> The preceding program uses five variables—`test1`, `test2`, `test3`, `test4`, and `test5`—to read the five test scores and then find the average test score. The website accompanying this book contains a modified version of this program that uses only one variable, `testScore`, to read the test scores and another variable, `sum`, to find the sum of the test scores. The program is named `Ch3_AverageTestScoreVersion2.cpp`.

## QUICK REVIEW

- 1. A stream in C++ is an infinite sequence of characters from a source to a destination.
- 2. An input stream is a stream from a source to a computer.
- 3. An output stream is a stream from a computer to a destination.
- 4. `cin`, which stands for common input, is an input stream object, typically initialized to the standard input device, which is the keyboard.
- 5. `cout`, which stands for common output, is an output stream object, typically initialized to the standard output device, which is the screen.
- 6. When the binary operator `>>` is used with an input stream object, such as `cin`, it is called the stream extraction operator. The left-side operand of `>>` must be an input stream variable, such as `cin`; the right-side operand must be a variable.
- 7. When the binary operator `<<` is used with an output stream object, such as `cout`, it is called the stream insertion operator. The left-side operand of `<<` must be an output stream variable, such as `cout`; the right-side operand of `<<` must be an expression or a manipulator.
- 8. When inputting data into a variable, the operator `>>` skips all leading whitespace characters.
- 9. To use `cin` and `cout`, the program must include the header file `iostream`.
- 10. The function `get` is used to read data on a character-by-character basis and does not skip any whitespace characters.
- 11. The function `ignore` is used to skip data in a line.
- 12. The function `putback` puts the last character retrieved by the function `get` back into the input stream.
- 13. The function `peek` returns the next character from the input stream but does not remove the character from the input stream.
- 14. Attempting to read invalid data into a variable causes the input stream to enter the fail state.
- 15. Once an input failure has occurred, you use the function `clear` to restore the input stream to a working state.
- 16. The manipulator `setprecision` formats the output of floating-point numbers to a specified number of decimal places.
- 17. The manipulator `fixed` outputs floating-point numbers in the fixed decimal format.
- 18. The manipulator `showpoint` outputs floating-point numbers with a decimal point and trailing zeros.
- 19. In C++, `'` (single-quote mark) is a digit separator.
- 20. The manipulator `setw` formats the output of an expression in a specific number of columns; the default output is right-justified.
- 21. If the number of columns specified in the argument of `setw` is less than the number of columns needed to print the value of the expression, the output is not truncated and the output of the expression expands to the required number of columns.
- 22. The manipulator `setfill` is used to fill the unused columns on an output device with a character other than a space.
- 23. If the number of columns specified in the `setw` manipulator exceeds the number of columns required by the next expression, the output is right-justified. To left-justify the output, you use the manipulator `left`.
- 24. To use the stream functions `get`, `ignore`, `putback`, `peek`, `clear`, and `unsetf` for standard I/O, the program must include the header file `iostream`.
- 25. To use the manipulators `setprecision`, `setw`, and `setfill`, the program must include the header file `iomanip`.
- 26. The header file `fstream` contains the definitions of `ifstream` and `ofstream`.
- 27. For file I/O, you must use the statement `#include <fstream>` to include the header file `fstream` in the program. You must also do the following: declare variables of type `ifstream` for file input and of type `ofstream` for file output and use open statements to open input and output files. You can use `<<`, `>>`, `get`, `ignore`, `peek`, `putback`, or `clear` with file stream variables.
