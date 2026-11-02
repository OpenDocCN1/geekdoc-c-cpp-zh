
### 3.15 State which of the following are *true* and which are *false*. If a statement is *false*, explain why.

- a) An algorithm is a procedure for solving a problem in terms of the actions to be executed, without specifying the order of the actions.
- b) Unless directed otherwise, the computer automatically executes C statements in sequence.
- c) The if…else double-selection statement selects a single action.
- d) A logic error affects the program when the program is compiled. It does not fail or terminate the program prematurely.
- e) You can determine your platform’s maximum unsigned int value with the constant `UINT_MAX` from `<limits.h>`.

*For Exercises 3.16–3.20, perform each of these steps:*

1. Read the problem statement.
2. Formulate the algorithm using pseudocode and top-down, stepwise refinement.
3. Write a C program.
4. Test, debug and execute the C program.

### 3.16 (Sales Tax)

Sales tax is collected from buyers and remitted to the government. A retailer has to file a monthly sales tax report which lists the sales for the month and the amount of sales tax collected, at both the county and state levels. Develop a program that will input the total collections for a month, calculate the sales tax on the collections, and display the county and state taxes. Assume that states have a 4% sales tax and counties have a 5% sales tax. Here is a sample input/output dialog.

```text
Enter total amount collected (-1 to quit): 45678
Enter name of month: January
Total Collections: $ 45678.00
Sales: $ 41906.42
County Sales Tax: $ 2095.32
State Sales Tax: $ 1676.26
Total Sales Tax Collected: $ 3771.58

Enter total amount collected (-1 to quit): 98000
Enter name of month: February
Total Collections: $ 98000.00
Sales: $ 89908.26
County Sales Tax: $ 4495.41
State Sales Tax: $ 3596.33
Total Sales Tax Collected: $ 8091.74
Enter total amount collected (-1 to quit): -1
```

### 3.17 (Mortgage Calculator)

Develop a C program to calculate the interest accrued on a bank customer’s mortgage. For each customer, the following facts are available:

- a) the account number
- b) the mortgage amount
- c) the mortgage term
- d) the interest rate

The program should input each fact, calculate the total interest payable ( = *mortgage amount* × *interest rate* × *mortgage term*), and add it to the mortgage amount to get the total amount payable. It should calculate the required monthly payment by dividing the total amount payable by the number of months in the mortgage term. The program should display the required monthly payment rounded off to the nearest dollar. The program should process each customer’s account at a time. Here is a sample input/output dialog:

```text
Enter account number (-1 to end): 100
Enter mortgage amount (in dollars): 6500
Enter mortgage term (in years): 3
Enter interest rate (as a decimal): 0.075
The monthly payable interest is $ 221

Enter account number (-1 to end): 200
Enter mortgage amount (in dollars): 12000
Enter mortgage term (in years): 10
Enter interest rate (as a decimal): 0.045
The monthly payable interest is $ 145

Enter account number (-1 to end): -1
```

### 3.18 (Sales-Commission Calculator)

One large chemical company pays its salespeople on a commission basis. The salespeople receive $200 per week plus 9% of their gross sales for that week. For example, a salesperson who sells $5000 worth of chemicals in a week receives $200 plus 9% of $5000, or a total of $650. Develop a program that will input each salesperson’s gross sales for last week and will calculate and display that salesperson’s earnings. Process one salesperson’s figures at a time. Here is a sample input/output dialog:

```text
Enter sales in dollars (-1 to end): 5000.00
Salary is: $650.00

Enter sales in dollars (-1 to end): 1234.56
Salary is: $311.11

Enter sales in dollars (-1 to end): -1
```

### 3.19 (Interest Calculator)

The simple interest on a loan is calculated by the formula

```text
interest = principal * rate * days / 365;
```

The preceding formula assumes that rate is the annual interest rate, and therefore includes the division by 365 (days). Develop a program that will input principal, rate and days for several loans, and will calculate and display the simple interest for each loan, using the preceding formula. Here is a sample input/output dialog:

