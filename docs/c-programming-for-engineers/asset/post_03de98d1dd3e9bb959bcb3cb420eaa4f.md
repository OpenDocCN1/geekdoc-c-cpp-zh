
## Table 5.7: Hardware support for arithmetic on selected microcontrollers

| Board | Microcontroller | Word Size | Integer Add/Subtract | Integer Multiply | Integer Divide | Single-Precision FP | Double-Precision FP |
|---|---|---|---|---|---|---|---|
| Arduino Uno R3 | Atmega328P | 8 | | | | | |
| Seeduino XIAO | ARM Cortex-M0+ | 32 | | | | | |
| Seeduino XIAO ESP32C3 | RISC-V (RV32IMC) | 32 | | | | | |
| Blue Pill | ARM Cortex-M3 | 32 | | | | | |
| NodeMCU | ESP8266 | 32 | | | | | |
| Arduino Uno R4 | ARM Cortex-M4F | 32 | | | | | |
| M5Stack | ESP32 | 32 | | | | | |
| Raspberry Pi 5* | ARM Cortex-A76 | 64 | | | | | |

* Not a microcontroller; listed for comparison

## Summary

In programming, data processing expressions are used to calculate values based on changing inputs. To ensure bug-free code, understanding variables and numeric concepts is crucial, especially when working with embedded systems. This chapter focuses on C arithmetic and bitwise operators. Logical and ternary operators, useful in decision-making structures, will be covered in Chapter 7.

## Questions

- 5.1 What is a modulus operation, and how do you perform it in C?
- 5.2 What is the effect of an integer division compared to a floating-point division?
- 5.3 Write a C program that demonstrates an example of implicit type conversion to an integer in an arithmetic operation.
- 5.4 How do you convert a character to an integer in C?
- 5.5 Write a C program that demonstrates the loss of precision when converting a float to an integer.
- 5.6 Write a C program to convert Fahrenheit to Celsius.
- 5.7 Write a C program to extract the lowest byte of an integer (bits 0-7) and add the value of the second lowest byte (bits 8-15).
- 5.8 Multiply a number by 10 using only shift and add operators.
- 5.9 The value of π can be approximated by 355/113. Write a C program that calculates the perimeter of a circle from a given radius using only integers.
- 5.10 Write a C program that intentionally divides by 0. What happens when it is run?

## Chapter 6

## Standard Input/Output

In this chapter, we will look at the essential C functions for input and output using standard input (stdin) and output devices (stdout). We will go over common functions like printf() and scanf(), as well as character-based input and output using putchar() and getchar(). These functions are important building blocks in C programming because they allow you to create user interfaces for your programs.

## 6.1 Output Formatting with printf

In this section, we will delve into the powerful printf function, which stands for "print formatted." This function allows you to display data on the screen in a specific format. Let us explore its syntax and various formatting options.

### 6.1.1 Basic Syntax

The basic syntax of the printf function is:

```
printf(format_string, arg1, arg2, ...);
```

where:

- format_string is a string that specifies the format of the output.
- arg1, arg2, etc., are the values to be formatted and printed. The number of variables must match the number of format specifiers in the format_string.

Imagine you want to print a person's name and age on separate lines. Here is how you would use printf:

```
int age = 30;
char name[] = "Alice";
printf("Name: %s\nAge: %d\n", name, age);
```

Here, the format string specifies two placeholders: %s for a string and %d for an integer. The \n escape sequence after each format specifier adds a newline character, separating the name and age on different lines. The values following the comma (separated by commas) match these placeholders, producing the output:

Name: Alice
Age: 30

### 6.1.2 Formatting Specifiers

Formatting specifiers are placeholders within the format string that indicate the type and format of the corresponding argument. Some common formatting specifiers include:

## Chapter 6. Standard Input/Output

| Format Specifier | Output |
|---|---|
| %% | Percent sign (%) |
| %%c | Character |
| %%d, %%i | Signed integer |
| %%e, %%f, %%g | Floating-point |
| %%s | String |
| %%x, %%X | Hexadecimal |
| %%o | Octal |
| %%p | Pointer in hexadecimal |
| %%u | Unsigned integer |
| %%ld, %%lu | Long integer |

