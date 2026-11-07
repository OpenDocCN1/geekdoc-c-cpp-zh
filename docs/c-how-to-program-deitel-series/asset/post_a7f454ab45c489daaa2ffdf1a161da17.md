
## 5.3 Find the errors in each of the following code segments and explain how to correct them.

a)

```cpp
unsigned int x = 1;
while ( x <= 10 );
    ++x;
}
```

b)

```cpp
for ( double y = 0.1, y != 1.0; y += .1 )
    cout << y << endl;
```

c)

```cpp
switch ( n )
{
    case 1:
        cout << "The number is 1" << endl;
    case 2:
        cout << "The number is 2" << endl;
        break;
    default:
        cout << "The number is not 1 or 2" << endl;
        break;
}
```

d) The following code should print the values 1 to 10.

```cpp
unsigned int n = 1;
while ( n < 10 )
    cout << n++ << endl;
```

## Answers to Self-Review Exercises

### 5.1

- a) False. The default case is optional. Nevertheless, it’s considered good software engineering to always provide a default case.
- b) False. The break statement is used to exit the switch statement. The break statement is not required when the default case is the last case. Nor will the break statement be required if having control proceed with the next case makes sense.
- c) False. When using the `&&` operator, both of the relational expressions must be true for the entire expression to be true.
- d) True.

### 5.2

a)

```cpp
unsigned int sum = 0;
for ( unsigned int count = 1; count <= 99; count += 2 )
    sum += count;
```

b)

```cpp
cout << fixed << left
     << setprecision( 1 ) << setw( 15 ) << 333.546372
     << setprecision( 2 ) << setw( 15 ) << 333.546372
     << setprecision( 3 ) << setw( 15 ) << 333.546372
     << endl;
```

Output is:

```text
333.5       333.55       333.546
```

c)

```cpp
cout << fixed << setprecision( 2 ) << setw( 10 ) << pow( 2.5, 3 ) << endl;
```

Output is:

```text
15.63
```

d)

```cpp
unsigned int x = 1;
while ( x <= 20 )
{
```

### 5.5 (Summing Integers)

Write a program that uses a `for` statement to sum a sequence of integers. Assume that the first integer read specifies the number of values remaining to be entered. Your program should read only one value per input statement. A typical input sequence might be

`5 100 200 300 400 500`

where the 5 indicates that the subsequent 5 values are to be summed.

### 5.6 (Averaging Integers)

Write a program that uses a `for` statement to calculate the average of several integers. Assume the last value read is the sentinel 9999. For example, the sequence `10 8 11 7 9 9999` indicates that the program should calculate the average of all the values preceding 9999.

### 5.7 (What Does This Program Do?)

What does the following program do?

```cpp
// Exercise 5.7: ex05_07.cpp
// What does this program do?
#include <iostream>
using namespace std;

int main()
{
   unsigned int x; // declare x
   unsigned int y; // declare y

   // prompt user
   cout << "Enter two integers in the range 1-20: ";
   cin >> x >> y; // read values for x and y

   for ( unsigned int i = 1; i <= y; ++i ) // count from 1 to y
   {
      for ( unsigned int j = 1; j <= x; ++j ) // count from 1 to x
         cout << '@'; // output @

      cout << endl; // begin new line
   } // end outer for
} // end main
```

### 5.8 (Find the Smallest Integer)

Write a program that uses a `for` statement to find the smallest of several integers. Assume that the first value read specifies the number of values remaining.

### 5.9 (Product of Odd Integers)

Write a program that uses a `for` statement to calculate and print the product of the odd integers from 1 to 15.

### 5.10 (Factorials)

The factorial function is used frequently in probability problems. Using the definition of factorial in Exercise 4.34, write a program that uses a `for` statement to evaluate the factorials of the integers from 1 to 5. Print the results in tabular format. What difficulty might prevent you from calculating the factorial of 20?

