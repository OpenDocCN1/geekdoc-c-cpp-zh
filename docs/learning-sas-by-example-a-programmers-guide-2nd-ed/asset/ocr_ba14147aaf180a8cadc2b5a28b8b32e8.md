# Chapter 2: Writing Your First SAS Program

The statements beginning with an asterisk (*) are called comment statements. They enable you to include comments for yourself or others reading your program later. One way of writing a SAS comment is to start with an asterisk, write as many lines as you like, and end the statement (as you do all statements) with a semicolon. Comments are not only useful for others to read and understand your program—they are useful to you as well. Just imagine trying to understand a section of a long program that you wrote a year ago and now need to correct or modify. Trust me—you will be glad you commented your program. You should also include information about the file name used to store the program, the purpose of the program, and the date you wrote the program as well as the date of any changes you made to the program.

The statement that starts with BMI= is called an assignment statement. It is an instruction to perform the computation on the right-hand side of the equal sign and assigning the resulting value to the variable on the left. In example, you are creating a new variable BMI that is defined as a person's weight (in kilograms) divided by a person's Height (in meters) squared. BMI (body mass index) is a useful index of obesity. Medical researchers often use BMI when computing the health risks of diseases (such as heart attacks).

This assignment uses three of the basic arithmetic operators used by SAS: the forward slash (/) for division, the asterisk (*) for multiplication, and the double asterisk (**) for exponentiation. This is a good time to mention the full set of arithmetic operators. They are as follows:

| Operator | Description | Priority |
|---|---|--|
| + | Addition | Lowest |
| - | Subtraction | Lowest |
| * | Multiplication | Next Highest |
| / | Division | Next Highest |
| ** | Exponentiation | Highest |
| | Negation | Highest |

The rules you learned about the order of algebraic operations in school apply to SAS arithmetic operators. That, multiplication and division occur before addition and subtraction. In the previous table, the two highest priority operators occur before all others; the next highest operators occur before the lowest. For example, the value of x in the following assignment statement is 14:

```
x = 2 + 3 * 4;
```

If you want to multiply the sum of 2 + 3 by 4, you need to use parentheses like this:

```
x = (2 + 3) * 4;
```

When you include parentheses in your expression, all operations within the parentheses are performed. In this example, because parentheses surround the addition operation, the 2 and 3 are added together and then multiplied by 4, yielding a value of 20.

As a further example of how the priority of arithmetic operators works, take a look at the expression that uses each of the different operators:

```
x = 2**3 + 4 * -5;
```