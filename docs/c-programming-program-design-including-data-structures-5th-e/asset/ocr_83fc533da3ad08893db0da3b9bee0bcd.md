A walk-through of this code shows that the `for` loop in Line 1 starts with `i = 1`. When `i` is 1, the inner `for` loop in Line 3 outputs one star and the insertion point moves to the next line. Then `i` becomes 2, the inner `for` loop outputs two stars, and the output statement in Line 5 moves the insertion point to the next line, and so on. This process continues until `i` becomes 6 and the loop stops.

What pattern does this code produce if you replace the `for` statement in Line 1 with the following?

```
```cpp
for (i = 5; i >= 1; i--)
```
```

# EXAMPLE 5-22

Suppose you want to create the following multiplication table:

|   |   |   |   |   |   |   |   |   |   |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 |
| 3 | 6 | 9 | 12 | 15 | 18 | 21 | 24 | 27 | 30 |
| 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 |
| 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 | 45 | 50 |

The multiplication table has five lines. Therefore, as in Example 5–21, we use a `for` statement to output these lines as follows:

```
```cpp
for (i = 1; i <= 5; i++)
    //output a line of numbers
```
```

In the first line, we want to print the multiplication table of one, in the second line we want to print the multiplication table of 2, and so on. Notice that the first line starts with 1 and when this line is printed, `i` is 1. Similarly, the second line starts with 2 and when this line is printed, the value of `i` is 2, and so on. If `i` is 1, `i * 1` is 1; if `i` is 2, `i * 2` is 2; and so on. Therefore, to print a line of the numbers, we can use the value of `i` as the starting number and 10 as the limiting value. That is, consider the following `for` loop:

```
```cpp
for (j = 1; j <= 10; j++)
    cout << setw(3) << i * j;
```
```

Let us take a look at this `for` loop. Suppose `i` is 1. Then we are printing the first line of the multiplication table. Also, `j` goes from 1 to 10 and so this `for` loop outputs the numbers 1 through 10, which is the first line of the multiplication table. Similarly, if `i` is 2, we are printing the second line of the multiplication table. Also, `j` goes from 1 to 10, and so this `for` loop outputs the second line of the multiplication table, and so on.

A little more thought produces the following nested loops to output the desired grid:

```
```cpp
for (i = 1; i <= 5; i++)                 //Line 1
{
    for (j = 1; j <= 10; j++)             //Line 3
        cout << setw(3) << i * j;         //Line 4
    cout << endl;                         //Line 5
}                                         //Line 6
```
```