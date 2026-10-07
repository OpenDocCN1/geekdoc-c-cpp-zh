# DO

# DON'T

DO use #define statements to create constants that can be used when declaring arrays. Then you can easily change the number of elements in the array. In grades.c, for example, you could change the number of students in the #define, and you wouldn't have to make any other changes in the program.

DON'T use multidimensional arrays with more than three dimensions if you can avoid them. Remember, multidimensional arrays can get big very quickly.

# Initializing Arrays

You can initialize all or part of an array when you first declare it. Follow the array declaration with an sign and list of values enclosed in braces and separated by commas. The listed values are assigned to array elements starting at number 0.

Consider the following code:

```
int array[4] = { 100, 200, 300, 400 };
```

For this example, the value 100 is assigned to array[0], the value 200 is assigned to array[1], the value 300 is assigned to array[2], and the value 400 is assigned to array[3].

If you omit the array size, the compiler creates an array large enough to hold the initialization values. Thus, the following statement would have exactly the same effect as the previous array declaration statement:

```
int array[] = { 100, 200, 300, 400 };
```

You can, however, include too few initialization values, as in this example:

```
int array[10] = { 1, 2, 3 };
```

If you don't explicitly initialize an array element, you can't be sure what value it holds when the program runs. If you include many initializers (more initializers than array elements), the compiler detects an error. According to the ANSI standard, the elements that are not initialized will be set to zero.

> TIP Don't rely on the compiler to automatically initialize values. It is best to make sure you know what a value is initialized by setting it yourself.