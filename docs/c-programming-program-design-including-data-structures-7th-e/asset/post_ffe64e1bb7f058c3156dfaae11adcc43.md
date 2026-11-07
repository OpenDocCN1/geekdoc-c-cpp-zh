
## EXAMPLE 5-22

Suppose you want to create the following multiplication table:

| | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 | 20 |
| 3 | 6 | 9 | 12 | 15 | 18 | 21 | 24 | 27 | 30 |
| 4 | 8 | 12 | 16 | 20 | 24 | 28 | 32 | 36 | 40 |
| 5 | 10 | 15 | 20 | 25 | 30 | 35 | 40 | 45 | 50 |

The multiplication table has five lines. Therefore, as in Example 5-21, we use a `for` statement to output these lines as follows:

```cpp
for (i = 1; i <= 5; i++)
    //output a line of numbers
```

In the first line, we want to print the multiplication table of 1, in the second line we want to print the multiplication table of 2, and so on. Notice that the first line starts with 1 and when this line is printed, `i` is 1. Similarly, the second line starts with 2 and when this line is printed, the value of `i` is 2, and so on. If `i` is 1, `i * 1` is 1; if `i` is 2, `i * 2` is 2; and so on. Therefore, to print a line of numbers, we can use the value of `i` as the starting number and 10 as the limiting value. That is, consider the following `for` loop:

```cpp
for (j = 1; j <= 10; j++)
    cout << setw(3) << i * j;
```

Let us take a look at this `for` loop. Suppose `i` is 1. Then we are printing the first line of the multiplication table. Also, `j` goes from 1 to 10 and so this `for` loop outputs the numbers 1 through 10, which is the first line of the multiplication table. Similarly, if `i` is 2, we are printing the second line of the multiplication table. Also, `j` goes from 1 to 10, and so this `for` loop outputs the second line of the multiplication table, and so on.

A little more thought produces the following nested loops to output the desired grid:

```cpp
for (i = 1; i <= 5; i++)          //Line 1
{                                //Line 2
    for (j = 1; j <= 10; j++)    //Line 3
        cout << setw(3) << i * j;//Line 4
    cout << endl;                //Line 5
}                                //Line 6
```

## EXAMPLE 5-23

Consider the following data:

```text
65 78 65 89 25 98 -999
87 34 89 99 26 78 64 34 -999
-999
23 99 98 97 26 78 100 63 87 23 -999
62 35 78 99 12 93 19 -999
```

The number -999 at the end of each line acts as a sentinel and therefore is not part of the data. Our objective is to find the sum of the numbers in each line and output the sum. Moreover, assume that this data is to be read from a file, say, `Exp_5_23.txt`. We assume that the input file has been opened using the input file stream variable `infile`.

This particular data set has five lines of input. So we can use a `for` loop or a counter-controlled `while` loop to process each line of data. Let us use a `while` loop to process these five lines. It follows that the `while` loop takes the following form:

```cpp
counter = 0;                    //Line 1
while (counter < 5)             //Line 2
{                               //Line 3
        //process the line       //Line 4

        //output the sum
        counter++;
}
```

Let us now concentrate on processing a line. Each line has a varying number of data items. For example, the first line has six numbers, the second line has eight numbers, and so on. Because each line ends with -999, we can use a sentinel-controlled `while` loop to find the sum of the numbers in each line with -999 as the sentinel value. Consider the following `while` loop:

```cpp
sum = 0;                       //Line 4
infile >> num;                 //Line 5
while (num != -999)            //Line 6
{                              //Line 7
        sum = sum + num;       //Line 8
        infile >> num;         //Line 9
}                              //Line 10
```

The statement in Line 4 initializes sum to 0, and the statement in Line 5 reads and stores the first number of the line into num. The Boolean expression `num != -999` in Line 6 checks whether the number is -999. If num is not -999, the statements in Lines 8 and 9 execute. The statement in Line 8 updates the value of sum; the statement in Line 9 reads and stores the next number into num. The loop continues to execute as long as num is not -999.

It now follows that the nested loop to process the data is as follows. (Assume that all variables are properly declared.)

```cpp
counter = 0;                         //Line 1
while (counter < 5)                  //Line 2
{                                    //Line 3
        sum = 0;                     //Line 4
        infile >> num;               //Line 5
        while (num != -999)          //Line 6
        {                            //Line 7
                sum = sum + num;     //Line 8
                infile >> num;       //Line 9
        }                            //Line 10

        counter++;                   //Line 11
        cout << "Line " << counter   //Line 12
             << ": Sum = " << sum << endl;  //Line 13
}                                    //Line 14
```

## EXAMPLE 5-24

Suppose that we want to process data similar to the data in Example 5-23, but the input file is of an unspecified length. That is, each line contains the same data as the data in each line in Example 5-23, but we do not know the number of input lines.

Because we do not know the number of input lines, we must use an EOF-controlled `while` loop to process the data. In this case, the required code is as follows. (Assume that all variables are properly declared and the input file has been opened using the input file stream variable `infile`.)

```cpp
counter = 0;                         //Line 1
infile >> num;                        //Line 2
while (infile)                         //Line 3
{                                      //Line 4
    sum = 0;                           //Line 5
    while (num != -999)                //Line 6
    {                                  //Line 7
        sum = sum + num;               //Line 8
        infile >> num;                 //Line 9
    }                                  //Line 10

    counter++;                         //Line 11
    cout << "Line " << counter        //Line 12
         << ": Sum = " << sum << endl; //Line 13
    infile >> num;                     //Line 14
}                                      //Line 15
```

Notice that we have again used the variable counter, this time to allow us to print the line number with the sum of each line.

## EXAMPLE 5-25

Consider the following data:

```text
101
John Smith
65 78 65 89 25 98 -999
102
Peter Gupta
87 34 89 99 26 78 64 34 -999
103
Buddy Friend
23 99 98 97 26 78 100 63 87 23 -999
104
Doctor Miller
62 35 78 99 12 93 19 -999
...
```

The number -999 at the end of a line acts as a sentinel and therefore is not part of the data.

Assume that this is the data of certain candidates seeking the student council’s presidential seat.

For each candidate, the data is in the following form:

```text
ID
Name
Votes
```

The objective is to find the total number of votes received by the candidate. We assume that the data is input from the file Exp_5_25.txt of unknown size. We also assume that the input file has been opened using the input file stream variable infile.

Because the input file is of an unspecified length, we use an EOF-controlled while loop. For each candidate, the first data item is the ID of type int on a line by itself; the second data item is the name, which may consist of more than one word; and the third line contains the votes received from the various departments.

To read the ID, we use the extraction operator >>; to read the name, we use the stream function getline. Notice that after reading the ID, the reading marker is after the ID and the character after the ID is the newline character. Therefore, after reading the ID, the reading marker is after the ID and before the newline character (of the line containing the ID).

The function getline reads until the end of the line. Therefore, if we read the name immediately after reading the ID, then what is stored in the variable name is the newline character (after the ID). It follows that to read the name, we must read and discard the newline character after the ID, which we can accomplish using the stream function get. Therefore, the statements to read the ID and name are as follows:

```cpp
infile >> ID;            //read the ID
infile.get(ch);           //read the newline character after the ID
getline(infile, name);    //read the name
```

(Assume that ch is a variable of type char.) The general loop to process the data is:

```cpp
infile >> ID;                         //Line 1
while (infile)                         //Line 2
{
    infile.get(ch);                     //Line 4
    getline(infile, name);               //Line 5

    //process the numbers in each line   //Line 6
    //output the name and total votes
    infile >> ID;    //begin processing the next line
}
```
