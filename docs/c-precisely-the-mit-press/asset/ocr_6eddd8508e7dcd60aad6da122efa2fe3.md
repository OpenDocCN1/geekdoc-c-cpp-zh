# Arrays 29

Example 34 Creating and One-Dimensional Arrays
This example rolls a thousand times, then prints the frequencies of the outcomes.

```
Random rnd = new Random(); // Random number generator
int[] freq = new int[6];     // All elements initialized to 0
for (int i=0; i<1000; i++) {
    int die = rnd.Next(1, 7); // Roll die
    freq[die-1] += 1; // Increment frequency
}
for (int c=1; c<=66; c++) Console.WriteLine(c + " came up " + freq[c-1] + " times");
```

Example 35 Using an Initialized Array
Method CheckDate whether a given date is legal in a non-leap year. The array should be created once, outside the method; otherwise a new array is created for every call to the method.

```
static readonly int[] days = { 31, 28, 31, 30, 31, 30, 31, 31, 30, 31 };
static bool CheckDate(int mth, int day)
{ return (mth >= 1) && (mth <= 12) && (day <= days[mth-1]);
```

Example 36 Array Element Type Check at Run-Time
This program compiles all, but at-runtime a[2]=p throws ArrayTypeMismatch, since the class Point of the bound p is not implicitly convertible to a's element type RedPoint.

```
Point[] a = new Point[10]; // Length 10, element type Point
Point p = new Point(42, 117); // Compile-time type Point, class Point
RedPoint cp = new RedPoint(3,4); // Compile-time type Point, class RedPoint
Point p2 = cp; // Compile-time type Point, class RedPoint
a[0] = cp; // OK, RedPoint is subclass of RedPoint
a[1] = p2; // OK, RedPoint is subclass of RedPoint
a[2] = p; // Run-time error: Point is not subclass of RedPoint
```

Example 37 Array Assignment Compatibility
In an assignment = e where a and array type e must be implicitly convertible to a defined in 5.3.2. In this example, the assignment to Object is legal because String and Reference types are legal; the assignment to Object is obviously legal because the arrays have the same element type, and the array creation is legal because the integers 1 and 2 are implicitly convertible to Object by boxing a constructor. The assignments to a3 and a4 are illegal because int is not a reference type and so int[] to Object or double[].

```
Object[] a1 = new String[] { "a", "bc" }; // Legal: array conversion
Object[] a2 = new Object[] { 1, 2 }; // Legal: conversion of 1, 2
Object[] a3 = new int[] { 1, 2 }; // Illegal: no array conversion
double[] a4 = new int[] { 1, 2 }; // Illegal: no array conversion
```

![](bbox=[0.118, 0.928, 0.235, 0.953])