days on which they occurred. A program is needed that will read this data, calculate these statistics, and write the results to an output file that can be accessed by the team personnel.

# 11.1.2 Object-Centered Design

# 11.1.2.1 Behavior

For maximum flexibility, our program should display on the screen a prompt for the name of the input file containing the pressure readings to be processed and then read this file name from the keyboard. It should then read an arbitrary number of values from that file and compute the average along with the minimum and maximum of those values and when they occurred. The program should display on the screen a prompt for the name of the output file, which is entered from the keyboard. It must then write the computed values to that output file.

# 11.1.2.2 Objects

In addition to the objects identified in the preceding behavior, the program must maintain a count of how many values have been read and their sum, because these values are needed to compute the average of a collection of values. This gives the following list of objects needed to solve the problem:

| Problem Objects | Software Objects |  |  |
|---|---|---|---|
|  | Type | Kind | Name |
| The name of the file in which the pressure readings are stored | string | variable | inputFileName |
| A pressure reading | double | variable | reading |
| The number of readings | int | variable | count |
| The sum of the readings | double | variable | sum |
| The average reading | double | variable | none (sum/count) |
| The minimum reading | double | variable | minimum |
| When it occurred | int | variable | minDay |
| The maximum reading | double | variable | maximum |
| When it occurred | int | variable | maxDay |
| The name of the file to which the results are to be written | string | variable | outputFileName |

From this list we can specify the input and output of our program as follows:

Input(keyboard):
inputFileName, a string naming an input file
outputFileName, a string naming an output file

Input(inputFileName):
a sequence of pressure readings

Output(outputFileName):
the average of the input values
the maximum and minimum values and when they occurred