# Chapter 6 Making Decisions

```
[deskCalc add: value2];
else if ( operator == '-')
[deskCalc subtract: value2];
else if ( operator == '*')
[deskCalc multiply: value2];
else if ( operator == '/')
[deskCalc divide: value2];
```

```
NSLog("%@.f", [deskCalc accumulator]);
[deskCalc release];
```

```
[pool drain];
return 0;
```

# Program 6.8 Output

Type in your expression.
123.5 + 59.3

182.80

# Program 6.8 Output (Rerun)

Type in your expression.
198.7 / 26

7.64

# Program 6.8 Output (Rerun)

Type in your expression.
89.3 + 2.5

223.25

The scanf specifies that three values are to be read into the variables with %lf format characters, operator, and value2. A double value can be read in with the value of the variable value1, which is the first operand of the expression.

Next, you read in operator. Because the operator is a character ('+', '-', '*', or '/') not a number, you read it into the variable operator. The % format characters tell the system to read the next character from the terminal. The blank spaces inside the format string indicate that an arbitrary number of blank spaces are to be permitted on the input. This enables you to separate the operands of the operator with blank spaces when you use these types of values.

After the two values and operator have been read, in the program stores the first value in the calculator's accumulator. Next, you test the value of operator against the four permissible operators. When a match is made, the corresponding message is sent to the calculator to perform the operation. In the last NSLog, the value of the accumulator is retrieved for display. Execution of the program is not complete.