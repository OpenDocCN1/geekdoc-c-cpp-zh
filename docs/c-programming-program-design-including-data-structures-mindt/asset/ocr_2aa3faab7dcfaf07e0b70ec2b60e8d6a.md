```
```cpp
for (i = 1; i <= 5; i++)
    //output a line of numbers
```
```

In the first line, we want to print the multiplication table of 1, in the second line we want to print the multiplication table of 2, and so on. Notice that the first line starts with 1 and when this line is printed, the value of i is 1. Similarly, the second line starts with 2 and when this line is printed, the value of i is 2, and so on. If i is 1, i * 1 is 1; if i is 2, i * 2 is 2; and so on. Therefore, to print a line of numbers, we can use the value of i as the starting number and 10 as the limiting value. That is, consider the following for loop:

```
```cpp
for (j = 1; j <= 10; j++)
    cout << setw(3) << i * j;
```
```

Let us take a look at this for loop. Suppose i is 1. Then we are printing the first line of the multiplication table. Also, j goes from 1 to 10 and so this for loop outputs the numbers 1 through 10, which is the first line of the multiplication table. Similarly, if i is 2, we are printing the second line of the multiplication table. Also, j goes from 1 to 10, and so this for loop outputs the second line of the multiplication table, and so on.

A little more thought produces the following nested loops to output the desired grid:

```
```cpp
for (i = 1; i <= 5; i++)              //Line 1
{                                    //Line 2
    for (j = 1; j <= 10; j++)        //Line 3
        cout << setw(3) << i * j;    //Line 4

    cout << endl;                    //Line 5
}                                    //Line 6
```
```

# EXAMPLE 5-23

Consider the following data:

```
```text
65 78 65 89 25 98 -999
87 34 89 99 26 78 64 34 -999
-999
23 99 98 97 26 78 100 63 87 23 -999
62 35 78 99 12 93 19 -999
```
```

The number -999 at the end of each line acts as a sentinel and therefore is not part of the data. Our objective is to find the sum of the numbers in each line and output the sum. Moreover, assume that this data is to be read from a file, say, Exp_5_23.txt. We assume that the input file has been opened using the file stream variable infile.

This particular data set has five lines of input. So we can use a for loop or a counter-controlled while loop to process each line of data. Let us use a while loop to process these five lines. It follows that the while loop takes the following form:

```
```cpp
counter = 0;              //Line 1
while (counter < 4)       //Line 2
{                         //Line 3
```
```