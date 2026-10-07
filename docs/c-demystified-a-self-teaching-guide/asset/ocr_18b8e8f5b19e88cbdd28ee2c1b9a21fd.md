# Initialization

As first discussed in Chapter 3, initialization is when when you assign a value to a variable in the same statement that you declare that variable. By contrast, assignment is when you assign a value to a variable in a statement after the one in which you declare that.

We will discuss assigning values to an array later in this chapter the "Assigning and Displaying Array Values." This section covers initialization of an array.

You have two alternative methods of initializing an array. The first alternative is explicit array sizing, in which the brackets contain a numerical constant that specifies the size of the array. The second alternative is implicit array sizing, in which the square brackets are empty and the size of the array is indicated implicitly by the number of elements on the right side of the assignment operator.

# Explicit Array Sizing

The following are examples of explicit array sizing:

```
int testScore[3] = { 74, 87, 91 };
float milesPerGallon[4] = { 44.4, 22.3, 11.6, 33.3 };
char grades[5] = { 'A', 'B', 'C', 'D', 'F' };
string strings[7] = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };
```

The syntax of initialization, with explicit and implicit array sizing, is that the declaration, as testScore[3]; is followed by an assignment operator and then, enclosed in curly braces, the values to assign to each array, in order, are separated by commas. For example, in the following statement, the value of the first element of the array (testScore[0]) would be 74, the value of the second element of the array 87, and the value of the third element of the array 91.

```
int testScore[3] = { 74, 87, 91 };
```

The number of elements on the right-hand side of the assignment operator cannot be greater than the number within the square brackets. The following statement will not compile, the error message being "many initializers".

```
float milesPerGallon[4] = { 44.4, 22.3, 11.6, 33.3, 7.4 }; //
won't compile
```

You do not have to assign values to each element of the array; the number of elements on the right-hand side of the assignment operator may be less than the number within the square brackets:

```
float milesPerGallon[4] = { 44.4, 22.3, 11.6 };
```

If you do not initialize all the elements of an array, the uninitialized elements have a default value depends on the data type of the array. For example, the default value is 0 for an integer array, 0.0 for a float array, and the null character, "0", for a character array.

> Note The null character is discussed later in this chapter the section "Initializing a Character Array."