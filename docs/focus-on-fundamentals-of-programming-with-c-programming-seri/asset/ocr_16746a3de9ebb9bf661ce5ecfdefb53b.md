# scanf_s() Function

scanf_s() is a function standard library which allows you to input values into a program from standard input (keyboard). It's usually used to input numerical data using formats similar to the printf() statement.

Note that scanf() is the traditional ANSI C function used to capture user input and is used in a Mac, Linux, or other non-Microsoft environment. However, as most students typically use Microsoft's Visual Studio, the text will utilize Microsoft's more secure scanf_s() function.

Like printf(), scanf_s() has a control string, followed by the list of items to be read. However scanf_s() wants to know the addresses of the items to be read, since it is a function which will change those values. Therefore the names of variables are preceded by the & sign. Note that character strings are an exception to this. Since a string is already a character pointer, we give the names of string variables unmodified by a leading & (more on strings later).

In the expression:

```
scanf_s("%d %d", &x, &y);
```

the arguments &x and &y tell scanf_s() where to store the data that it reads. & is an operator in C which gives the address of its operand, i.e., &x gives the address of x. Note that the arguments to the scanf_s() function MUST be pointers to the locations in memory (addresses) where the input is to be stored.

Here are scanf_s() fomat codes:

| Code | Meaning |
| :--- | :--- |
| %c | read a character |
| %d | read a decimal integer |
| %ld | reads a long decimal integer |
| %f | read a floating point number |
| %lf | reads a double |
| %h | read a short integer |
| %x | read a hexadecimal number |
| %s | read a string |