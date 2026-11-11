# ### 4.10.1 Assignment Statement

Values can be assigned to variables using the assignment operator = as follows:

```
```
variable_name = constant;
```
```

We have already used such statements in Chapter 3. Further examples are:

```
```
initial_value     = 0;
final_value       = 100;
balance           = 75.84;
yes               = 'x';
```
```

C permits multiple assignments in one line. For example

```
```
initial_value = 0; final_value = 100;
```
```

are valid statements.

An assignment statement implies that the value of the variable on the left of the ‘equal sign’ is set equal to the value of the quantity (or the expression) on the right. The statement

```
```
year = year + 1;
```
```

means that the ‘new value’ of **year** is equal to the ‘old value’ of **year** plus 1.

During assignment operation, C converts the type of value on the right-hand side to the type on the left. This may involve truncation when real value is converted to an integer.

It is also possible to assign a value to a variable at the time the variable is declared. This takes the following form:

```
```
data-type variable_name = constant;
```
```

Some examples are:

```
```
int final_value       = 100;
char yes              = 'x';
double balance        = 75.84;
```
```

The process of giving initial values to variables is called *initialization*. C permits the *initialization* of more than one variables in one statement using multiple assignment operators. For example the statements

```
```
p = q = s = 0;
x = y = z = MAX;
```
```

are valid. The first statement initializes the variables **p**, **q**, and **s** to zero while the second initializes **x**, **y**, and **z** with **MAX**. Note that **MAX** is a symbolic constant defined at the beginning.

Remember that external and static variables are initialized to zero by *default*. Automatic variables that are not initialized explicitly will contain garbage.

# **WORKED-OUT PROBLEM 4.2**

The program in Fig. 4.8 illustrates the use of `scanf` function.

The first executable statement in the program is a `printf`, requesting the user to enter an integer number. This is known as "prompt message" and appears on the screen like

```
```
Enter an integer number
```
```

As soon as the user types in an integer number, the computer proceeds to compare the value with 100. If the value typed in is less than 100, then a message

```
```
Your number is smaller than 100
```
```

is printed on the screen. Otherwise, the message

```
```
Your number contains more than two digits
```
```

is printed. Outputs of the program run for two different inputs are also shown in Fig. 4.9.