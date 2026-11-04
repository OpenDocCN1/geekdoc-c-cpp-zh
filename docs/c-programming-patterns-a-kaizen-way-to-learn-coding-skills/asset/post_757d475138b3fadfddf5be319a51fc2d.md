
## Alternative solution2

From the previous solution, when the if-condition is true we will print a star("*") character and in the else part of the if-statement we will print spaces. Let's start with the observation table that we got from the previous solution.

| Row | Spaces min_val | Spaces max_val | Col min_val | Col max_val | Expected Output |
|---|---|---|---|---|---|
| 1 | 1 | 4 | 5 | 5 | * |
| 2 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 4 | 1 | 1 | 2 | 8 | * * * * * * * |
| 5 | 0 | 0 | 1 | 9 | * * * * * * * * * |

Reversing the counter values of variable row, i.e. row = 5, 4, 3, 2, 1 so that it will match the column min_val of the variable col.

| Row | Spaces min_val | Spaces max_val | Col min_val | Col max_val | Expected Output |
|---|---|---|---|---|---|
| 5 | 1 | 4 | 5 | 5 | * |
| 4 | 1 | 3 | 4 | 6 | * * * |
| 3 | 1 | 2 | 3 | 7 | * * * * * |
| 2 | 1 | 1 | 2 | 8 | * * * * * * * |
| 1 | 0 | 0 | 1 | 9 | * * * * * * * * * |

We can use the variable totalRows to generalise the column max_val for printing star character(s).

| Row | Spaces min_val | Spaces max_val | Col min_val | Col max_val | Expected Output |
|---|---|---|---|---|---|
| 5 | 1 | 4 | row | 5 + 0 / totalRows + 0 | * |
| 4 | 1 | 3 | row | 5 + 1 / totalRows + 1 | * * * |
| 3 | 1 | 2 | row | 5 + 2 / totalRows + 2 | * * * * * |
| 2 | 1 | 1 | row | 5 + 3 / totalRows + 3 | * * * * * * * |
| 1 | 0 | 0 | row | 5 + 4 / totalRows + 4 | * * * * * * * * * |

Part of variable col's column max_val's expression is still having distinct numeric value at each row.

| Variable : row | Variable : col (min_val) | max_val | 1 | 2 | 3 | Expected Output |
|---|---|---|---|---|---|---|
| 5 | row | 5 | 5+0 | totalRows+0 | totalRows+0 | * |
| 4 | row | 6 | 5+1 | totalRows+1 | totalRows+5-4 | * * * |
| 3 | row | 7 | 5+2 | totalRows+2 | totalRows+5-3 | * * * * * |
| 2 | row | 8 | 5+3 | totalRows+3 | totalRows+5-2 | * * * * * * * |
| 1 | row | 9 | 5+4 | totalRows+4 | totalRows+5-1 | * * * * * * * * * |

Part of variable col's column max_val's expression matches with the row values.

| Variable : row | Variable : col (min_val) | max_val | 4 | 5 | Expected Output |
|---|---|---|---|---|---|
| 5 | row | 5 | totalRows + 5 - 5 | totalRows + totalRows - 5 | * |
| 4 | row | 6 | totalRows + 5 - 4 | totalRows + totalRows - 4 | * * * |
| 3 | row | 7 | totalRows + 5 - 3 | totalRows + totalRows - 3 | * * * * * |
| 2 | row | 8 | totalRows + 5 - 2 | totalRows + totalRows - 2 | * * * * * * * |
| 1 | row | 9 | totalRows + 5 - 1 | totalRows + totalRows - 1 | * * * * * * * * * |

The condition (col >= row) gives starting point from which for-loop will start printing star("*") character(s) till the maximum value of variable col which is (2 * totalRows - row) for every value of row. The if-condition can be given for the range of values between (row) and (2 * totalRows - row) using the comparison and logical operators as:

```text
If ( col >= ( row ) && col <= (2 * totalRows - row ) ) ← Same expression
```

We already know that;

```text
variable col = 1,2,3,4,5 or 1,2,3,4, ...,(2 * totalRows - row)
variable row = 5,4,3,2,1 or totalRows,4,3,2,1
```

We can eliminate the logical AND(&&) condition( col <= (2 * totalRows - row) ) in the if-condition. This logical AND(&&) condition has already been taken care of as the loop-condition in the column level inner for-loop.