### 6.1.3 Width and Precision

You can specify the width and precision of the output using the following syntax:

```
printf("%width.precisionf", value);
```

Here, width specifies the minimum field width, and precision specifies the number of digits after the decimal point for floating-point numbers.

### 6.1.4 Flags

Flags modify the output format in various ways. Some commonly used flags include:

| Character | Purpose |
|---|---|
| - | Left-align the output |
| + | Always display a sign (even for positive numbers) |
| 0 | Pad with zeros instead of spaces |
| : | Control decimal places for floating-point numbers |
| w | Minimum field width for the output |

### 6.1.5 Escape Sequences

In printf, backslashes (\) mark the start of special effects within the string. The character right after the backslash indicates the action to be taken. These combinations, called escape sequences, trigger specific effects within the string. Some common escape sequences include:

## 6.2. Floating-Point Numbers

| Escape Character | Output |
|---|---|
| \n | Newline |
| \t | Horizontal tab |
| \r | Carriage return |
| \b | Backspace |
| \f | Form feed |
| \" | Double quote |
| \' | Single quote |
| \\ | Backslash |
| \theta | Null character (ASCII value 0) |
| \a | Alert/bell |
| \v | Vertical tab |
| \xhh | Hexadecimal |
| \000 | Octal |

### 6.1.6 Examples

Here are some examples demonstrating how to use printf to format output in various scenarios.

```
printf("%d\n", alpha);      // use 2 columns
printf("%5d\n", alpha);     // 3 leading spaces
printf("%%-5d\n", alpha);    // 3 trailing space
printf("%%05d\n", alpha);    // 3 leading zeroes
```

Result output:

| 25 |
| 25 | |
| 25 |
| 00025 | |

## 6.2 Printing Floating-Point Numbers

The following are the format specifiers to print floating-point numbers in C:

| Format Specifier | Purpose |
|---|---|
| %%f | Single-precision |
| %%lf | Double-precision |
| %.n | n is the number of digits after decimal point |
| %%e or %%E | Scientific notation * |
| %.w | w is the field width |
| %%g | %f or %e, whichever is shorter |

In C, floating-point numbers can be represented using either the float or double data types. Floats typically have a precision of 6-7 decimal digits, while doubles have a precision of 15-16 decimal digits.

A floating-point number is double by default unless you add 'f' or 'F' to make it float. Therefore, 3.75 is a double, while 3.75f or 3.75F is a float. Double precision is commonly used for most calculations. However, floats save storage if you need to store lots of numbers and tolerate lower precision.

Here is how you can store and print π in both data types:

```
float pi_float = 3.141593;
printf("%.f\n", pi_float); // Output: 3.141593
```

```
double pi_double = 3.141592653589793;
printf("%.15f\n", pi_double); // Output: 3.141592653589793
```

The %f specifies the number as a single-precision floating point number. Since a float has only 6-7 digit precision, providing a more accurate value for π would still yield the same output. Using %E would give you the same precision. The %.15f specifies printing the number with 15 digit precision. If you used the specifier for float when printing a double, the output may be unpredictable.

The %e and %E format specifiers are used to print floating-point numbers in scientific notation. It represents the number in the form of mx10^n, where m and n are integer.

```
double num = 1234.56789;
printf("%e", num); // Output: 1.234568e+03
```

In this example, %e is used to print the variable num. The number 1234.56789 is represented in scientific notation as 1.234568e+03, meaning 1.234568 × 10^3.

The %g specifier is used to print floating-point numbers in either %f or %e format, shorter and more precise.

Here's an example:

```
double num = 1234.56789;
printf("%g", num); // Output: 1234.57
```

In this example, %g is used to print the variable num. Since the number is relatively large, it is printed in %f format with 6 significant digits by default, resulting in "1234.57" being printed.

## 6.3 Input Handling with scanf

The scanf function is used for reading input from the standard input device, typically the keyboard. It allows the programmer to capture data entered by the user and stores the values entered by the user into variables.
