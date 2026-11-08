`float`: The data type float is used in C++ to represent any decimal number between −3.4 * 10^38 and 3.4 * 10^38. The memory allocated for a value of the float data type is four bytes.

`double`: The data type double is used in C++ to represent any decimal number between −1.7 * 10^308 and 1.7 * 10^308. The memory allocated for a value of the double data type is eight bytes.

The maximum and minimum values of the data types float and double are system dependent. To find these values on a particular system, you can check your compiler’s documentation or, alternatively, you can run a program given in Appendix F (Header File cfloat).

Other than the set of values, there is one more difference between the data types float and double. The maximum number of significant digits—that is, the number of decimal places—in float values is six or seven. The maximum number of significant digits in values belonging to the double type is 15.

> **NOTE:** For values of the double type, for better precision, some compilers might give more than 15 significant digits. Check your compiler’s documentation.

The maximum number of significant digits is called the **precision**. Sometimes float values are called **single precision**, and values of type double are called **double precision**. If you are dealing with decimal numbers, for the most part you need only the float type; if you need accuracy to more than six or seven decimal places, you can use the double type.

> **NOTE:** In C++, by default, floating-point numbers are considered type double. Therefore, if you use the data type float to manipulate floating-point numbers in a program, certain compilers might give you a warning message, such as “truncation from double to float.” To avoid such warning messages, you should use the double data type. For purposes and to avoid such warning messages in programming examples, this book mostly uses the data type double to manipulate floating-point numbers.

# Data Types and Variables

Now that we know how to define an identifier, what a data type is, and the term variable, we can show how to declare a variable. When we declare a variable, not only do we specify the name of the variable, we also specify what type of data a variable can store. A syntax rule to declare a variable is:

```
dataType identifier;
```