### 5.11 (Compound Interest)

Modify the compound interest program of Section 5.4 to repeat its steps for the interest rates 5%, 6%, 7%, 8%, 9% and 10%. Use a `for` statement to vary the interest rate.

### 5.12 (Drawing Patterns with Nested `for` Loops)

Write a program that uses `for` statements to print the following patterns separately, one below the other. Use `for` loops to generate the patterns. All asterisks (`*`) should be printed by a single statement of the form `cout << '*';` (this causes the asterisks to print side by side). *Hint:* The last two patterns require that each line begin with an appropriate number of blanks. Extra credit: Combine your code from the four separate problems into a single program that prints all four patterns side by side by making clever use of nested `for` loops.

```text
       (a)          (b)          (c)          (d)
       *            **********       **********          *
       **           *********        *********           **
       ***          ********         ********            ***
       ****         *******          *******             ****
       *****        ******           ******              *****
       ******       *****            *****               ******
       *******      ****             ****                *******
       ********     ***              ***                 ********
       *********    **               **                  *********
       **********   *                *                   **********
```

### 5.13 (Bar Chart)

One interesting application of computers is drawing graphs and bar charts. Write a program that reads five numbers (each between 1 and 30). Assume that the user enters only valid values. For each number that is read, your program should print a line containing that number of adjacent asterisks. For example, if your program reads the number 7, it should print `*******`.

### 5.14 (Calculating Total Sales)

A mail order house sells five different products whose retail prices are: product 1—$2.98, product 2—$4.50, product 3—$9.98, product 4—$4.49 and product 5—$6.87. Write a program that reads a series of pairs of numbers as follows:

- a) product number
- b) quantity sold

Your program should use a switch statement to determine the retail price for each product. Your program should calculate and display the total retail value of all products sold. Use a sentinel-controlled loop to determine when the program should stop looping and display the final results.

### 5.15 (Gradebook Modification)

Modify the GradeBook program of Figs. 5.9–5.11 to calculate the grade-point average. A grade of A is worth 4 points, B is worth 3 points, and so on.

### 5.16 (Compound Interest Calculation)

Modify Fig. 5.6 so it uses only integers to calculate the compound interest. [Hint: Treat all monetary amounts as a number of pennies. Then “break” the result into its dollar and cents portions by using the division and modulus operations. Insert a period.]

### 5.17 (What Prints?)

Assume `i = 1, j = 2, k = 3` and `m = 2`. What does each statement print?

- a) `cout << ( i == 1 ) << endl;`
- b) `cout << (j == 3 ) << endl;`
- c) `cout << (i >= 1 && j < 4 ) << endl;`
- d) `cout << (m <= 99 && k > m ) << endl;`
- e) `cout << (j > 1 || k == m ) << endl;`
- f) `cout << (k + m < j || i == j ) << endl;`
- g) `cout << (!m) << endl;`
- h) `cout << (!(j == m )) << endl;`
- i) `cout << (!(k > m )) << endl;`

### 5.18 (Number Systems Table)

Write a program that prints a table of the binary, octal and hexadecimal equivalents of the decimal numbers in the range 1–256. If you are not familiar with these number systems, read Appendix D. [Hint: You can use the stream manipulators dec, oct and hex to display integers in decimal, octal and hexadecimal formats, respectively.]

### 5.19 (Calculating π)

Calculate the value of π from the infinite series

\[
\pi = 4 - \frac{4}{3} + \frac{4}{5} - \frac{4}{7} + \frac{4}{9} - \frac{4}{11} + \cdots
\]

Print a table that shows the approximate value of π after each of the first 1000 terms of this series.

### 5.20 (Pythagorean Triples)

A right triangle can have sides that are all integers. A set of three integer values for the sides of a right triangle is called a Pythagorean triple. These three sides must satisfy the relationship that the sum of the squares of two of the sides is equal to the square of the hypotenuse.