```text
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

Develop a program that will determine the gross pay for each of several employees. The company pays “straight time” for the first 40 hours worked by each employee and pays “time-and-a-half” for all hours worked in excess of 40 hours. You’re given a list of the employees of the company, the number of hours each employee worked last week and the hourly rate of each employee. Your program should input this information for each employee and should determine and display the employee's gross pay. Here is a sample input/output dialog:

```text
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

### 3.21 (Preincrementing vs Postincrementing)

Write a program that demonstrates the difference between preincrementing and postincrementing using the increment operator `++`.

### 3.22 (Checking if a Number is Prime)

A prime number is any natural number greater than 1 that is divisible only by 1 and by itself. Write a C program that reads an integer and determines whether it is a prime number or not.

### 3.23 (Find the Largest Number)

The process of finding the largest number (i.e., the maximum of a group of numbers) is used frequently in computer applications. For example, a program that determines the winner of a sales contest would input the number of units sold by each salesperson. The salesperson who sells the most units wins the contest. Write a pseudocode program and then a program that inputs a series of 10 non-negative numbers and determines and prints the largest of the numbers. *[Hint: Your program should use three variables as shown below.]*

- counter: A counter to count to 10 (i.e., to keep track of how many numbers have been input and to determine when all 10 numbers have been processed)
- number: The current number input to the program
- largest: The largest number found so far

### 3.24 (Tabular Output)

Write a program that uses looping to print the following table of values. Use the tab escape sequence, `\t`, in the printf statement to separate the columns with tabs.

| N | N² | N³ | N⁴ |
|---:|---:|---:|---:|
| 1 | 1 | 1 | 1 |
| 2 | 4 | 8 | 16 |
| 3 | 9 | 27 | 81 |
| 4 | 16 | 64 | 256 |
| 5 | 25 | 125 | 625 |
| 6 | 36 | 216 | 1296 |
| 7 | 49 | 343 | 2401 |
| 8 | 64 | 512 | 4096 |
| 9 | 81 | 729 | 6561 |
| 10 | 100 | 1000 | 10000 |

### 3.25 (Tabular Output)

Write a program that utilizes looping to produce the following table of values:

| A | A+3 | A+6 | 9A |
|---:|---:|---:|---:|
| 7 | 10 | 13 | 63 |
| 14 | 17 | 20 | 126 |
| 21 | 24 | 27 | 189 |
| 28 | 31 | 34 | 252 |
| 35 | 38 | 41 | 315 |

### 3.26 (Find the Two Largest Numbers)

Using an approach similar to Exercise 3.23, find the **two** largest values of the 10 numbers. *[Note: You may input each number only once.]*

### 3.27 (Validating User Input)

Modify the program in Figure 3.10 to validate its inputs. On any input, if the value entered is other than 1 or 2, keep looping until the user enters a correct value.

### 3.28 What does the following program print?

```c
#include <stdio.h>

int main( void )
{
   int x = 1;
   int total = 0;

   while ( x <= 5 ) { // loop 5 times
      total += x; // perform calculation
      printf( "%d\n", x*x);
      ++x; // increment counter x
   } // end while

   printf( "Total is %d\n", total); // display result
} // end function main
```

### 3.29 What does the following program print?

```c
#include <stdio.h>

int main( void )
{
   int outer_count = 1; // initialize count
   while ( outer_count <= 10 ) { // loop 10 times
      int inner_count = 1;
      while ( inner_count <= outer_count ) {
         printf( "*" );
         inner_count++;
      } // end inner while
      printf( "\n" );
      outer_count++;
   } // end outer while
} // end main
```

### 3.30 (Dangling-Else Problem)

Determine the output for each of the following when x is 9 and y is 11, and when x is 11 and y is 9. The compiler ignores the indentation in a C program. Also, the compiler always associates an `else` with the previous `if` unless told to do otherwise by the placement
