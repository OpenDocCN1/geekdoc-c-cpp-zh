# Chapter 5

The values 5.0 and 3 here are the arguments to the function They happen to be constants, but you can use any expression as an argument, as long as a value of the correct type is ultimately produced. The arguments to the power() function substitute for the parameters x and n, which were used in the definition of the function. The computation is performed using these values and then a copy of the result, 125, is returned to the calling function, main(), which is then stored in y. You can think of the function as having this value in the statement or expression in which it appears. You then output the value of y:

```
cout << endl
    << "5.0 cubed = " << y;
```

The next call of the function is used within the output statement:

```
cout << endl
    << "3.0 cubed = "
    << power(3.0, index);      // Outputting return value
```

Here, the value returned by the function is transferred directly to the output stream. Because you haven’t stored the returned value anywhere, it is otherwise unavailable to you. The first argument in the call of the function here is a constant; the second argument is a variable.

The function power() is used next in this statement:

```
x = power(x, power(2.0, 2.0));      // Using a function as an argument
```

Here the power() function is called twice. The first call to the function is the rightmost in the expression, and the result supplies the value for the second argument to the leftmost call. Although the arguments in the sub-expression power(2.0, 2.0) are both specified as the double literal 2.0, the function is actually called with the first argument as 2.0 and the second argument as the integer literal, 2. The compiler converts the double value specified for the second argument to type int because it knows from the function prototype (shown again below) that the type of the second parameter has been specified as int.

```
double power(double x, int n);      // Function prototype
```

The double result 4.0 is returned by the first call to the power() function, and after conversion to type int, the value 4 is passed as the second argument in the next call of the function, with x as the first argument. Because x has the value 3.0, the value of 3.0⁴ is computed and the result, 81.0, stored in x. This sequence of events is illustrated in Figure 5-2.

This statement involves two implicit conversions from type double to type int that were inserted by the compiler. There’s a possible loss of data when converting from type double to type int so the compiler issues warning message when this occurs, even though the compiler has itself inserted this conversion. Generally relying on automatic conversions where there is potential for data loss is a dangerous programming practice, and it is not at all obvious from the code that this conversion is intended. It is far better to be explicit in your code by using the static_cast operator when necessary. The statement in the example is much better written as:

```
x = power(x, static_cast<int>(power(2.0, 2)));
```