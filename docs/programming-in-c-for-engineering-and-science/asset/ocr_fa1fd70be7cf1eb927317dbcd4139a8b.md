This drop-through behavior continues until a break, a return, or the end of the switch statement is reached. Because there are no break or return statements here, execution proceeds through the next two cases and reaches the default case, which displays

```
*** Invalid conversion: B
```

and sets result to zero. The output statement following the switch then displays

```
The converted temperature is 0
```

To avoid this behavior, we must remember to end each statement list in a switch statement with a break (or return statement), except for the final statement list, where it is not necessary.

The program in Example 8.2 uses the switch statement in a main function, but it is perhaps more commonly used to control selection in functions other than main. In this case, the function is probably using the switch to select its return value, and so a return statement can be used instead of a break statement. The following example illustrates this.

# 8.3.5 Example: Converting Engineering Program Codes to Names

Numeric or letter codes are commonly used to represent information about someone or something; for example, a student’s class level at a university, an employee’s salary bracket at a company, the stage in some manufacturing processes, a student’s major program, and so on. Here we will use the last example and develop a function that accepts the code for an engineering student’s program and returns the name of the program: C for civil, E for electrical, I for industrial, M for mechanical, and U for undecided.

Suppose we start with the following stub for our function:

```
/*---------------------------------------------------------------------
This function returns the name of an engineering program
corresponding to a given program code.

Receive: a character
Return: the appropriate (string) name of an engineering program
(Civil, Electrical, Industrial, Mechanical, Undecided)
or an empty string for a nonvalid code
Output: An error message in case of a nonvalid code
---------------------------------------------------------------------*/
string engrProgram(int progCode)
{
}
```

Here, the key word in the function’s documentation is corresponding. Because we must return the name of the program corresponding to progCode, we must compare progCode to each of the possible codes, and then select an appropriate return statement.

The following algorithm applies this strategy.