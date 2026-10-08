contains macro definitions, constants, and prototypes of functions and types used for different standard input and output operations.
We have already learned how to include a header file in our programs. The next section discussed the usage of formatted functions.

# 4.3 Formatted Functions

The formatted functions are considered to be all-purpose functions. These functions, as can be seen from Table 1, are used to input or output all type of data, may it be char, int, float, or double. The general syntax of the formatted function is shown in Figure 3:

![](bbox=[0.25, 0.45, 0.8, 0.55])

It can be seen in Figure 3 that the function name can be scanf or printf. The format specifier string indetifies the data type format in which the values of the variables are to be read or written. The identifier list consists of the address of variables in case of scanf and names of variables in case of print.
Before we continue further, let us understand the concept of address and name of a variable. An identifier when defined in C program is associated with three entities, as shown in Figure 4:

![](bbox=[0.3, 0.7, 0.7, 0.9])