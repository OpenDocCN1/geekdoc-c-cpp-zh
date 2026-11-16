# 1.8 Managing Input and Output Operations

One of the primary advantages of modern computers is their ability to communicate with the user during program execution. This feature enables the programmer to read the values for the input variables, when the program is in execution without altering the program. Once the required value has been read and the ENTER key is pressed, program execution starts again, and the output is displayed on the screen. To perform input and output operations, C has a number of input and output functions. These functions can be broadly classified into two types. They are,

+   - Formatted I/O functions.
+   - Unformatted I/O functions.

# 1.8.1 Formatted I/O Functions

The formatted input/output functions read any type of data as input from the user and displays any type of data as output in the screen. They use format strings (also referred as conversion specifiers) for identifying the type of the data involved. These functions return an integer value after execution. The return value is equal to the number of values successfully read/written. The return value will be useful for the user to check the correctness of data read/written. The scanf() function is a formatted input function and printf() function is a formatted output function.

# The scanf() Function

The scanf() function permits a program to be interrupted during execution in order to read the required values from the user through the keyboard. scanf stands for "scan function" or "scan formatted". This function (i.e., scanf()) can be used to read any combination of numeric values, single characters and strings. The general form or the syntax of scanf() function is

```
scanf("format_string", Val1, Var2, ... , Varn);
```

where format_string refers to conversion specification which refers to a string containing certain required formatting information and Val1, Var2,.., Varn are arguments that represents individual input data items. Each character group must begin with a % sign followed by a conversion character, which indicates the type of the corresponding data item to be read. A simple form of scanf() function may be

```
scanf("%d", &a);
```

where the variable a has been previously declared as an integer. %d is called as the conversion specifier. Its role is to specify that the number is to be converted to decimal notation before it gets scanned. The ampersand symbol (&) that precedes before the variable name "a" is compulsory, whenever an integer, a floating-point, or a character value is to be read from the user. Actually ampersand (&) means address of, &a means address of a. The value read by the computer after the user has been entered