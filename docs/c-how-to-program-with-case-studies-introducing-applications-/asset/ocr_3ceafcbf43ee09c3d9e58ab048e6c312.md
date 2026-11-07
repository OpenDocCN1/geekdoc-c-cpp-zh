```
```c
32      // output value of a[3]
33      printf("\n\nEffects of passing array element "
34             "by value:\n\nThe value of a[3] is %d\n", a[3]);
35
36      modifyElement(a[3]); // pass array element a[3] by value
37
38      // output value of a[3]
39      printf("The value of a[3] is %d\n", a[3]);
40   }
41
42   // in function modifyArray, "b" points to the original array "a" in memory
43   void modifyArray(int b[], size_t size) {
44      // multiply each array element by 2
45      for (size_t j = 0; j < size; ++j) {
46         b[j] *= 2; // actually modifies original array
47      }
48   }
49
50   // in function modifyElement, "e" is a local copy of array element
51   // a[3] passed from main
52   void modifyElement(int e) {
53      e *= 2; // multiply parameter by 2
54      printf("Value in modifyElement is %d\n", e);
55   }
```
```

```
```
Effects of passing entire array by reference:

The values of the original array are:
  0 1 2 3 4
The values of the modified array are:
  0 2 4 6 8


Effects of passing array element by value:

The value of a[3] is 6
Value in modifyElement is 12
The value of a[3] is 6
```
```

**Fig. 6.11** | Passing arrays and individual array elements to functions. (Part 2 of 2.)

# ### Using const to Prevent Functions from Modifying Array Elements

There may be situations in your programs in which a function should not modify array elements. C++'s type qualifier const (short for “constant”) can prevent a function from modifying an argument. When an array parameter is preceded by the const qualifier, the function treats the array elements as constants. Any attempt to modify an array element in the function body results in a compile-time error. This is another example of the principle of least privilege. A function should not be given the capability to modify an array in the caller unless it’s absolutely necessary.

The following definition of a function named tryToModifyArray uses the parameter const int b[] (line 3) to specify that array b is constant and cannot be modified: