# 108 Learning SAS by Example: A Programmer's Guide, Second Edition

Program 8.10: Using an Iterative DO Loop to Make a Table of Squares and Square Roots

```
data Table;
  do n = 1 to 10;
    Square = n*n;
    SquareRoot = sqrt(n);
    output;
  end;
run;
```

title "Table of Squares and Square Roots"; proc print data=table noobs;
run;

Notice that this program does not have any input data. It generates the value of $n$ in the DO loop, computes the squares and square roots (SQRT is a square root function—returns the square root of its argument), and outputs an observation to the data set. For all the values from 1 to 10. Here is the output:

Figure 8.7: Output from Program 8.10

# Table of Squares and Square Roots

| n | Square | SquareRoot |
| 1 | 1 | 1.000000 |
| 2 | 4 | 1.41421 |
| 3 | 9 | 1.73205 |
| 4 | 16 | 2.000000 |
| 5 | 25 | 2.23607 |
| 6 | 36 | 2.44949 |
| 7 | 49 | 2.64575 |
| 8 | 64 | 2.82843 |
| 9 | 81 | 3.00000 |
| 10 | 100 | 3.16228 |

What if you want a table where $n$ has values of 0, 10, 20, 30, and so forth up to 100. The following DO statement does the trick:

```
do n = 0 to 100;
```

DO loops also count backward. For example, the following statement produces values of 10, 8, 6, 4, and 2 for the index variable:

```
do index = 10 to 1 by -2;
```

When you use a negative increment value, the index value is decremented by this value for each iteration of the DO loop. When the value of the index variable is less than the stop value, the loop stops.