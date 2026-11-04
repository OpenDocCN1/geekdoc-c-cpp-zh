
## Problem3. Write a program for each of the following different wave design.

|   |1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1| |*|*| | | | |*|*| | | | |*|*| | | | | | | |
|2|*| | |*| | |*| | |*| | |*| | |*| | | | | | |
|3|*| | |*| | |*| | |*| | |*| | |*| | | | | | |
|4|*| | |*| | |*| | |*| | |*| | |*| | |*| | | |
|5|*| | |*| | |*| | |*| | |*| | |*| | |*| | | |
|6|*| | |*| | |*| | |*| | |*| | |*| | |*| | | |
|7| | | | |*|*| | | | |*|*| | | | |*|*| | | | |

|   |1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1| |<|>| | | | |<|>| | | | |<|>| | | | | | | |
|2|<| | |>| | |<| | |>| | |<| | |>| | | | | | | |
|3|<| | |>| | |<| | |>| | |<| | |>| | | | | | | |
|4|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|5| | | |<| | |>| | |<| | |>| | |<| | |>| | | |
|6| | | |<| | |>| | |<| | |>| | |<| | |>| | | |
|7| | | | |<|>| | | | |<|>| | | | |<|>| | | | |

|   |1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1| |<|>| | | | |<|>| | | | |<|>| | | | | | | |
|2|<| | |>| | |<| | |>| | |<| | |>| | | | | | | |
|3|<| | |>| | |<| | |>| | |<| | |>| | | | | | | |
|4|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|-|
|5| | | |[| | |]| | |[| | |]| | |[| | |]| | | |
|6| | | |[| | |]| | |[| | |]| | |[| | |]| | | |
|7| | | | |[|]| | | | |[|]| | | | |[|]| | | | |

|   |1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1| |<|>| | | | |[|]| | | | |<|>| | | | | | | |
|2|<| | |>| | |[|]| | | | |<| | |>| | | | | | | |
|3|<| | |>| | |[|]| | | | |<| | |>| | | | | | | |
|4|<| | |>| | |[|]| | | | |<| | |>| | | | | | | |
|5| | | |<| | |>| | |[|]| | | | |<| | |>| | | |
|6| | | |<| | |>| | |[|]| | | | |<| | |>| | | |
|7| | | | |<|>| | | | |[|]| | | | |<|>| | | | |

|   |1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1| | |3|4| | | |15|16| | | | |27|28| | | | | | | |
|2|2|2| | |5| | |14| | |17| |26| | |29| | | | | | | |
|3|3|1| | |6| | |13| | |18| |25| | |30| | | | | | | |
|4|4|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0| | |
|5|5| | |7| | |12| | |19| |24| | |31| | |36| | | | |
|6|6| | |8| | |11| | |20| |23| | |32| | |35| | | | |
|7|7| | |9|10| | | |21|22| | | | |39| |34| | | | |

|   |1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19|20|21|22|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1|1|1|2| | | | |5|6| | | | |9|10| | | | | | | |
|2|2|1| | |2| | |5| | |6| | |9| | |10| | | | | | |
|3|3|1| | |2| | |5| | |6| | |9| | |10| | | | | | |
|4|4|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0|0| | |
|5|5| | |3| | |4| | |7| | |8| | |11| | |12| | | | |
|6|6| | |3| | |4| | |7| | |8| | |11| | |12| | | | |
|7|7| | |3|4| | | | |7|8| | | | |11|12| | | | |

## Recursion: Repeat without looping

In *for-loop*, the same piece of code which is enclosed in for-loop’s code block gets repeated until the condition to repeat it becomes false. We are able to get similar kind of effect using function and function calls. We know that a function can call other function(s) as not to repeat the same piece of code or set of programming instructions again and again. In case, if we do the opposite and repeat the same piece of code again and again by calling the same function then this process is known as **recursion** and function is known as **recursive function**. Moreover, like in most of repetitive processing we tried to maintain a **terminating condition** so that after which it should stop working. Similarly, we are required to give a terminating condition in order to end the motion of recursive function calls. You need to maintain a simple format to write recursive function which is given as follows;

```
recursiveFunction( startValue, parm1,param2,...){
    1.Write terminating condition which is just opposite to how you write
    loop-condition /update-condition in a for-loop
    2. Write your programming logic.
        Pass all the required variables as parameters ( parm1, param2,... ) in this functional
        call which are used in writing programming logic.
    3.recursiveFunction( nextValue, parm1,param2...);
}
```

Let’s implement a recursive function call program to print number in ascending order.

### RecursiveLoopIncrement.c

```
#include <stdio.h>

/* function declaration */
void loopInc(int counter, int totalRows);

int main() {
    // number of rows
    int totalRows = 10;
    // recursive function call to print number in an incremental order
    loopInc( 1, totalRows );
    return 0;
}

void loopInc(int counter, int totalRows) {
    // terminating condition
    if ( counter > totalRows ) {
        return;
    }
    // programming logic
    if ( counter <= totalRows ) {
        printf( "%d\n", counter );//print to console
    }
    // tail recursive call
    loopInc( counter + 1, totalRows );
}
```

## Output

- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9
- 10

Note: - Practically program with iterative logic (for-loop based) can be converted into a program based on recursive function calls and vice-versa. One of the important questions related to this topic generally asked in interview.

## Let's implement a recursive function call based program to print a diamond pattern.

### RecursiveDiamondPattern.c

```
#include <stdio.h>

/* function declaration */
void outerLoop( int row, int totalRows );
void nestedLoopLowerHalf( int col, int row, int totalRows );
void nestedLoopUpperHalf( int col, int row, int totalRows );

int main() {

    int totalRows = 7;
        outerLoop(1, totalRows);
    return 0;
}

    void outerLoop( int row, int totalRows ) {
    // for every row , col = 1,... and hence 1 value as a parameter.
        int col = 1;

            // Row level Repetitive Action : printing single row.
            if ( row <= (2 * totalRows - 1) ) {

                // Action1.Execute's Column level Repetitive Action

                // 1st half
                if ( row <= totalRows ) {
                    nestedLoopUpperHalf(col, row, totalRows);
                }
                // 2nd half
                if (row > totalRows ) {
                    nestedLoopLowerHalf(col, row, totalRows);
                }
                printf("\n"); // Action2.Move cursor to next row.
            } else {
                return;// recursive call terminating condition
            }
            // next recursive call for the next row.
            outerLoop(row + 1, totalRows);
    }

    void nestedLoopUpperHalf( int col, int row, int totalRows ) {
        // recursive call terminating condition
        if ( !(col <= (2 * totalRows - 1)) ) {
            return;
        }

        if ( (col <= (2 * totalRows - 1)) ) {
            if ( col >= (totalRows - row + 1) &&
                col <= (totalRows + row - 1) ) {
                    printf("* ");
            } else {
                printf("  ");
            }
        }

        // next recursive call to print it in the next column.
        nestedLoopUpperHalf(col + 1, row, totalRows );
    }

    void nestedLoopLowerHalf(int col, int row, int totalRows ) {
        if ( col <= (2 * totalRows - 1)) {
            if ( col >= (row - totalRows + 1) &&
                col <= (3 * totalRows - (row + 1)) ) {
                printf("* " );
            } else {
                printf(" " );
            }
        } else {
            return; // recursive call terminating condition
        }
        // next recursive call for the next column.
        nestedLoopLowerHalf(col + 1, row, totalRows );

    }// end function
```

## Output

      *
     * *
    * * *
   * * * *
  * * * * *
 * * * * * *
* * * * * * *
 * * * * * *
  * * * * *
   * * * *
    * * *
     *
