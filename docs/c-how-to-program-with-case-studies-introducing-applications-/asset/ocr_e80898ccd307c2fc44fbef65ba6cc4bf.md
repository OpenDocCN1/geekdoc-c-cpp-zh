Functions printf and scanf facilitate interaction between the user and the computer. This interaction resembles a dialogue and is often called interactive computing.

# ### Prompting for and Inputting the Second Integer

Line 13

```
```c
printf("Enter second integer: "); // prompt
```
```

prompts the user to enter the second integer, then line 14

```
```c
scanf("%d", &integer2); // read an integer
```
```

obtains a value for variable integer2 from the user.

# ### Defining the sum Variable

Line 16

```
```c
int sum = 0; // variable in which sum will be stored
```
```

defines the int variable sum and initializes it to 0 before we use sum in line 17.

# ### Assignment Statement

The assignment statement in line 17

```
```c
sum = integer1 + integer2; // assign total to sum
```
```

calculates the total of variables integer1 and integer2, then assigns the result to variable sum using the assignment operator (=). The statement is read as, “sum gets the value of the expression integer1 + integer2.” Most calculations are performed in assignments.

# ### Binary Operators

The = operator and the + operator are binary operators—each has two operands. The + operator's operands are integer1 and integer2. The = operator's operands are sum and the value of the expression integer1 + integer2. Place spaces on either side of a binary operator to make the operator stand out and make the program more readable.

# ### Printing with a Format Control String

The format control string "Sum is %d\n" in line 19

```
```c
printf("Sum is %d\n", sum); // print sum
```
```

contains some literal characters to display (“Sum is ”) and the conversion specification %d, which is a placeholder for an integer. The sum is the value to insert in place of %d. The conversion specification for an integer (%d) is the same in both printf and scanf—this is true for most, but not all, C data types.

# ### Combining a Variable Definition and Assignment Statement

You can initialize a variable in its definition. For example, lines 16 and 17 can add the variables integer1 and integer2, then initialize the variable sum with the result:

```
```c
int sum = integer1 + integer2; // assign total to sum
```
```