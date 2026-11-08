Looking at the code, you see that in order to declare a constant in C++, you use the keyword const, followed by the data type, followed by the name of the constant. Named constants must be initialized when they are declared and their contents may not be changed during the execution of the program. The three named constants, ADDRESS_LINE1, ADDRESS_LINE2, and ADDRESS_LINE3, are local to the function nameAndAddress because they are declared within the function. An opening curly brace ({) marks the beginning of the function and a closing curly brace (}) marks the end.

The **header** for the method, nameAndAddress, begins with the keyword void, followed by the function name, which is nameAndAddress. The keyword void indicates that the nameAndAddress function does not return a value.

> **NOTE**
> By convention, in C++ the names of constants appear in all uppercase letters. Multiple words are separated with underscores. This makes it easier for you to spot named constants in a long block of code.

Notice that an additional #include preprocessor directive has been added at the beginning of the program. The preprocessor directive #include <string> allows you to use string objects in your C++ program. You will learn more about string objects in subsequent chapters. Also, notice the statement that follows the #include preprocessor directives, void nameAndAddress();. This is called a function declaration or function prototype.

In C++, you must declare all functions that are used in your program before you may call them. A **function declaration** specifies the data type of the value the function returns, the function name, and the data type of any arguments that are passed to the function. The nameAndAddress function returns the data type void. The keyword void is used to specify that this function returns nothing. You will learn more about function declarations and function arguments in Chapter 7 of this book.

> **NOTE**
> Function declarations end with a semicolon (;).

This program is now complete. Figure 3-4 shows the program's output in response to the input William Pryor (for the name), and 1200 (for the balance).

```
Command Prompt
C:\Users\Jo Ann\C++ Pal\Chapter_3\Author First\Student>CustomerBill
Enter customer's first name: William
Enter customer's last name: Pryor
Enter customer's balance: 1200
ABC Manufacturing
123 Industrial Pkwy
Wild Rose, WI 54984
Customer Name: William Pryor
Customer Balance: 1200
C:\Users\Jo Ann\C++ Pal\Chapter_3\Author First\Student>_
```

**Figure 3-4** Output of the CustomerBill program when the input is William Pryor and 1200