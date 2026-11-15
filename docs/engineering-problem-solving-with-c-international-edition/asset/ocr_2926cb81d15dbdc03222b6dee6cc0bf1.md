# Table 5.1 Operator Precedence

| Precedence | Operation | Associativity |
| :--- | :--- | :--- |
| 1 | ( ) [ ] | Innermost first |
| 2 | ++ -- + - ! (type) | Right to left (unary) |
| 3 | * / % | Left to right |
| 4 | + - | Left to right |
| 5 | < <= > >= | Left to right |
| 6 | == != | Left to right |
| 7 | && | Left to right |
| 8 | || | Left to right |
| 9 | ?: | Right to left |
| 10 | = += -= *= /= %= | Right to left |
| 11 | , | Left to right |

number of elements then depends on the specific data file used when the program is run. In all these examples, the array must be declared to be a maximum size, and then the actual number of elements used can be less than or equal to that maximum size.

The next program reads an array from a data file and then references a function to determine the maximum value in the array. The variable npts is used to specify the number of values in the array; the value of npts can be less than or equal to the defined size of the array, which is 100. The function has two arguments—the name of the array and the number of points in the array, as indicated in the function prototype statement.

![](bbox=[0.14, 0.48, 0.2, 0.54])

This program assumes that there will not be more than 100 values in the file; otherwise, this program will not work correctly. Arrays must be specified to be as large as, or larger than, the maximum number of values to be read into them.

The purpose of program chapter5_2 is to illustrate the use of an array as a function argument. If the purpose of this program was to demonstrate the maximum of the data values in the file, an array would not have been necessary; the maximum could have been determined as the data values were read.

```
/*---------------------------------------------*/
/* Program chapter5_2 */
/* */
/* This program reads values from a data file and */
/* determines the maximum value with a function. */
/* */
#include <stdio.h>
#define N 100
#define FILENAME "lab2.txt"
int main(void)
{
 /* Declare variables and function prototype. */
 int k=0, npts;
 double y[N];
 FILE *lab;
 double max(double x[],int n);
```