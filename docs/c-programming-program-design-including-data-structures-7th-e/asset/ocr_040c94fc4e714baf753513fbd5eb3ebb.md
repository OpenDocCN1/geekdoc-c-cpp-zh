constants. We can now expand the previous algorithm to solve the problem given at the beginning of this programming example:

+   1. Declare the variables.
+   2. Open the input file.
+   3. Open the output file.
+   4. To output the floating-point numbers in a fixed decimal format with a decimal point and trailing zeros, set the manipulators fixed and showpoint. Also, to output the floating-point numbers with two decimal places, set the precision to two decimal places.
+   5. Read the student name.
+   6. Output the student name.
+   7. Read the five test scores.
+   8. Output the five test scores.
+   9. Find the average test score.
+   10. Output the average test score.
+   11. Close the input and output files.

Because this program reads data from a file and outputs data to a file, it must include the header file fstream. Because the program outputs the average test score to two decimal places, you need to set the precision to two decimal places. Therefore, the program uses the manipulator setprecision, which requires you to include the header file iomanip. Because firstName and lastName are string variables, we must include the header file string. The program also includes the header file iostream to print a message on the screen so that you will not stare at a blank screen while the program executes.

# COMPLETE PROGRAM LISTING

```
******************************************************
// Author: D.S. Malik
//
// Program to calculate the average test score.
// Given a student's name and five test scores, this program
// calculates the average test score. The student's name, the
// five test scores, and the average test score are stored in
// the file testavg.out. The data is input from the file
// test.txt.
//******************************************************

#include <iostream>
#include <fstream>
#include <iomanip>
#include <string>

using namespace std;
```