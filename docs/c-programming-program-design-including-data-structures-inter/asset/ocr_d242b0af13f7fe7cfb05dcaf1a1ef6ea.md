> > **NOTE**

As noted earlier, the default type of floating-point numbers is double. Therefore, if you declare a named constant of type float, then you must specify that the value is of type float as follows:

```
~~~cpp
const float CONVERSION = 2.54f;
~~~
```

Otherwise, the compiler will generate a warning message. Notice that 2.54f says that it is a float value. Recall that the memory size for float values is four bytes; for double values, eight bytes. Because memory size is of little concern these days, as indicated earlier, we will mostly use the type double to work with floating-point values.

Using a named constant to store fixed data, rather than using the data value itself, has one major advantage. If the fixed data changes, you do not need to edit the entire program and change the old value to the new value wherever the old value is used. (For example, in the program that computes the sales tax, the sales tax rate may change.) Instead, you can make the change at just one place, recompile the program, and execute it using the new value throughout. In addition, by storing a value and referring to that memory location whenever the value is needed, you avoid typing the same value again and again and prevent accidental typos. If you misspell the name of the constant value’s location, the computer will warn you through an error message, but it will not warn you if the value is mistyped.

# ### VARIABLES

Earlier in this chapter, we introduced the term variable and how to declare it. We now review this concept and also give the general syntax to declare variables.

In some programs, data needs to be modified during program execution. For example, after each test, the average test score and the number of tests taken changes. Similarly, after each pay increase, the employee’s salary changes. This type of data must be stored in those memory cells whose contents can be modified during program execution. In C++, memory cells whose contents can be modified during program execution are called variables.

**Variable:** A memory location whose content may change during program execution.

The syntax for declaring one variable or multiple variables is:

```
~~~cpp
dataType identifier, identifier, . . .;
~~~
```

# ### EXAMPLE 2-12

Consider the following statements:

```
~~~cpp
double amountDue;
int counter;
char ch;
int x, y;
string name;
~~~
```