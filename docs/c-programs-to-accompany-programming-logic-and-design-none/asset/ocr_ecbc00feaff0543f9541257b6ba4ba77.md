Program control is now passed to the swap function. The header for the swap function on line 27 specifies that the function does not return a value and accepts two parameters, val1 and val2. The two parameters are declared as pointers to ints (int* val1, int* val2). The parameter val1 contains the address of num1 and the parameter val2 contains the address of num2. On line 29, the int variable named temp is declared. Because val1 and val2 are both pointers, the indirection operator (*) is used on lines 30, 31, and 32 to gain access to the values stored in memory that are pointed to by val1 and val2. On line 30, the value pointed to by val1 (the value of num1) is accessed indirectly and then assigned to temp. On line 31, the value pointed to by val2 (the value of num2) is accessed indirectly and then assigned to what val1 points to, which is num1. This assignment statement changes the value of num1 in the main function. Line 32 assigns the value stored in temp to what val2 points to, which is num2. This assignment changes the value of num2 in the main function.

When the swap function returns control to the main function, the values of num1 and num2 are displayed again on lines 20 and 22. This time, the value of num1 is 10 and the value of num2 is 5, illustrating that the local variables num1 and num2 have been changed by the swap function.

You can compile and execute this program to see the output values on your system. The program, named PassByAddress.cpp, is included with the data files provided with this book.

Next, you will learn what it means to overload a function and how to accomplish overloading functions in C++.

# EXERCISE 7-6: PASS BY REFERENCE AND PASS BY ADDRESS

In this exercise, you use what you have learned about passing arguments by reference and by address to functions in C++.

+   1. Given the following variable and function declarations, write the function call and the function's header:

+   a. double price = 22.95, increase = .10;

```
void changePrice(double&, double);
```

+   b. double price = 22.95, increase = .10;

```
void changePrice(double*, double);
```