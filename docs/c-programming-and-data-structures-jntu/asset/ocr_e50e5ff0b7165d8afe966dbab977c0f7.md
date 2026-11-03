# Example 5.7

The program in Fig. 5.7 illustrates the function of %[ ] specification.

# Reading Mixed Data Types

It is possible to use one scanf statement to input a data line containing mixed mode data. In such cases, care should be exercised to ensure that the input data items match the control specifications in order and type. When an attempt is made to read an item that does not match the type expected, the scanf function does not read any further and immediately returns the values read. The statement

```
scanf("%d %c %f %s", &count, &code, &ratio, name);
```

will read the data

15 p 1.575 coffee

correctly and assign the values to the variables in the order in which they appear. Some systems accept integers in the place of real numbers and vice-versa, and the input data is converted to the type specified in the control string.

# Detection of Errors in Input

When a scanf function completes its list, it returns the value of number of items that are successfully

![](bbox=[0.25, 0.77, 0.8, 0.93])

Fig. 5.7 Illustration of conversion specification [ . ] for strings