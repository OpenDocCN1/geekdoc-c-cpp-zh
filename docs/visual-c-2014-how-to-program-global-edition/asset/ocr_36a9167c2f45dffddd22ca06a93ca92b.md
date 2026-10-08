# Chapter 8 Arrays; Introduction to Exception Handling

# Section 8.10 Case Study: GradeBook Using a Rectangular Array

+   - When the foreach statement traverses a rectangular array's elements, it looks at each element of the first row by index, then each element of the second row by index and so on.

# Section 8.11 Variable-Length Argument Lists

+   - A one-dimensional array declared by params in a method's parameter list indicates that the method receives a variable number of arguments with the type of the array's elements.

+   - The params modifier can affect only the last entry of the parameter list.

+   - C# treats a variable-length argument list as a one-dimensional array.

# Section 8.12 Using Command-Line Arguments

+   - When an app is executed from the Command Prompt, the execution passes the command-line arguments that appear after the app name to the app's Main method as strings in a one-dimensional array.

# Section 8.13 (Optional) Passing Arrays by Value and Reference

+   - When a reference-type object is passed with ref, the called method actually gains control over the reference itself, allowing the method to replace the original reference in the caller with a different object or even null.

+   - If you encounter a situation where you truly want the called procedure to modify the caller's reference, pass the reference-type parameter using keyword ref—but situations are rare.

# Terminology

array
array-access expression
array-creation expression
array initializer
auto-property initializer
bounds checking
catch block
column index
column of an array
command-line arguments
context keyword
element of an array
exception
exception handling
fault-tolerant program
foreach statement
getter-only auto-implemented property
index
zero
IndexOfRangeException
initializer list
iteration variable

jagged array
leading 0
Length property of an array
m-by-n array
magic number
Message of an exception
dimensional array
name of an array
named constant
nested array initializer
params modifier
rectangular array
row index
of an array
square brackets, []
table of values
test harness
tverse an array
try statement
two-dimensional array
variable-length argument list
zeroth element

# Self-Review Exercises

+   8.1 Fill in the blank(s) in each of the following statements: Lists and tables of values can be stored in ____