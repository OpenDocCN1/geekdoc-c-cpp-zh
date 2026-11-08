1. Given the following variable declarations and function calls, write the function’s header:

```
a. double cost, percent, amount;
   amount = calculateDiscount(cost, percent);
```

```
b. double area, one_length, two_length;
   area = rectArea(one_length, two_length);
```

```
c. string lower_case, upper_case;
   upper_case = changeCase(lower_case);
```

2. Given the following function headers and variable declarations, write a function call:

```
a. int custID = 1234;
   string custName;
   string findName(int custNumber)
```

```
b. int val1 = 10, val2 = 20, sum;
   int add(int num1, int num2)
```

```
c. int number = 3, exponent = 2, result;
   int power(int num, int exp)
```

# LAB 7-4: WRITING FUNCTIONS THAT RETURN A VALUE

In this lab, you complete a partially written C++ program that includes a function that returns a value. The program is a simple calculator that prompts the user for two numbers and an operator (+, -, *, or /). The two numbers and the operator are passed to the function where the appropriate arithmetic operation is performed. The result is then returned to the main function where the arithmetic operation and result are displayed. For example, if the user enters 3, 4, and *, the following is displayed:

```
3 * 4 = 12
```

The source code file provided for this lab includes the necessary variable declarations and input and output statements. Comments are included in the file to help you write the remainder of the program.