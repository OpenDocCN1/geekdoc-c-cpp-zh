# Chapter 6
311
Function and Parameter Declarations

Similarly, in the second and third function calls, the compiler creates two functions: one in which the data type T is replaced by the keyword float, and in one which the type T is replaced by the keyword double. This is the output produced by Program 6.4:

```
The absolute value of -4 is 4nThe absolute value of -4.23 is 4.23nThe absolute value of -4.23456 is 4.23456
```

The value of using a function template is that one function has been defined to create different functions, each of which uses the same logic and operations but operates on different types.
Finally, both Programs 6.3 and 6.4 define a template using a single placeholder type, function templates with more than one data type can be defined. For example, the template prefix

```
template <class DTYPE1, class DTYPE2, class DTYPE3>
```

can be used to create a function requiring three different types. As before, in the function template's header and body, the data types DTYPE1, DTYPE2, and DTYPE3 are used in the same manner as any built-in data type, such as int, float, and double. Also, as noted previously, the names DTYPE1, DTYPE2, and DTYPE3 can be any non-keyword identifier.
Conventionally, the letter T followed by zero or more digits is used, such as T, T1, T2, T3, and so forth.

![](bbox=[0.19, 0.483, 0.173, 0.543])

# EXERCISES 6.1

+   1. (Practice) For the following function headers, determine the number, type, and order (sequence) of the values that must be passed to the function:
a. void factorial(int n)
b. void volts(int res, double induct, double cap)
c. void power(int type, double induct, double cap)
d. double flag(char type, double current, double time)
e. void total(double amount, double c, char d, double e, double f)
f. void roi(int a, int b, char c, char declflag)
g. getVal(int item, int iter, char declag, char delim)

+   2. (Practice) Write a function named checked() has three parameters. The first parameter should accept an integer number, and the second and third parameters should accept a double-precision number. The function body should just display the values of data passed to the function when it's called. (Note: When tracing errors in functions, having the function display values it has passed is helpful. Quite often, the error isn't in what the function body does with data, but in the data received and stored.)