in the formal parameter at a different memory location, and is considered local to that function. In this example, as shown on line 26, the value is stored in the formal parameter named `number`.

The header for the `evenOrOdd` function on line 26 includes the `void` keyword, so you know the function will not return a value. The name of the function follows and within the parentheses that follow the function name, the parameter `number` is given a local name and declared as the `int` data type.

Remember that even though the parameter `number` has the same name as the local variable `number` in the `main` function, the values are stored at different memory locations. Figure 7-2 illustrates that the variable `number` that is local to `main` is stored at one memory location and the parameter `number` in the `evenOrOdd` function is stored at a different memory location.

Within the function on line 28, the modulus operator `%` is used in the test portion of the `if` statement to determine if the value of the local `number` is even or odd. The user is then informed if `number` is even (line 29) or odd (line 31), and program control is transferred back to the statement that follows the call to `evenOrOdd` in the `main` function (line 20).

Back in the `main` function, the user is asked to enter another number on line 20 and the `while` loop continues to execute, calling the `evenOrOdd` function with a new input value. The loop is exited when the user enters the sentinel value 999 and the program ends.

In the next section, you will learn how to pass more than one value to a function.

> > **NOTE**
> > It is important that the data types of the formal parameter and the actual parameter are the same.

# EXERCISE 7-2: WRITING FUNCTIONS THAT REQUIRE
A SINGLE PARAMETER

In this exercise, you use what you have learned about writing functions that require a single parameter in C++.

+   1. Given the following variable declarations and function calls, write the function’s header and function declaration:
+   
+      a. `string name;`
+   
+      `printBirthdayInvitation(name);`
+   
+      b. `double side_length;`
+   
+      `displaySquareArea(side_length);`
+   
+      c. `int month;`
+   
+      `displayDaysInMonth(month);`