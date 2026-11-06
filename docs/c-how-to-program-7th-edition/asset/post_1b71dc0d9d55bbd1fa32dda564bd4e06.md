
- c)

  ```cpp
  for ( x = 1; x <= 20; x++ )
  {
      if ( x % 5 == 0 )
          cout << x << endl;
      else
          cout << '\t';
  }
  ```

### 5.3

- a) *Error:* The semicolon after the `while` header causes an infinite loop.  
  *Correction:* Replace the semicolon by a `{`, or remove both the `;` and the `{`.

- b) *Error:* Using a floating-point number to control a `for` repetition statement.  
  *Correction:* Use an `int` and perform the proper calculation to get the values you desire.

  ```cpp
  for ( y = 1; y <= 10; ++y )
      cout << ( static_cast<double>( y ) / 10 ) << endl;
  ```

- c) *Error:* Missing `break` statement in the first case.  
  *Correction:* Add a `break` statement at the end of the first case. This is not an error if you want the statement of case 2: to execute every time the case 1: statement executes.

- d) *Error:* Improper relational operator used in the loop-continuation condition.  
  *Correction:* Use `<=` rather than `<`, or change 10 to 11.

## Exercises

### 5.4

Find the error(s), if any, in each of the following:

- a)

  ```cpp
  For ( x = 100, x >= 1, x++ )
  cout << x << endl;
  ```

- b) The following code should print whether an integer value is odd or even:

  ```cpp
  switch ( value % 2 )
  {
      case 0:
          cout << "Even integer" << endl;
      case 1:
          cout << "Odd integer" << endl;
  }
  ```

- c) The following code should output the odd integers from 19 to 1:

  ```cpp
  for ( x = 19; x >= 1; x += 2 )
      cout << x << endl;
  ```

- d) The following code should output the even integers from 2 to 100:

  ```cpp
  counter = 2;
  do
  {
      cout << counter << endl;
      counter += 2;
  } while ( counter < 100 );
  ```

### 5.5 (Summing Integers)

Write a program that uses a `for` statement to sum a sequence of integers. Assume that the first integer read specifies the number of values remaining to be entered. Your program should read only one value per input statement. A typical input sequence might be

```
5 100 200 300 400 500
```

where the 5 indicates that the subsequent 5 values are to be summed.

### 5.6 (Averaging Integers)

Write a program that uses a `for` statement to calculate the average of several integers. Assume the last value read is the sentinel 9999. A typical input sequence might be

```
10 8 11 7 9 9999
```

indicating that the program should calculate the average of all the values preceding 9999.

### 5.7 What does the following program do?

```cpp
// Exercise 5.7: ex05_07.cpp
// What does this program print?
#include <iostream>
using namespace std;

int main()
{
   int x; // declare x
   int y; // declare y

   // prompt user for input
   cout << "Enter two integers in the range 1-20: ";
   cin >> x >> y; // read values for x and y

   for (int i = 1; i <= y; i++) // count from 1 to y
   {
      for (int j = 1; j <= x; j++) // count from 1 to x
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

Write a program that uses `for` statements to print the following patterns separately, one below the other. Use `for` loops to generate the patterns. All asterisks (*) should be printed by a single statement of the form `cout << '*';` (this causes the asterisks to print side by side). [Hint: The last two patterns require that each line begin with an appropriate number of blanks. **Extra credit:** Combine your code from the four separate problems into a single program that prints all four patterns side by side by making clever use of nested `for` loops.]

```text
(a)          (b)          (c)          (d)
*            **********   **********          *
**           *********    *********          **
***          ********     ********          ***
****         *******      *******          ****
*****        ******       ******          *****
******       *****        *****          ******
*******      ****         ****          *******
********     ***          ***          ********
*********    **           **          *********
**********   *            *          **********
```

### 5.13 (Bar Chart)

One interesting application of computers is drawing graphs and bar charts. Write a program that reads five numbers (each between 1 and 30). Assume that the user enters only valid values. For each number that is read, your program should print a line containing that number of adjacent asterisks. For example, if your program reads the number 7, it should print `*******`.

### 5.14 (Calculating Total Sales)

A mail order house sells five different products whose retail prices are: product 1—$2.98, product 2—$4.50, product 3—$9.98, product 4—$4.49 and product 5—$6.87. Write a program that reads a series of pairs of numbers as follows:

- a) product number
- b) quantity sold

Your program should use a `switch` statement to determine the retail price for each product. Your program should calculate and display the total retail value of all products sold. Use a sentinel-controlled loop to determine when the program should stop looping and display the final results.

### 5.15 (GradeBook Modification)

Modify the GradeBook program of Fig. 5.9–Fig. 5.11 to calculate the grade-point average. A grade of A is worth 4 points, B is worth 3 points, and so on.

### 5.16 (Compound Interest Calculation)

Modify Fig. 5.6 so it uses only integers to calculate the compound interest. [Hint: Treat all monetary amounts as numbers of pennies. Then “break” the result into its dollar and cents portions by using the division and modulus operations. Insert a period.]

### 5.17 (What Prints?)

Assume `i = 1`, `j = 2`, `k = 3` and `m = 2`. What does each statement print?

- a) `cout << ( i == 1 ) << endl;`
- b) `cout << ( j == 3 ) << endl;`
- c) `cout << ( i >= 1 && j < 4 ) << endl;`
- d) `cout << ( m <= 99 && k < m ) << endl;`
- e) `cout << ( j >= i || k == m ) << endl;`
- f) `cout << ( k + m < j || 3 - j >= k ) << endl;`
- g) `cout << ( ! m ) << endl;`
- h) `cout << ( ! ( j - m ) ) << endl;`
- i) `cout << ( ! ( k > m ) ) << endl;`

### 5.18 (Number Systems Table)

Write a program that prints a table of the binary, octal and hexadecimal equivalents of the decimal numbers in the range 1–256. If you are not familiar with these number systems, read Appendix D, Number Systems, first. [Hint: You can use the stream manipulators `dec`, `oct` and `hex` to display integers in decimal, octal and hexadecimal formats, respectively.]

### 5.19 (Calculating π)

Calculate the value of π from the infinite series

$$\pi = 4 - \frac{4}{3} + \frac{4}{5} - \frac{4}{7} + \frac{4}{9} - \frac{4}{11} + \cdots$$

Print a table that shows the approximate value of π after each of the first 1000 terms of this series.

### 5.20 (Pythagorean Triples)

A right triangle can have sides that are all integers. A set of three integer values for the sides of a right triangle is called a Pythagorean triple. These three sides must satisfy the relationship that the sum of the squares of two of the sides is equal to the square of the hypotenuse. Find all Pythagorean triples for side1, side2 and hypotenuse all no larger than 500. Use a triple-nested `for` loop that tries all possibilities. This is an example of brute force computing. You’ll learn in more advanced computer science courses that there are many interesting problems for which there is no known algorithmic approach other than sheer brute force.

### 5.21 (Calculating Salaries)

A company pays its employees as managers (who receive a fixed weekly salary), hourly workers (who receive a fixed hourly wage for up to the first 40 hours they work and “time-and-a-half”—1.5 times their hourly wage—for overtime hours worked), commission workers (who receive $250 plus 5.7 percent of their gross weekly sales), or pieceworkers (who receive a fixed amount of money per item for each of the items they produce—each pieceworker in this company works on only one type of item). Write a program to compute the weekly pay for each employee. You do not know the number of employees in advance. Each type of employee has its own pay code:
