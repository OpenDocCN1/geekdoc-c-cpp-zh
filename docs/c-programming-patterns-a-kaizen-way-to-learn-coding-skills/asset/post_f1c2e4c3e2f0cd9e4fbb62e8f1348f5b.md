
So in this particular case we can avoid participation of else-condition which further simplifies our condition logic. We can further refine our flow-chart given as follows.

![](img/67765455776ddeb6395161cd553ecd87_230_0.png)

## NumberPattern1C_2.c

```
#include <stdio.h>
int main() {
    int totalRows = 5; //number of rows to display
    for( int row = 1 ; row <= totalRows ; row ++ ) {
        // spaces to be printed before printing numbers
        for(int col = 1 ; col <= totalRows   ; col++) {
            int upper_limit = ( totalRows + 1 - row );
            if( col <= upper_limit ) {
                printf( "%d ", upper_limit );
            }
        }// inner for-loop
        printf("\n");// moves control to the next line
    }// outer for-loop
    return 0;
}
```

We know that the total number of column level repetition are the total number of rows. Furthermore, inner loop's if-condition is responsible for decreasing the count of printing of numeric characters in columns. So the total number of repetition should also go on decreases as the number of rows goes on increases. Rows where not all column places are filled with numeric character(s) are unnecessarily looping more. We can stop this extra looping by dynamically matching the upper_limit of inner for-loop with the if-condition.

Hence, we can completely remove the if-condition and replace the logical expression of upper_limit of inner for-loop with the logical expression used in If-condition.

## NumberPattern1C_3.c

```
#include <stdio.h>
int main() {

    int totalRows = 5;  //number of rows to display

    for( int row = 1 ; row <= totalRows ; row++ ) {

        int upper_limit = ( totalRows + 1 - row );

        for(int col = 1 ; col <= upper_limit ; col++ ) {
            printf( "%d " , upper_limit );
        }

        printf("\n");// moves control to the next line
    }

    return 0;
}
```

## Output

5 5 5 5 5
4 4 4 4
3 3 3
2 2
1

Now, test for different number of lines, let it be 7. It should work correctly.

## NumberPattern1C_3.c

```
#include <stdio.h>
int main() {
    int totalRows = 7; //number of rows to display

    for( int row = 1 ; row <= totalRows ; row++ ) {
        int upper_limit = ( totalRows + 1 - row );
        for(int col = 1 ; col <= upper_limit ; col++ ) {
            printf( "%d ", upper_limit );
        }
        printf("\n");// moves control to the next line
    }

    return 0;
}
```

## Output

7 7 7 7 7 7 7
6 6 6 6 6 6
5 5 5 5 5
4 4 4 4
3 3 3
2 2
1

## Alternative solution

This time let's use decrementing outer for-loop using row variable (5 to 1) and try to determine the logical condition in order to position the numeric character(s) in our row by column picture format.

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 5 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 5 | 5 | 5 | 5 | 5 |

row =5 , 1 <=Col <= 5 (print upper_limit=5)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 4 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 4 | 4 | 4 | 4 |  |

row = 4 , (1 <=Col <= 4) (print upper_limit=4)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 3 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 3 | 3 | 3 |  |  |

row = 3 , (1 <=Col <= 3) (print upper_limit=3)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 2 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 2 | 2 |  |  |  |

row = 2 , (1 <=Col <= 2) (print upper_limit=2)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 1 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 1 |  |  |  |  |

row = 1 , (1 <=Col <= 1) (print upper_limit=1)

| Column level Repetitive Action |  |  | Expected Output |
|---|---|---|---|
| row | lower_limit <=col<= upper_limit |  |  |
|  | lower_limit | upper_limit |  |
| 5 | 1 | 5 | 5 5 5 5 5 |
| 4 | 1 | 4 | 4 4 4 4 |
| 3 | 1 | 3 | 3 3 3 |
| 2 | 1 | 2 | 2 2 |
| 1 | 1 | 1 | 1 |

The numeric output will be the value of row variable printed that many times equals the upper_limit of row variable.

The upper_limit of row variable varies and matches with the value of row variable.

| Column level Repetitive Action | | | Expected Output |
|---|---|---|---|
| row | If_condition( lower_limit <=col<= upper_limit) | | |
| | lower_limit | upper_limit | |
| 5 | 1 | row | 5 5 5 5 5 |
| 4 | 1 | row | 4 4 4 4 |
| 3 | 1 | row | 3 3 3 |
| 2 | 1 | row | 2 2 |
| 1 | 1 | row | 1 |

So our loop-condition( lower_limit <=col<= upper_limit) becomes

| loop-condition | lower_limit <=col<= upper_limit |
|---|---|
| Mathematical expression | 1 <= col <= row |
| Syntax | for( int col = 1; col <=row ; col++) |

![](img/67765455776ddeb6395161cd553ecd87_234_0.png)

Hence, our final program will be,

## NumberPattern2C.c

```c
#include <stdio.h>
int main() {

    int totalRows = 5;  //number of rows to display

    for( int row = totalRows ; row >= 1; row -- ) {

        // row value to be printed
        for(int col = 1 ; col <= row ; col++) {
            printf( "%d ", row );
        }// inner for-loop

        printf("\n");// moves control to the next line

    }// outer for-loop

    return 0;

}
```

## Output

```
5 5 5 5 5
4 4 4 4
3 3 3
2 2
1
```

Now, test for different number of lines, let it be 7. It should work correctly.

## NumberPattern2C.c

```c
#include <stdio.h>
int main() {
    int totalRows = 7; //number of rows to display
    for( int row = totalRows ; row >= 1 ; row -- ) {
        // row value to be printed
        for(int col = 1 ; col <= row ; col++) {
            printf( "%d ", row );
        }// inner for-loop
        printf("\n");// moves control to the next line
    }// outer for-loop
    return 0;
}
```

## Output

7 7 7 7 7 7 7
6 6 6 6 6 6
5 5 5 5 5
4 4 4 4
3 3 3
2 2
1

```
5 5 5 5 5
 4 4 4 4
  3 3 3
   2 2
    1
```

## NumberPattern1D

## **Tabular representation**

| | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 |
|---|---|---|---|---|---|
| Row=1 | 5 | 5 | 5 | 5 | 5 |
| Row=2 | space | 4 | 4 | 4 | 4 |
| Row=3 | space | space | 3 | 3 | 3 |
| Row=4 | space | space | space | 2 | 2 |
| Row=5 | space | space | space | space | 1 |

## **(Row, Col) value pairs representation**

| | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 |
|---|---|---|---|---|---|
| Row=1 | 1,1 | 1,2 | 1,3 | 1,4 | 1,5 |
| Row=2 | | 2,2 | 2,3 | 2,4 | 2,5 |
| Row=3 | | | 3,3 | 3,4 | 3,5 |
| Row=4 | | | | 4,4 | 4,5 |
| Row=5 | | | | | 5,5 |

## Analysis of output

In this case we need to take care of printing two different types of characters at a particular column in a particular row. The character types are the following.

- 1) Space character
- 2) Numeric character

| row | 5 |  |  |  |  |
|---|---:|---:|---:|---:|---:|
| Col | 1 | 2 | 3 | 4 | 5 |
| Output | 5 | 5 | 5 | 5 | 5 |

For row =1, 0<=spaces<=0, 1<=num<=5

| row | 4 |  |  |  |  |
|---|---:|---:|---:|---:|---:|
| Col | 1 | 2 | 3 | 4 | 5 |
| Output | space | 4 | 4 | 4 | 4 |

For row =2, 1<=spaces<=1, 1<=num<=4

| row | 3 |  |  |  |  |
|---|---:|---:|---:|---:|---:|
| Col | 1 | 2 | 3 | 4 | 5 |
| Output | space | space | 3 | 3 | 3 |

For row =3, 1<=spaces<=2, 1<=num<=3

| row | 2 |  |  |  |  |
|---|---:|---:|---:|---:|---:|
| Col | 1 | 2 | 3 | 4 | 5 |
| Output | space | space | space | 2 | 2 |

For row =4, 1<=spaces<=3, 1<=num<=2

| row | 1 |  |  |  |  |
|---|---:|---:|---:|---:|---:|
| Col | 1 | 2 | 3 | 4 | 5 |
| Output | space | space | space | space | 1 |

For row =5, 1<=spaces<=4, 1<=num<=1

## Observations

- 1) There is repetition at row level vertically, i.e., row = 1 to 5.
- 2) There is repetition at col level horizontally. , i.e., col = 1 to 5.

This gets divided into two parts. One for repetitively printing spaces and remaining column for printing numeric characters.

| For Loop | Lower limit | Upper limit |
|---|---|---|
| Outer loop(decrementing) | row=1 | row>=5 |
| Inner Loop - spaces | spaces=1 | spaces <= ?(Unkown) |
| Inner Loop - Number | num = 1 | num =?(Unkown) |
