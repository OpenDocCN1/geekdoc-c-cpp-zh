The running result of the program is:

```
Enter 3 float point numbers:
4.7
Integer Part=4 Fraction Part=0.7
8.913
Integer Part=8 Fraction Part=0.913
-4.7518
Integer Part=-4 Fraction Part=-0.7518
```

In this program, using references as formal parameters can achieve the same result. Please try to modify the program in Example 6.10 and use references as the parameters of the function.

# 6.2.9 Pointer-Type Functions

Functions have return values after being called, except for void-type functions. Points can also be the return values of functions. When the return value of a function is a pointer, this is a pointer-type function. The primary purpose of using a pointer as the return value of a function is to return large amounts of data from the called function to the calling function when the function finishes. However, if the return value is not a pointer, the called function can only return a variable or an object when it finishes.

The general form of defining a pointer-type function is:

```
data type *function name (parameter list)
{
  function body
}
```

"Data type” denotes the type of the pointer that the function returns; “function name” and “*" identify a function of pointer type; and “parameter list” is the list of the formal parameters of the function.

# 6.2.10 Pointers that Point to Functions

Up to now, all the pointers that we are pointing to data, for example:

```
int *intpart;
float *fracpart;
```

During program execution, not only data take up memory spaces, codes of the executive program are also loaded into memory and take up some memory space. Every