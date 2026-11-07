# **Program 3.20**  Overflow and underflow in doubles (Continued)

```
```cpp
// Print the positive and negative maximum double
cout << "The value of maximum double: " << num1 << endl;
cout << "The value of minimum double: " << num2 << endl;
// Multiply the values by 1000.00
num1 *= 1000.00;
num2 *= 1000.00;
// Print the overflowed values
cout << "The value of num1 * 1000 after overflow: " << num1 << endl;
cout << "The value of num2 * 1000 after underflow: " << num2 << endl;
return 0;
}

Run:
The value of maximum double: 1.79769e+308
The value of minimum double: -1.79769e+308
The value of num1 * 1000 after overflow: 1#INF
The value of num2 * 1000 after underflow: -INF
```
```

# ## 3.5 FORMATTING DATA

The programs we have used in the previous section input or output data in a standard (default) format. For example, Boolean data are input and output as 0 or 1. The integer values are input and output in decimal format (see Appendix B). The floating-point values are input in a standard format (integral part followed by a decimal point and the fraction part) and output as required by the application. Sometimes we need to change this behavior. We need to format data as we like. This is done with the help of predefined objects called **manipulators**. We have manipulators for outputting data and manipulators for inputting data. We first discuss the manipulators for outputting data, which are more common and extensive; we then discuss manipulators for inputting data.

# ### 3.5.1 Manipulators for Output

As we mentioned before, output operations are done using output objects. We use the predefined output object (cout). So far, we have only passed data items to the insertion operator (<<); we have not defined how the data should be formatted when displayed or printed. An output manipulator is an object that can be passed to the insertion operator to change the behavior of the output. We have two different kinds of output manipulators: with no argument and with one argument. We discuss each next.

# ### No-Argument Manipulators

There are several output manipulators that need no argument. The no-argument manipulators are part of `<iostream>`, which means no extra header file is needed. We show the common no-argument manipulators in Table 3.3.

The manipulators for each category (except `endl`) come in groups of two or three. One of the manipulators in each group is the default. If we do not use a manipulator in that group, it is set to the default value. In Table 3.3 we show the default values in red. Note that the term (none) means that there is no default: The system uses the fixed or scientific based on