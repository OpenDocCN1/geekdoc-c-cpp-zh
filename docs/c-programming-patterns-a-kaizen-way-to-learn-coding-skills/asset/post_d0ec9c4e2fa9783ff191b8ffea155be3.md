
*Exercise.* Complete the steps for the generation of this logic pattern for every row 1 to 5 by showing output on the computer screen diagram.

| Steps for pattern generation(row = 1 to 5) | Computer Screen |
|---|---|
| For row = 1 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 2. |
| For row = 2 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 3. |
| For row = 3 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 4. |
| For row = 4 | Computer screen diagram: columns 1–9 and rows 1–5; arrow points to row 5. |
| For row = 5 | Computer screen diagram: columns 1–9 and rows 1–6; arrow points to row 6. |

## **Let’s convert steps into C program.**

| Use of C in-built method | |
|---|---|
| Move to the next row | `printf("\n");` |
| Move to the next (row, col) position and print space " " character in the same row | `printf(" ");` |
| Move to the next (row, col) position and print star "*" character in the same row | `printf("*");` |

Mentioned methods are bound to get repeat many a times in a program in order to output these characters repeatedly. Hence we will use these within *for-loop* for such repetitive task in a program.

## COLUMN LEVEL REPETITIVE ACTION

Let’s consider two attributes rows and columns of a 2-dimensional pattern as variables;

row → variable type of integer to store integer value one at a time and represents row number between 0 and 4

col → variable type of integer to store integer value one at a time and represents column number between 1 and 5

spaces → variable type of integer to store integer value one at a time and represents space character at column number between 1 and 5

totalRows → variable type of integer to store integer value for total number of rows.

## Logic Trace Tables

| (row, col) value pair depicts the position of “*” character on the display screen |
| row=1, col1 | row=1, col2 | row=1, col3 | row=1, col4 | row=1, col5 | row=1, col6 | row=1, col7 | row=1, col8 | row=1, col9 |
|  | row=2, col2 | row=2, col3 | row=2, col4 | row=2, col5 | row=2, col6 | row=2, col7 | row=2, col8 |  |
|  |  | row=3, col3 | row=3, col4 | row=3, col5 | row=3, col6 | row=3, col7 |  |  |
|  |  |  | row=4, col4 | row=4, col5 | row=4, col6 |  |  |  |
|  |  |  |  | row=5, col5 |  |  |  |  |

The space (“ ”) and star(“*”) characters are repeated many times.

So, we can use for-loop for space (“ ”) and star(“*”) characters.

| Row level Repetitive Action | Expected Output |
| Variable: row | Column level Repetitive Action | |
|  | Variable : spaces | Variable : col | |
| 1 | 0(no space) | 1,2,3,4,5,6,7,8,9 | * * * * * * * * * |
| 2 | 1 | 2,3,4,5,6,7,8 | * * * * * * * |
| 3 | 1,2 | 3,4,5,6,7 | * * * * * |
| 4 | 1,2,3 | 4,5,6 | * * * |
| 5 | 1,2,3,4 | 5 | * |

We can fill previous table as follows also in order to explore various components of for-loop.

| Row level Repetitive Action | Expected Output |
| Variable : row | Column level Repetitive Action | |
|  | Variable : spaces | Variable : col | |
|  | min_val | max_val | min_val | max_val | |
| 1 | 0 | 0 | 1 | 9 | * * * * * * * * * |
| 2 | 1 | 1 | 2 | 8 | * * * * * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 3 | 4 | 6 | * * * |
| 5 | 1 | 4 | 5 | 5 | * |

We know that totalRows=5(total number of rows).

Let’s try to use variable totalRows to generalise the variable col’s columns are min_val & max_val.

| Row level Repetitive Action | Expected Output |
| Variable : row | Column level Repetitive Action | |
| Variable : spaces | Variable : col | |
| min_val | max_val | min_val | max_val | |
| 1 | 0 | 0 | totalRows -4 | totalRows +4 | * * * * * * * * |
| 2 | 1 | 1 | totalRows -3 | totalRows +3 | * * * * * * |
| 3 | 1 | 2 | totalRows -2 | totalRows +2 | * * * * * |
| 4 | 1 | 3 | totalRows -1 | totalRows +1 | * * * |
| 5 | 1 | 4 | totalRows -0 | totalRows +0 | * |

Let’s use decrementing for-loop with range 4 to at the row level repetition.

