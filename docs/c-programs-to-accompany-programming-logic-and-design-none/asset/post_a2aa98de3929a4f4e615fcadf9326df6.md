
- 1. Given the following variable declarations and function calls, write the function’s header:

  ```cpp
  a. double cost, percent, amount;
     amount = calculateDiscount(cost, percent);
  ```

  ```cpp
  b. double area, one_length, two_length;
     area = rectArea(one_length, two_length);
  ```

  ```cpp
  c. string lower_case, upper_case;
     upper_case = changeCase(lower_case);
  ```

- 2. Given the following function headers and variable declarations, write a function call:

  ```cpp
  a. int custID = 1234;
     string custName;
     string findName(int custNumber)
  ```

  ```cpp
  b. int val1 = 10, val2 = 20, sum;
     int add(int num1, int num2)
  ```

  ```cpp
  c. int number = 3, exponent = 2, result;
     int power(int num, int exp)
  ```

## LAB 7-4: WRITING FUNCTIONS THAT RETURN A VALUE

In this lab, you complete a partially written C++ program that includes a function that returns a value. The program is a simple calculator that prompts the user for two numbers and an operator (+, -, *, or /). The two numbers and the operator are passed to the function where the appropriate arithmetic operation is performed. The result is then returned to the main function where the arithmetic operation and result are displayed. For example, if the user enters 3, 4, and *, the following is displayed:

```
3 * 4 = 12
```

The source code file provided for this lab includes the necessary variable declarations and input and output statements. Comments are included in the file to help you write the remainder of the program.

- 1. Open the source code file named `Arithmetic.cpp` using Notepad or the text editor of your choice.
- 2. Write the C++ statements as indicated by the comments.
- 3. Save this source code file in a directory of your choice and then make that directory your working directory.
- 4. Compile the source code file `Arithmetic.cpp`.
- 5. Execute the program.

## PASSING AN ARRAY AND AN ARRAY ELEMENT TO A FUNCTION

As a C++ programmer, there are times when you will want to write a function that will perform a task on all of the elements you have stored in an array. For example, in Chapter 7 of *Programming Logic and Design, Fifth Edition*, you saw a design for a program that used a function to quadruple all of the values stored in an array. This design is translated into C++ code in Figure 7-5.

```cpp
1    // PassEntireArray.cpp - This program quadruples the values stored in an array.
2    // Input: None
3    // Output: The original values and the quadrupled values
4
5    #include <iostream>
6    #include <string>
7    using namespace std;
8
9    void quadrupleTheValues(int[]);
10   int main()
11   {
12       const int LENGTH = 4;
13       int someNums[] = {10, 12, 22, 35};
14       int x;
15
16       cout << "At beginning of main function. . . " << endl;
17       x = 0;
18       while (x < LENGTH)
19       {
20           cout << someNums[x] << endl;
21           x++;
22       }
23       quadrupleTheValues(someNums);
24       cout << "At the end of main function. . . " << endl;
25       x = 0;
26       while (x < LENGTH)
27       {
28           cout << someNums[x] << endl;
29           x++;
30       }
31       return 0;
32   } // End of main function
33
34   void quadrupleTheValues(int vals[])
35   {
36       const int LENGTH = 4;
37       int x;
38
39       x = 0;
40       while(x < LENGTH)
41       {
42           cout << " In quadrupleTheValues() function, value is " << vals[x] << endl;
43           x++;
44       }
45       x = 0;
46       while(x < LENGTH)
47       {
48           vals[x] = vals[x] * 4;
49           x++;
50       }
51       x = 0;
52       while(x < LENGTH)
53       {
54           cout << "  After change, value is " << vals[x] << endl;
55           x++;
56       }
57       return;
58   } // End of quadrupleTheValues function
```

**Figure 7-5** C++ code for `PassEntireArray` program

The main function begins on line 10 and proceeds with the declaration and initialization of the constant named LENGTH (line 12) and the array of ints named someNums (line 13), followed by the declaration of the variable named x (line 14), which is used as a loop control variable. The first while loop in the program on lines 18 through 22 is responsible for printing the values stored in the array at the beginning of the program. Next, on line 23, the function named quadrupleTheValues is called. The array named someNums is passed as an argument. Notice that when an entire array is passed to a function, the square brackets and the size are not included. Also note that when you pass an entire array to a function, the beginning memory address of the array is passed by value. This means that instead of a copy of the array being passed, the memory address of the array is passed. Although you cannot change the beginning memory address of the array, this does give the function access to that memory location; the function can then change the values stored in the array if necessary.

Program control is then transferred to the quadrupleTheValues function. The header for the function on line 34 includes one parameter, `int vals[]`. The syntax for declaring an array as a formal parameter includes the parameter’s data type, followed by a local name for the array, followed by empty square brackets. Note that a size is not included within the square brackets.

> **NOTE:** On line 9, you see the function declaration for the `quadrupleTheValues` function. The function declaration includes the return type of the function (`void`), the name of the function (`quadrupleTheValues`), and the data type of the parameter(s) (`int`) and empty square brackets (`[]`) that specify the parameter is an array.

In the `quadrupleTheValues` function, the first while loop on lines 40 through 44 prints the values stored in the array, and the second while loop on lines 46 through 50 accesses each element in the array, quadruples the value, and then stores the quadrupled values in the array at their same location. The third while loop on lines 52 through 56 prints the changed values now stored in the array. Program control is then returned to the location in the `main` function where the function was called.

When program control returns to the `main` function, the next statements to execute (lines 24 through 30) are responsible for printing out the values stored in the array once more. The output from this program is displayed in Figure 7-6.

![](img/08ab7b9c5b7606ff5c1616ca55d8b41c_140_0.png)

**Figure 7-6** Output from *PassEntireArray* program

As shown in Figure 7-6, the array values printed at the beginning of the main function (lines 18 through 22) are the values with which the array was initialized. Next, the `quadrupleTheValues` function prints the array values (lines 40 through 44) again before they are changed. As shown, the values remain the same as the initialized values. The `quadrupleTheValues` function then prints the array values again after the values are quadrupled (lines 52 through 56). Finally, after the call to `quadrupleTheValues`, the main function prints the array values one last time (lines 26 through 30). These are the quadrupled values, indicating that the `quadrupleTheValues` function has access to the memory location where the array is stored and is able to permanently change the values stored there.

You can also pass a single array element to a function, just as you pass a variable or constant. The following C++ code initializes an array named `someNums`, declares a variable named `newNum`, and passes one element of the array to a function named `tripleTheNumber`. The array element is passed by value in this example, which means a copy of the value stored in the array is passed to the `tripleTheNumber` function:

```cpp
int someNums[] = {10, 12, 22, 35};
int newNum;
newNum = tripleTheNumber(someNums[1]);
```

The following C++ code includes the header for the function named `tripleTheNumber` along with the code that triples the value passed to it:

```cpp
int tripleTheNumber(int num)
{
    int result;
    result = num * 3;
    return result;
}
```

Next, you will learn how to pass arguments to a function by reference and by address.

## EXERCISE 7-5: PASSING ARRAYS TO FUNCTIONS

In this exercise, you use what you have learned about passing arrays and array elements to functions in C++.

- 1. Given the following function calls, write the function’s header:

  ```cpp
  a. int marchBirthdays[] = {3, 12, 13, 22, 27, 31};
     printBirthdayInvitations(marchBirthdays);
  ```

  ```cpp
  b. double janSales[] = {100.00, 200.00, 55.00, 230.00};
     double total;
     total = monthlySales(janSales);
  ```
