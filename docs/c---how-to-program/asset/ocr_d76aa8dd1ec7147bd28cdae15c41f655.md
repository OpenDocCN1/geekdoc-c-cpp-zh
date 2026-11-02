```
g)  #if TRUE
        #define FALSE 0
        #else
            #define FALSE 1
        #endif
h)  #define CUBE_VOLUME(x)  ((x) * (x) * (x))
```

# Exercises

**13.4**  _(_Volume of a Sphere_)_ Write a program that defines a macro with one argument to compute the volume of a sphere. The program should compute the volume for spheres of radius 1 to 10 and print the results in tabular format. The formula for the volume of a sphere is

(4.0 / 3) * π * r³

where π is 3.14159.

**13.5**  _(_Adding Two Numbers_)_ Write a program that defines macro SUM with two arguments, x and y, and use SUM to produce the following output:

```
The sum of x and y is 13
```

**13.6**  _(_Smallest of Two Numbers_)_ Write a program that defines and uses macro MINIMUM2 to determine the smallest of two numeric values. Input the values from the keyboard.

**13.7**  _(_Smallest of Three Numbers_)_ Write a program that defines and uses macro MINIMUM3 to determine the smallest of three numeric values. Macro MINIMUM3 should use macro MINIMUM2 defined in Exercise 13.6 to determine the smallest number. Input the values from the keyboard.

**13.8**  _(_Printing a String_)_ Write a program that defines and uses macro PRINT to print a string value.

**13.9**  _(_Printing an Array_)_ Write a program that defines and uses macro PRINTARRAY to print an array of integers. The macro should receive the array and the number of elements in the array as arguments.

**13.10**  _(_Totaling an Array's Contents_)_ Write a program that defines and uses macro SUMARRAY to sum the values in a numeric array. The macro should receive the array and the number of elements in the array as arguments.