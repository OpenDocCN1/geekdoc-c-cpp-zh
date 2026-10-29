# Self-Test Exercises (continued)

8. Suppose we expect the elements of the array a to be ordered so that

```
a[0] <= a[1] <= a[2] <= ...
```

However, to be safe we want our program to test the array and issue a warning in case it turns out that some elements are out of order. The following code is supposed to output such a warning, but it contains a bug. What is it?

```
double a[10];
<Same code to fill the array a goes here.>
for (int index = 0; index < 10; index++)
    if (a[index] > a[index + 1])
        cout << "Array elements " << index << " and " << (index + 1) << " are out of order.";
```

9. Write some C++ code that will fill an array a with 20 values of type int read in from the keyboard. You need not write a full program, just the code to do this, but do give the declarations for the array and for all variables.

10. Suppose you have the following array declaration in your program:

```
int yourArray[7];
```

Also, suppose that in your implementation of C++, variables of type int use two bytes of memory. When you run your program, how much memory will this array consume? Suppose that, when you run your program, the system assigns the memory address 1000 to the indexed variable yourArray[0]. What will be the address of the indexed variable yourArray[3]?

# 5.2 Arrays in Functions

You can use both array indexed variables and entire arrays as arguments to functions. We first discuss array indexed variables as arguments to functions.

# Indexed Variables as Function Arguments

An indexed variable can be an argument to a function in exactly the same way that any variable of the array base type can be an argument. For example, suppose a program contains the following declarations:

```
double i, n, a[10];
```

If myFunction takes one argument of type double, then the following is legal:

```
myFunction(n);
```

Since an indexed variable of the array a is also a variable of type double, just like n, the following is equally legal:

```
myFunction(a[3]);
```