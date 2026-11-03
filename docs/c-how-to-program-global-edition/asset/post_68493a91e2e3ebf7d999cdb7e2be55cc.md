
conversion specifier for printing addresses. The %p conversion specifier normally outputs addresses as hexadecimal numbers, but this is compiler dependent. Hexadecimal (base 16) numbers consist of the digits 0 through 9 and the letters A through F (these letters are the hexadecimal equivalents of the decimal numbers 10–15). Appendix C provides an in-depth discussion of the relationships among binary (base 2), octal (base 8), decimal (base 10; standard integers) and hexadecimal integers. The output shows that array, &array and &array[0] have the same value, namely 0031F930. The output of this program is system dependent, but the addresses are always identical for a particular execution of this program on a particular computer.

![](img/bf54db922e6fa8319cba11069e785521_257_0.png)

## Performance Tip 6.3

*Passing arrays by reference makes sense for performance reasons. If arrays were passed by value, a copy of each element would be passed. For large, frequently passed arrays, this would be time consuming and would consume storage for the copies of the arrays.*

```c
// Fig. 6.12: fig06_12.c
// Array name is the same as the address of the array's first element.
#include <stdio.h>

// function main begins program execution
int main(void)
{
    char array[5]; // define an array of size 5

    printf("    array = %p\n&array[0] = %p\n    &array = %p\n",
           array, &array[0], &array);
}
```

```text
    array = 0031F930
&array[0] = 0031F930
    &array = 0031F930
```

**Fig. 6.12** | Array name is the same as the address of the array’s first element.

![](img/bf54db922e6fa8319cba11069e785521_257_1.png)

## Software Engineering Observation 6.2

*It’s possible to pass an array by value (by placing it in a struct as we explain in Chapter 10, C Structures, Unions, Bit Manipulation and Enumerations).*

Although entire arrays are passed by reference, individual array elements are passed by value exactly as simple variables are. Such simple pieces of data (such as individual ints, floats and chars) are called scalars. To pass an element of an array to a function, use the indexed name of the array element as an argument in the function call. In Chapter 7, we show how to pass scalars (i.e., individual variables and array elements) to functions by reference.

For a function to receive an array through a function call, the function’s parameter list must specify that an array will be received. For example, the function header for function modifyArray (that we called earlier in this section) might be written as

```c
void modifyArray(int b[], size_t size)
```

indicating that `modifyArray` expects to receive an array of integers in parameter `b` and the number of array elements in parameter `size`. The size of the array is not required between the array brackets. If it's included, the compiler checks that it's greater than zero, then ignores it. Specifying a negative size is a compilation error. Because arrays are automatically passed by reference, when the called function uses the array name `b`, it will be referring to the array in the caller (array `hourlyTemperatures` in the preceding call). In Chapter 7, we introduce other notations for indicating that an array is being received by a function. As we'll see, these notations are based on the intimate relationship between arrays and pointers.

### Difference Between Passing an Entire Array and Passing an Array Element

Figure 6.13 demonstrates the difference between passing an entire array and passing an individual array element. The program first prints the five elements of integer array `a` (lines 19–21). Next, `a` and its size are passed to function `modifyArray` (line 25), where each of `a`'s elements is multiplied by 2 (lines 48–50). Then `a` is reprinted in `main` (lines 29–31). As the output shows, the elements of `a` are indeed modified by `modifyArray`. Now the program prints the value of `a[3]` (line 35) and passes it to function `modifyElement` (line 37). Function `modifyElement` multiplies its argument by 2 (line 58) and prints the new value. When `a[3]` is reprinted in `main` (line 40), it has not been modified, because individual array elements are passed by value.

```c
1   // Fig. 6.13: fig06_13.c
2   // Passing arrays and individual array elements to functions.
3   #include <stdio.h>
4   #define SIZE 5
5
6   // function prototypes
7   void modifyArray(int b[], size_t size);
8   void modifyElement(int e);
9
10  // function main begins program execution
11  int main(void)
12  {
13     int a[SIZE] = {0, 1, 2, 3, 4}; // initialize array a
14
15     puts("Effects of passing entire array by reference:\n\nThe "
16          "values of the original array are:");
17
18     // output original array
19     for (size_t i = 0; i < SIZE; ++i) {
20        printf("%3d", a[i]);
21     }
22
23     puts(""); // outputs a newline
24
25     modifyArray(a, SIZE); // pass array a to modifyArray by reference
26     puts("The values of the modified array are:");
```

