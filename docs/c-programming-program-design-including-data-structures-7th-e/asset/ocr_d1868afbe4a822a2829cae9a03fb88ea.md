# EXAMPLE 6-2

Now that the function `larger` is written, the following C++ code illustrates how to use it:

```
double num1 = 13.00;
double num2 = 36.53;
double maxNum;
```

Consider the following statements:

```
cout << "The larger of 5 and 6 is " << larger(5, 6)
     << endl;                                      //Line 1

cout << "The larger of " << num1 << " and " << num2
     << " is " << larger(num1, num2) << endl;       //Line 2

cout << "The larger of " << num1 << " and 29 is "
     << larger(num1, 29) << endl;                   //Line 3

maxNum = larger(38.45, 56.78);                       //Line 4
```

+   - The expression `larger(5, 6)` in Line 1 is a function call, and 5 and 6 are actual parameters. When the expression `larger(5, 6)` executes, 5 is copied into `x`, and 6 is copied into `y`. Therefore, the statement in Line 1 outputs the larger of 5 and 6.
+   - The expression `larger(num1, num2)` in Line 2 is a function call. Here, `num1` and `num2` are actual parameters. When the expression `larger(num1, num2)` executes, the value of `num1` is copied into `x`, and the value of `num2` is copied into `y`. Therefore, the statement in Line 2 outputs the larger of `num1` and `num2`.
+   - The expression `larger(num1, 29)` in Line 3 is also a function call. When the expression `larger(num1, 29)` executes, the value of `num1` is copied into `x`, and 29 is copied into `y`. Therefore, the statement in Line 3 outputs the larger of `num1` and 29. Note that the first parameter, `num1`, is a variable, while the second parameter, 29, is a constant value.
+   - The expression `larger(38.45, 56.78)` in Line 4 is a function call. In this call, the actual parameters are 38.45 and 56.78. In this statement, the value returned by the function `larger` is assigned to the variable `maxNum`.

> **NOTE**
> 
> In a function call, you specify only the actual parameter, not its data type. For example, in Example 6-2, the statements in Lines 1, 2, 3, and 4 show how to call the function `larger` with the actual parameters. However, the following statements contain incorrect calls to the function `larger` and would result in syntax errors. (Assume that all variables are properly declared.)
> 
> ```cpp
> x = larger(int one, 29);          //illegal
> y = larger(int, int, 29);        //illegal
> cout << larger(int one, int two); //illegal
> ```