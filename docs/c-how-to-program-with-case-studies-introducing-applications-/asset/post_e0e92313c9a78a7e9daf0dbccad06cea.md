
and display that salesperson's earnings. Process one salesperson's figures at a time.
Here is a sample input/output dialog:

```
Enter sales in dollars (-1 to end): 5000.00
Salary is: $650.00

Enter sales in dollars (-1 to end): 1234.56
Salary is: $311.11

Enter sales in dollars (-1 to end): -1
```

### 3.19 (Interest Calculator)

The simple interest on a loan is calculated by the formula

interest = principal * rate * days / 365;

The preceding formula assumes that rate is the annual interest rate, so it divides by 365 (days per year). Develop a program that uses scanf to input principal, rate and days for several loans, and will calculate and display the simple interest for each loan, using the preceding formula. Here is a sample input/output dialog:

```
Enter loan principal (-1 to end): 1000.00
Enter interest rate: .1
Enter term of the loan in days: 365
The interest charge is $100.00

Enter loan principal (-1 to end): 1000.00
Enter interest rate: .08375
Enter term of the loan in days: 224
The interest charge is $51.40

Enter loan principal (-1 to end): -1
```

### 3.20 (Salary Calculator)

Develop a program that will determine the gross pay for each of several employees. The company pays "straight time" for the first 40 hours worked by each employee and pays "time-and-a-half" for all hours worked in excess of 40 hours. You're given a list of the company's employees, the number of hours each worked last week and each employee's hourly rate. Your program should use scanf to input this information for each employee and determine and display the employee's gross pay. Here is a sample input/output dialog:

```
Enter # of hours worked (-1 to end): 39
Enter hourly rate of the worker ($00.00): 10.00
Salary is $390.00

Enter # of hours worked (-1 to end): 40
Enter hourly rate of the worker ($00.00): 10.00
Salary is $400.00

Enter # of hours worked (-1 to end): 41
Enter hourly rate of the worker ($00.00): 10.00
Salary is $415.00

Enter # of hours worked (-1 to end): -1
```

### 3.21 (*Predecrementing vs. Postdecrementing*)

Write a program that demonstrates the difference between predecrementing and postdecrementing using the decrement operator --.

### 3.22 (*Printing Numbers from a Loop*)

Write a program that utilizes looping to print the numbers from 1 to 10 side by side on the same line with three spaces between numbers.

### 3.23 (*Find the Largest Number*)

Finding the largest number (i.e., the maximum of a group of numbers) is used frequently in computer applications. For example, a program that determines the winner of a sales contest would input the number of units sold by each salesperson. The salesperson who sells the most units wins the contest. Write a pseudocode program and then a program that uses scanf to input a series of 10 non-negative numbers and determines and prints the largest of the numbers. Your program should use three variables:

- a) counter—A counter to count to 10 (i.e., to keep track of how many numbers have been input and to determine when all 10 numbers have been processed).
- b) number—The current number input to the program.
- c) largest—The largest number found so far.

### 3.24 (*Tabular Output*)

Write a program that uses looping to print the following table of values. Use the tab escape sequence, \t, in the printf statement to separate the columns with tabs.

| N | 10*N | 100*N | 1000*N |
|---|---|---|---|
| 1 | 10 | 100 | 1000 |
| 2 | 20 | 200 | 2000 |
| 3 | 30 | 300 | 3000 |
| 4 | 40 | 400 | 4000 |
| 5 | 50 | 500 | 5000 |
| 6 | 60 | 600 | 6000 |
| 7 | 70 | 700 | 7000 |
| 8 | 80 | 800 | 8000 |
| 9 | 90 | 900 | 9000 |
| 10 | 100 | 1000 | 10000 |

### 3.25 (*Tabular Output*)

Write a program that utilizes looping to produce the following table of values:

| A | A+2 | A+4 | A+6 |
|---|---|---|---|
| 3 | 5 | 7 | 9 |
| 6 | 8 | 10 | 12 |
| 9 | 11 | 13 | 15 |
| 12 | 14 | 16 | 18 |
| 15 | 17 | 19 | 21 |

### 3.26 (*Find the Two Largest Numbers*)

Using an approach similar to Exercise 3.23, find the two largest values of the 10 numbers. You may input each number only *once*.

### 3.27 *(Validating User Input)*

Modify the program in Figure 3.6 to validate its inputs. For each input, if the value is other than 1 or 2, keep looping until the user enters a correct value.

### 3.28 What does the following program print?

```c
#include <stdio.h>

int main(void) {
   int count = 1; // initialize count

   while (count <= 10) { // loop 10 times
      // output 1 line of text
      puts(count % 2 ? "*****" : "+++++++");
      ++count; // increment count
   } // end while
} // end function main
```

### 3.29 What does the following program print?

