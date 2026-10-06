# Chapter 8 Arrays

holds the names of 50 employees. Imagine declaring 50 variables to hold all of those names:

```
Declare String employee1
Declare String employee2
Declare String employee3
and so on...
Declare String employee50
```

Then, imagine designing the code to input all 50 names:

```
// Get the first employee name.
Display "Enter the name of employee 1."
Input employee1
```

```
// Get the second employee name.
Display "Enter the name of employee 2."
Input employee2
```

```
// Get the third employee name.
Display "Enter the name of employee 3."
Input employee3
and so on...
```

```
// Get the fiftieth employee name.
Display "Enter the name of employee 50."
Input employee50
```

As you can see, variables are not well-suited for storing and processing lists of data. Each variable is a separate item that must be declared and individually processed. Fortunately, most programming languages allow you to create arrays, which are specifically designed for storing and processing lists of data. Like a variable, an array is a named storage location in memory. Unlike a variable, an array can hold a group of values. All of the values in an array must be the same data type. You can have an array of Integers, an array of Reals, or an array of Strings, but you cannot store a mixture of data types in an array. The following example shows how we declare an array in pseudocode:

```
Declare Integer units[10]
```

Notice that this statement looks like a regular variable declaration except for the number inside brackets. The number inside the brackets, a size declarator, specifies the number of values that the array can hold. This pseudocode declares an array units that can hold 10 values. In most programming languages, an array size declarator must be a nonnegative integer. Here is another example:

```
Declare Real salesAmounts[7]
```

This statement declares an array named salesAmounts that can hold 7 real numbers. The following pseudocode shows one more example. This statement declares an array that can hold 50 strings. The name of the array is names.

```
Declare String names[50]
```

In most languages, an array's size cannot be changed while the program is running. If you have written a program that uses an array and then you find that you change