So the if-condition will now reduce to If ( col >= row ). We can summarise it all as;

**Prints a star when condition is True for every value of variable col**

| col=1 | col=2 | col=3 | col=4 | ....................................... | col= (2 * totalRows - row) |
|---|---|---|---|---|---|
| **If ( condition=( col >= row ) is True)**<br>**Print star character**<br>**Else**<br>**Print space character** |  |  |  |  |  |

We generalised the non-repeating numeric pattern of the column max_val into an expression.

We can now define column level *for-loop*.

| *Elements of Column level for-loop* |  |
|---|---|
| min_val | 1 |
| max_val | (2 * totalRows - row) |
| variable_name | col |
| statement(s) | `printf("* ");` |

### ROW LEVEL REPETITIVE ACTION

The following statements have been repeated 5 times (total number of rows).

**Column level for-loop** for printing **star characters** // *inner for-loop*

```c
printf("\n");// Move cursor to the next row
```

We have assigned **unique value** to **each row** starting from 5 till 1.

Let's consider;

**row →** variable **type of integer** to store integer value one at a time and represents row number between 5 and 1. The **totalRows** has initially assigned the value 5.

We got everything related to **for-loop** for row level repetition.

| *Elements Of Row Level decrementing for-loop* |  |
|---|---|
| min_val | 1 |
| max_val | totalRows |
| variable_name | **row** |
| statement(s) | **Column level for-loop** for printing **star characters**<br>`printf("\n"); //Moves cursor to the next row` |

Let's execute the following program.

## PatternE.C

```c
#include <stdio.h>
int main() {

    int totalRows = 5; // total number of rows to display

    // Row level Repetitive Action:
    // Action1. Executes Column level Repetitive Action
    // Action2.Move cursor to next row.
    for (int row = totalRows; row >= 1; row--) {

        // Column level Repetitive Action :

        // Action1.Move cursor in the same row
        for (int col = 1; col <= (2 * totalRows - row); col++) {

            if (col >= row) {
                // Action2.prints star "*" character
                printf("* ");
            } else {
                // Action3.prints space " " character
                printf(" ");
            }

        }// inner for-loop

        printf("\n\n");// Move cursor to the next row

    }// outer for-loop

    return 0;

}
```

### Output

```text
        *
      * *
    * * *
  * * * * *
* * * * * * *
```

## Pattern1F

Our programming job is to output this pattern on a part of the computer screen as shown in the following. We can consider the computer screen as a combination of (row, column) numeric value paired boxes which are spread all over the screen. Each box is treated as a resident of just a single character only.

![](img/67765455776ddeb6395161cd553ecd87_162_0.png)

![](img/67765455776ddeb6395161cd553ecd87_162_1.png)

### Analysis of output

We see that the complete pattern can be easily expressed as a collection of selected (row, column) numeric value pairs. The selection of (row number, column number) numeric pairs will be based on the keyboard characters used to design the given pattern. With this numeric pair number scheme we can correctly locate a particular keyboard character on the computer screen. The first value in any selected numeric pair represents the row number and second value represents a column number. For example:

(2, 4) means character “*” at **second row** and **fourth column** in the table.

|  | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 | Col=6 | Col=7 | Col=8 | Col=9 |
|---|---|---|---|---|---|---|---|---|---|
| **Row=1** | *(1,1) | *(1,2) | *(1,3) | *(1,4) | *(1,5) | *(1,6) | *(1,7) | *(1,8) | *(1,9) |
| **Row=2** | space | *(2,2) | *(2,3) | *(2,4) | *(2,5) | *(2,6) | *(2,7) | *(2,8) | space |
| **Row=3** | space | space | *(3,3) | *(3,4) | *(3,5) | *(3,6) | *(3,7) | space | space |
| **Row=4** | space | space | space | *(4,4) | *(4,5) | *(4,6) | space | space | space |
| **Row=5** | space | space | space | space | *(5,5) | space | space | space | space |

***The actual challenge is to find correct (row, col) positions on the computer screen by writing a program. This will be carried out by applying for-loop along with appropriate logical conditions. This stimulates growth for algorithmic thinking, a fundamental requirement of a confident programmer.***