```c
#include <stdio.h>

int main(void) {
   int row = 10; // initialize row

   while (row >= 1) { // loop until row < 1
      int column = 1; // set column to 1 as iteration begins

      while (column <= 10) { // loop 10 times
         printf("%s", (row % 2) ? ">" : "<"); // output
         ++column; // increment column
      } // end inner while

      --row; // decrement row
      puts(""); // begin new output line
   } // end outer while
} // end function main
```

### 3.30 *(Dangling-Else Problem)*

Determine the output for each of the following when x is 9 and y is 11, and when x is 11 and y is 9. The compiler ignores the indentation in a C program. Also, the compiler always associates an else with the previous if unless told to do otherwise by the placement of braces { }. For instance, you may not be sure which if an else matches, so this is referred to as the "dangling-else" problem. We eliminated the indentation from the following code to make the problem more challenging. *[Hint: Apply the indentation conventions you have learned.]*

```c
a) if (x < 10)
      if (y > 10)
         puts("*****");
      else
         puts("#####");
      puts("$$$$$");
```

```c
b) if (x < 10) {
    if (y > 10)
        puts("*****");
    }
else {
    puts("#####");
    puts("$$$$$");
}
```

### 3.31 (Another Dangling-Else Problem)

Modify the following code to produce the output shown. Use proper indentation techniques. You may not make any changes other than inserting braces. The compiler ignores the indentation in a program. We eliminated the indentation from the following code to make the problem more challenging. [Note: It's possible that no modification is necessary.]

```c
if (y == 8)
if (x == 5)
    puts("@@@@@");
else
    puts("#####");
    puts("$$$$$");
    puts("&&&&&");
```

a) Assuming x = 5 and y = 8, the following output is produced.

```
@@@@@
$$$$$
&&&&&
```

b) Assuming x = 5 and y = 8, the following output is produced.

```
@@@@@
```

c) Assuming x = 5 and y = 8, the following output is produced.

```
@@@@@
&&&&&
```

d) Assuming x = 5 and y = 7, the following output is produced.

```
#####
$$$$$
&&&&&
```

### 3.32 (Square of Asterisks)

Write a program that reads in the side of a square and then prints that square out of asterisks. Your program should work for squares of all side sizes between 1 and 20. For example, if your program reads a size of 4, it should print

```
****
****
****
****
```

### 3.33 (*Hollow Square of Asterisks*)

Modify the program you wrote in the preceding exercise so that it prints a hollow square. For example, if your program reads a size of 5, it should print

```
*****
*   *
*   *
*   *
*****
```

### 3.34 (*Palindrome Tester*)

A palindrome is a number or a text phrase that reads the same backward as forward. For example, each of the following five-digit integers is a palindrome: 12321, 55555, 45554 and 11611. Write a program that reads in a five-digit integer and determines whether or not it’s a palindrome. [Hint: Use the division and remainder operators to separate the number into its individual digits.]

### 3.35 (*Printing the Decimal Equivalent of a Binary Number*)

Input a binary integer (5 digits or fewer) containing only 0s and 1s and print its decimal equivalent. [Hint: Use the remainder and division operators to pick off the "binary" number's digits one at a time from right-to-left. Just as in the decimal number system, in which the rightmost digit has a positional value of 1, and the next digit left has a positional value of 10, then 100, then 1000, and so on, in the binary number system the rightmost digit has a positional value of 1, the next digit left has a positional value of 2, then 4, then 8, and so on. Thus the decimal number 234 can be interpreted as 4 * 1 + 3 * 10 + 2 * 100. The decimal equivalent of binary 1101 is 1 * 1 + 0 * 2 + 1 * 4 + 1 * 8 or 1 + 0 + 4 + 8 or 13.]

### 3.36 (*How Fast Is Your Computer?*)

How can you determine how fast your own computer operates? Write a program with a while loop that counts from 1 to 1,000,000,000, incrementing by 1 during each iteration of the loop. Every time the count reaches a multiple of 100,000,000, print that number on the screen. Use your watch to time how long each 100 million iterations of the loop takes. [Hint: Use the remainder operator to recognize each time the counter reaches a multiple of 100,000,000.]

### 3.37 (*Detecting Multiples of 10*)

Write a program that prints 100 asterisks, one at a time. After every tenth asterisk, print a newline character. [Hint: Count from 1 to 100. Use the % operator to recognize each time the counter reaches a multiple of 10.]

### 3.38 (*Counting 7s*)

Write a program that reads an integer (5 digits or fewer) and determines and prints how many digits in the integer are 7s.

### 3.39 (*Checkerboard Pattern of Asterisks*)

Write a program that displays the following checkerboard pattern:

```
* * * * * * * *
 * * * * * * * *
* * * * * * * *
 * * * * * * * *
* * * * * * * *
 * * * * * * * *
* * * * * * * *
 * * * * * * * *
```
