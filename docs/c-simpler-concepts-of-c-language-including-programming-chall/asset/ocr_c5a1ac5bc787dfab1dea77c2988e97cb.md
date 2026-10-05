# 4

# 1.6. C VARIABLES

In C programming a variable must be declared before it is being used. Variables can be declared at the start of any block of code. Most local variables are created when the function is called, and are destroyed on return from that function.

A declaration begins with the type, followed by the name of one or more variables. For example,

```
int top, bottom;
```

Variables can be initialised when they are declared, this is done by adding an equals sign and the required value after the declaration.

```
int top = 100;      /* Maximum Temperature */
int bottom = -20;     /* Minimum Temperature * /
```

C provides a wide range of types. All the types are going to be discussed in the forth topics.

# 1.7. C DATA TYPES

C supports many types of data. Each data type will occupy different amount of memory space. There are three major classifications of the data types in C. It is represented in the figure 1.1.

![](bbox=[0.125, 0.438, 0.875, 0.542])

Figure 1.1 Data types supported in C programming

# 1.7.1. Primary (built in) data types

They are the basic data types and there are four built in data types available in C programming.

They are listed as follows:

+   a. Integer
b. Floating point representation (Real)
c. Double precision real number
d. Character representation and
e. Void

A table 1.5 has the description and memory requirements for the data types specified above.

| Type (Keyword) | Description | Size (bytes) |
|---|---|---|n| Integer (int) | Used to represent integer quantity | 2 bytes (May vary from compiler to compiler) |
| Floating point (float) | Used to represent floating point number (a number with a decimal point) | 4 bytes (1 word) |