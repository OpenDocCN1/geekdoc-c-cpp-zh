
- d) 0143  
  0x63
- e) 100000  
  +100000
- f) 4.45e+002

## Exercises

### 21.6 (Write C++ Statements) Write a statement for each of the following:

- a) Print integer 40000 left justified in a 15-digit field.
- b) Read a string into character array variable state.
- c) Print 200 with and without a sign.
- d) Print the decimal value 100 in hexadecimal form preceded by 0x.
- e) Read characters into array charArray until the character 'p' is encountered, up to a limit of 10 characters (including the terminating null character). Extract the delimiter from the input stream, and discard it.
- f) Print 1.234 in a 9-digit field with preceding zeros.

### 21.7 (Inputting Decimal, Octal and Hexadecimal Values) Write a program to test the inputting of integer values in decimal, octal and hexadecimal formats. Output each integer read by the program in all three formats. Test the program with the following input data: 10, 010, 0x10.

### 21.8 (Printing Pointer Values as Integers) Write a program that prints pointer values, using casts to all the integer data types. Which ones print strange values? Which ones cause errors?

### 21.9 (Printing with Field Widths) Write a program to test the results of printing the integer value 12345 and the floating-point value 1.2345 in various-sized fields. What happens when the values are printed in fields containing fewer digits than the values?

### 21.10 (Rounding) Write a program that prints the value 100.453627 rounded to the nearest digit, tenth, hundredth, thousandth and ten-thousandth.

### 21.11 (Length of a String) Write a program that inputs a string from the keyboard and determines the length of the string. Print the string in a field width that is twice the length of the string.

### 21.12 (Converting Fahrenheit to Celsius) Write a program that converts integer Fahrenheit temperatures from 0 to 212 degrees to floating-point Celsius temperatures with 3 digits of precision. Use the formula

```
celsius = 5.0 / 9.0 * ( fahrenheit - 32 );
```

to perform the calculation. The output should be printed in two right-justified columns and the Celsius temperatures should be preceded by a sign for both positive and negative values.

### 21.13 In some programming languages, strings are entered surrounded by either single or double quotation marks. Write a program that reads the three strings suzy, "suzy" and 'suzy'. Are the single and double quotes ignored or read as part of the string?

### 21.14 (Reading Phone Numbers with an Overloaded Stream Extraction Operator) In Fig. 18.5, the stream extraction and stream insertion operators were overloaded for input and output of objects of the PhoneNumber class. Rewrite the stream extraction operator to perform the following error checking on input. The operator>> function will need to be reimplemented.

- a) Input the entire phone number into an array. Test that the proper number of characters has been entered. There should be a total of 14 characters read for a phone number of the form (800) 555-1222. Use the ios_base member function clear to set failbit for improper input.
- b) The area code and exchange do not begin with 0 or 1. Test the first digit of the area-code and exchange portions of the phone number to be sure that neither begins with 0 or 1. Use the ios_base member function clear to set failbit for improper input.
- c) The middle digit of an area code used to be limited to 0 or 1 (though this has changed). Test the middle digit for a value of 0 or 1. Use the ios_base member function clear to set failbit for improper input.

If none of the above operations results in failbit being set for improper input, copy the parts of the telephone number into the PhoneNumber object’s areaCode, exchange and line members. If failbit has been set on the input, have the program print an error message and end, rather than print the phone number.

### 21.15 (Point Class) Write a program that accomplishes each of the following:

- a) Create a user-defined class Point that contains the private integer data members xCoordinate and yCoordinate and declares stream insertion and stream extraction overloaded operator functions as friends of the class.
- b) Define the stream insertion and stream extraction operator functions. The stream extraction operator function should determine whether the data entered is valid, and, if not, it should set the failbit to indicate improper input. The stream insertion operator should not be able to display the point after an input error occurred.
- c) Write a main function that tests input and output of user-defined class Point, using the overloaded stream extraction and stream insertion operators.

### 21.16 (Complex Class) Write a program that accomplishes each of the following:

- a) Create a user-defined class Complex that contains the private integer data members real and imaginary and declares stream insertion and stream extraction overloaded operator functions as friends of the class.
- b) Define the stream insertion and stream extraction operator functions. The stream extraction operator function should determine whether the data entered is valid, and, if not, it should set failbit to indicate improper input. The input should be of the form 3 + 8i.
- c) The values can be negative or positive, and it’s possible that one of the two values is not provided, in which case the appropriate data member should be set to 0. The stream insertion operator should not be able to display the point if an input error occurred. For negative imaginary values, a minus sign should be printed rather than a plus sign.
- d) Write a main function that tests input and output of user-defined class Complex, using the overloaded stream extraction and stream insertion operators.

### 21.17 (Printing a Table of ASCII Values) Write a program that uses a for statement to print a table of ASCII values for the characters in the ASCII character set from 33 to 126. The program should print the decimal value, octal value, hexadecimal value and character value for each character. Use the stream manipulators dec, oct and hex to print the integer values.

### 21.18 (String-Terminating Null Character) Write a program to show that the getline and three-argument get istream member functions both end the input string with a string-terminating null character. Also, show that get leaves the delimiter character on the input stream, whereas getline extracts the delimiter character and discards it. What happens to the unread characters in the stream?

- 22.1 Introduction
- 22.2 Example: Handling an Attempt to Divide by Zero
- 22.3 Rethrowing an Exception
- 22.4 Stack Unwinding
- 22.5 When to Use Exception Handling
- 22.6 Constructors, Destructors and Exception Handling
- 22.7 Exceptions and Inheritance
- 22.8 Processing new Failures
- 22.9 Class unique_ptr and Dynamic Memory Allocation
- 22.10 Standard Library Exception Hierarchy
- 22.11 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

## 22.1 Introduction

An exception is an indication of a problem that occurs during a program's execution. Exception handling enables you to create applications that can resolve (or handle) exceptions. In many cases, this allows a program to continue executing as if no problem had been encountered. The features presented in this chapter enable you to write robust and fault-tolerant programs that can deal with problems and continue executing or terminate gracefully.

We begin with a review of exception-handling concepts via an example that demonstrates handling an exception that occurs when a function attempts to divide by zero. We show how to handle exceptions that occur in a constructor or destructor and exceptions that occur if operator new fails to allocate memory for an object. We introduce several C++ Standard Library exception handling classes and show you how to create your own.

> **Software Engineering Observation 22.1**
> Exception handling provides a standard mechanism for processing errors. This is especially important when working on a project with a large team of programmers.

> **Software Engineering Observation 22.2**
> Incorporate your exception-handling strategy into your system from its inception. Including effective exception handling after a system has been implemented can be difficult.

> **Error-Prevention Tip 22.1**
> Without exception handling, it's common for a function to calculate and return a value on success or return an error indicator on failure. A common problem with this architecture is using the return value in a subsequent calculation without first checking whether the value is the error indicator. Exception handling eliminates this problem.

## 22.2 Example: Handling an Attempt to Divide by Zero

Let's consider a simple example of exception handling (Figs. 22.1–22.2). We show how to deal with a common arithmetic problem—division by zero. Division by zero using integer arithmetic typically causes a program to terminate prematurely. In floating-point arithmetic, many C++ implementations allow division by zero, in which case a result of positive or negative infinity is displayed as INF or -INF, respectively.
