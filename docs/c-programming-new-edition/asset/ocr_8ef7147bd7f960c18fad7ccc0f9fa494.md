Well it doesn’t understand anything unless you tell it folks! So now how do you tell it? To specify to the computer what type you want to store, you specify the data type (i.e., int for integer, float for numbers with decimal point and char for character.) just before the variable name.

Take a look below:

```
int e_sal float da char e_name
```

Here e_sal, da, e_name are the different variable names. Though the programmer decides the variable names it is always preferable to use meaningful variable names. For example in the above example, e_sal means employee salary, da means dearness allowance and e_name means employee name.

# 2.4. TYPE DECLARATION

One may tend to consider type declarations to be just another drop in the vast ocean of C’s technical jargon and tend to turn a blind eye towards it but it doesn’t happen to be so. You are aware that C uses variables (a, b, x, y, and so on). These variables can be assigned to any one of the data types, i.e., the variable can be assigned to store an integer number or a floating point number (a number with decimals, in case you forgot) or a character.

This assignment of a data type to the variable is called type declaration. Type declaration has to be done at the beginning of the program right after the opening braces. The process of type declaration makes programming in C very uncomplicated because once the variable is declared at the beginning, the same variable can be used any number of times in the program and each time its data type will be the same as that declared in the beginning.

+   - **Example 2.2:** Presume that x is a variable and it has been assigned the data type int. This means that the variable x can store only integer numbers throughout the program anywhere it is called. **int sal;** If there is more than one variable to which the same data type has to be assigned, it can be done by making it succeed the data type instead of prefixing the data type name before all the variables.

For Example:

```
int sno,cno,hno; float sal,id; char sname,cname;
```

There are a few rules that have to be broadcast while exercising the task of type declaration.