**Fig. 6.13** | Passing arrays and individual array elements to functions. (Part 1 of 2.)

```c
28    // output modified array
29    for (size_t i = 0; i < SIZE; ++i) {
30        printf("%3d", a[i]);
31    }
32
33    // output value of a[3]
34    printf("\n\nEffects of passing array element "
35           "by value:\nThe value of a[3] is %d\n", a[3]);
36
37    modifyElement(a[3]); // pass array element a[3] by value
38
39    // output value of a[3]
40    printf("The value of a[3] is %d\n", a[3]);
41 }
42
43 // in function modifyArray, "b" points to the original array "a"
44 // in memory
45 void modifyArray(int b[], size_t size)
46 {
47    // multiply each array element by 2
48    for (size_t j = 0; j < size; ++j) {
49        b[j] *= 2; // actually modifies original array
50    }
51 }
52
53 // in function modifyElement, "e" is a local copy of array element
54 // a[3] passed from main
55 void modifyElement(int e)
56 {
57    // multiply parameter by 2
58    printf("Value in modifyElement is %d\n", e *= 2);
59 }
```

```
Effects of passing entire array by reference:

The values of the original array are:
  0  1  2  3  4
The values of the modified array are:
  0  2  4  6  8

Effects of passing array element by value:

The value of a[3] is 6
Value in modifyElement is 12
The value of a[3] is 6
```

Fig. 6.13 | Passing arrays and individual array elements to functions. (Part 2 of 2.)

There may be situations in your programs in which a function should not be allowed to modify array elements. C provides the type qualifier const (for “constant”) that can be used to prevent modification of array values in a function. When an array parameter is preceded by the const qualifier, the array elements become constant in the function body—any attempt to modify an element of the array in the function body results in a compile-time error.

## Using the const Qualifier with Array Parameters

Figure 6.14 shows the definition of a function named tryToModifyArray that's defined with the parameter const int b[] (line 3). This specifies that array b is constant and cannot be modified. Each of the function's attempts to modify array elements results in a compiler error. The const qualifier is discussed in additional contexts in Chapter 7.

> **Software Engineering Observation 6.3**
> The const type qualifier can be applied to an array parameter in a function definition to prevent the original array from being modified in the function body. This is another example of the principle of least privilege. A function should not be given the capability to modify an array in the caller unless it's absolutely necessary.

```c
1 // in function tryToModifyArray, array b is const, so it cannot be
2 // used to modify its array argument in the caller
3 void tryToModifyArray(const int b[])
4 {
5 b[0] /= 2; // error
6 b[1] /= 2; // error
7 b[2] /= 2; // error
8 }
```

Fig. 6.14 | Using the const type qualifier with arrays.

## 6.8 Sorting Arrays

Sorting data (i.e., placing the data into ascending or descending order) is one of the most important computing applications. A bank sorts all checks by account number so that it can prepare individual bank statements at the end of each month. Telephone companies sort their lists of accounts by last name and, within that, by first name to make it easy to find phone numbers. Virtually every organization must sort some data, and in many cases massive amounts of it. Sorting data is an intriguing problem which has attracted some of the most intense research efforts in the field of computer science. In this chapter we discuss a simple sorting scheme. In Chapter 12 and Appendix D, we investigate more complex schemes that yield better performance.

> **Performance Tip 6.4**
> Often, the simplest algorithms perform poorly. Their virtue is that they're easy to write, test and debug. More complex algorithms are often needed to realize maximum performance.

Figure 6.15 sorts the values in the elements of the 10-element array a (line 10) into ascending order. The technique we use is called the bubble sort or the sinking sort because the smaller values gradually "bubble" their way upward to the top of the array like air bubbles rising in water, while the larger values sink to the bottom of the array. The technique is to make several passes through the array. On each pass, successive pairs of elements (element 0 and element 1, then element 1 and element 2, etc.) are compared. If a pair is in
