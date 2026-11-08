
## Choosing the Right Looping Structure

All three loops have their place in C++. If you know, or the program can determine in advance, the number of repetitions needed, the for loop is the correct choice. If you do not know, and the program cannot determine in advance the number of repetitions needed, and it could be 0, the while loop is the right choice. If you do not know, and the program cannot determine in advance the number of repetitions needed, and it is at least 1, the do...while loop is the right choice.

## break and continue Statements

The break statement, when executed in a switch structure, provides an immediate exit from the switch structure. Similarly, you can use the break statement in while, for, and do...while loops. When the break statement executes in a repetition structure, it immediately exits from the structure. The break statement is typically used for two purposes:

- To exit early from a loop.
- To skip the remainder of the switch structure.

After the break statement executes, the program continues to execute with the first statement after the structure. The use of a break statement in a loop can eliminate the use of certain flag variables. The following C++ code segment helps illustrate this idea. (Assume that all variables are properly declared.)

```cpp
    sum = 0;
    isNegative = false;

    cin >> num;

    while (cin && !isNegative)
    {
        if (num < 0)    //if num is negative, terminate the loop
                        //after this iteration
        {
            cout << "Negative number found in the data." << endl;
            isNegative = true;
        }
        else
        {
            sum = sum + num;
            cin >> num;
        }
    }
```

This while loop is supposed to find the sum of a set of positive numbers. If the data set contains a negative number, the loop terminates with an appropriate error message. This while loop uses the flag variable isNegative to accomplish the desired result. The variable isNegative is initialized to false before the while loop. Before adding num to sum, check whether num is negative. If num is negative, an error message appears on the screen and isNegative is set to true. In the next iteration, when the expression in the while statement is evaluated, it evaluates to false because !isNegative is false. (Note that because isNegative is true, !isNegative is false.)

The following while loop is written without using the variable isNegative:

```cpp
sum = 0;
cin >> num;

while (cin)
{
    if (num < 0)    //if num is negative, terminate the loop
    {
        cout << "Negative number found in the data." << endl;
        break;
    }

    sum = sum + num;
    cin >> num;
}
```

In this form of the while loop, when a negative number is found, the expression in the if statement evaluates to true; after printing an appropriate message, the break statement terminates the loop. (After executing the break statement in a loop, the remaining statements in the loop are discarded.)

> **NOTE** The break statement is an effective way to avoid extra variables to control a loop and produce an elegant code. However, break statements must be used very sparingly within a loop. An excessive use of these statements in a loop will produce spaghetti-code (loops with many exit conditions) that can be very hard to understand and manage. You should be extra careful in using break statements and ensure that the use of the break statements makes the code more readable and not less readable. If you’re not sure, don’t use break statements.

The continue statement is used in while, for, and do...while structures. When the continue statement is executed in a loop, it skips the remaining statements in the loop and proceeds with the next iteration of the loop. In a while and do...while structure, the expression (that is, the loop-continue test) is evaluated immediately after the continue statement. In a for structure, the update statement is executed after the continue statement, and then the loop condition (that is, the loop-continue test) executes.

If the previous program segment encounters a negative number, the while loop terminates. If you want to discard the negative number and read the next number rather than terminate the loop, replace the break statement with the continue statement, as shown in the following example:

```cpp
sum = 0;
cin >> num;

while (cin)
{
    if (num < 0)
    {
        cout << "Negative number found in the data." << endl;
        cin >> num;
        continue;
    }

    sum = sum + num;
    cin >> num;
}
```

It was stated earlier that all three loops have their place in C++ and that one loop can often replace another. The execution of a continue statement, however, is where the while and do...while structures differ from the for structure. When the continue statement is executed in a while or a do...while loop, the update statement may not execute. In a for structure, the update statement always executes.

## Nested Control Structures

In this section, we give examples that illustrate how to use nested loops to achieve useful results and process data.

### EXAMPLE 5-21

Suppose you want to create the following pattern:

```
*
**
***
****
*****
```

Clearly, you want to print five lines of stars. In the first line, you want to print one star, in the second line, two stars, and so on. Because five lines will be printed, start with the following for statement:

```cpp
for (i = 1; i <= 5; i++)
```

The value of i in the first iteration is 1, in the second iteration it is 2, and so on. You can use the value of i as the limiting condition in another for loop nested within this loop to control the number of stars in a line. A little more thought produces the following code:

```cpp
for (i = 1; i <= 5; i++)        //Line 1
{                               //Line 2
    for (j = 1; j <= i; j++)    //Line 3
        cout << "*";            //Line 4
    cout << endl;                //Line 5
}                               //Line 6
```

### EXAMPLE 5-23

Consider the following data:

```
65 78 65 89 25 98 -999
87 34 89 99 26 78 64 34 -999
23 99 98 97 26 78 100 63 87 23 -999
62 35 78 99 12 93 19 -999
```

The number -999 at the end of each line acts as a sentinel and therefore is not part of the data. Our objective is to find the sum of the numbers in each line and output the sum. Moreover, assume that this data is to be read from a file, say, Exp_5_23.txt. We assume that the input file has been opened using the input file stream variable infile.

This particular data set has four lines of input. So we can use a for loop or a counter-controlled while loop to process each line of data. Let us use a while loop to process these four lines. It follows that the while loop takes the following form:

```cpp
counter = 0;                  //Line 1
while (counter < 4)           //Line 2
{                              //Line 3
    //process the line        //Line 4

    //output the sum
    counter++;
}
```

Let us now concentrate on processing a line. Each line has a varying number of data items. For example, the first line has six numbers, the second line has eight numbers, and so on. Because each line ends with -999, we can use a sentinel-controlled while loop to find the sum of the numbers in each line. (Remember how a sentinel-controlled loop works.) Consider the following while loop:

```cpp
sum = 0;                      //Line 4
infile >> num;                //Line 5
while (num != -999)           //Line 6
{                             //Line 7

    sum = sum + num;          //Line 8
    infile >> num;            //Line 9
}                             //Line 10
```

The statement in Line 4 initializes sum to 0, and the statement in Line 5 reads and stores the first number of the input line to num. The Boolean expression num != -999 in Line 6 checks whether the number is -999. If num is not -999, the statements in Lines 8 and 9 execute. The statement in Line 8 updates the value of sum; the statement in Line 9 reads and stores the next number into num. The loop continues to execute as long as num is not -999.

It now follows that the nested loop to process the data is as follows. (Assume that all variables are properly declared.)
