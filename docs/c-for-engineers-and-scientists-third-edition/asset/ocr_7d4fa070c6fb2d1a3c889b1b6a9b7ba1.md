# Chapter 8

# 447
I/O Stream Objects and Methods

The following two runs were made with Program 8.2:

A file by the name prices.dat exists.
Do you want to continue and overwrite it
with the new data (y or n): n
The existing file will not be overwritten.

and

A file by the name prices.dat exists.
Do you want to continue and overwrite it
with the new data (y or n): y
The file has been successfully opened for output.

They can be combined into a single statement:

```
ifstream inFile("prices.dat");
```

# Embedded and Interactive Filenames Programs 8.1 and 8.2 have two problems:

+   - The external filename is embedded in the program code.
- There's no provision for a user to enter the filename while the program is running.

As programs are written, if the filename is to change, a programmer must modify the
extexternal filename in the call to open() and recompile the program. Both problems can be
avoid by assigning the filename to a string variable.

A string variable, used in this book, is a variable that can hold a string value, which is
an sequence of zero or more characters enclosed in quotation marks, such as "Hello
World" and "". Remember that the quotation marks delimit the beginning and end of a
string aren't stored as part of the string.

In declaring and initializing a string variable for an open() method, the string is
considered a C-string. (See the Point of Information "Using C-Strings as Filenames" for
precautions when using a C-string.) A safer alternative, and one used throughout this book,
is to use a string class object and convert it to a C-string using the c_str() method.