This is in order to match the part of the expression of variable col's columns min_val & max_val.

Using variable row to generalise the variable col's columns min_val & max_val.

| Row level Repetitive Action | Expected Output |
| Variable : row | Column level Repetitive Action | |
| Variable : spaces | Variable : col | |
| min_val | max_val | min_val | max_val | |
| 4 | 0 | 0 | totalRows - row | totalRows + row | * * * * * * * * |
| 3 | 1 | 1 | totalRows - row | totalRows + row | * * * * * * |
| 2 | 1 | 2 | totalRows - row | totalRows + row | * * * * * |
| 1 | 1 | 3 | totalRows - row | totalRows + row | * * * |
| 0 | 1 | 4 | totalRows - row | totalRows + row | * |

The condition (col >= (totalRows – row)) gives the minimum limit, a starting point from which it will start printing star(*) character(s) till the maximum value of variable col which is (totalRows + row).

The if-condition can be given for between the range of values

(totalRows - row ) and (totalRows + row) using the comparison and logical operators as:

```
If ( col >= ( totalRows - row ) && col <= ( totalRows + row ) )
```

We already know that;

Variable col = 1,2,3,4,...,9 or 1,2,3,4,..., ( totalRows + row )

Variable row = 4,3,2,1,0 or (totalRows – 1),3,2,1,0

We can eliminate the logical AND(&&) condition( col <= ( totalRows + row ) ) in the if-condition to print the star(*) characters. This logical AND(&&) condition already been considered as the upper_limit in the loop-condition for column level inner for-loop. So the if-condition will now reduce to the following.

If ( col >= (totalRows - row ) ) It will allow to print star(*) character when result of if-condition's expression is true or else will prints the space character. We generalised the non-repeating numeric pattern of the column max_val into an expressions. We can now define column level for-loop.

| Elements of Column level for-loop |
|---|---|
| min_val | 1 |
| max_val | totalRows + row |
| variable_name | col |
| statement(s) | printf("*"); |

## Row Level Repetitive Action

The following statements had been repeated 5 times(total number of rows).

Column level for-loop for printing star characters // inner for-loop

```
printf("\n "); // Move cursor to the next row
```

row → variable type of integer to store integer value one at a time and represents

row number between 4 or (totalRows - 1) and 0. The totalRows has initially assigned the value 5.

We got everything related to for-loop for row level repetition.

| Elements Of Row Level decrementing for-loop |
|---|---|
| min_val | 0 |
| max_val | totalRows - 1 |
| variable_name | row |
| statement(s) | Column level for-loop for printing star characters
printf("\n"); // Move to the next row |

The flow-chart can be given as follows:

![](img/67765455776ddeb6395161cd553ecd87_166_0.png)

Let's execute the following program.

## PatternF1.c

```
#include <stdio.h>
int main() {
    int totalRows = 5; // total number of rows to display
    // Row level Repetitive Action :
    // Action1.Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = (totalRows - 1); row >= 0; row--) {
        // Column level Repetitive Action :
        // Action1.Move cursor in the same row
        for (int col = 1; col <= (totalRows + row); col++) {
            if (col >= (totalRows - row)) {
                // Action2.prints star "*" character
                printf("* ");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }
        }// inner for-loop
        printf("\n");// Move cursor to the next row
    }// outer for-loop
    return 0;
}
```

## Output

* * * * * * * *
  * * * * * *
    * * * * *
      * * *
        *

## Alternative solution2

By using incrementing for-loop at the row level repetition we can give alternative solutions.

## Problem F1. Find the different logic and write the program to print the following pattern for 5 rows.

Test the logic for 12 rows. Some of the details are mentioned in the form of table to start with.

| Row level Repetitive Action | Expected Output |
| Variable : row | Column level Repetitive Action | |
| | Variable : spaces | Variable : col | |
| | min_val | max_val | min_val | max_val | |
| 1 | 0 | 0 | 1 | 9 | * * * * * * * * * |
| 2 | 1 | 1 | 2 | 8 | * * * * * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 3 | 4 | 6 | * * * |
| 5 | 1 | 4 | 5 | 5 | * |

When the if-condition is true program should print a star('*') character and in the else part of the if-else-statement program should print space character.

## Problem F2. Continuation to previous problem (Problem F1) write the program for the following situation.

When the if-condition is true, then program should print a space(' ') character and in the else part of the if-else-statement program should print star('*') character.
