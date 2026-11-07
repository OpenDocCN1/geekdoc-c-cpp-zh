Function automaticArrayInit is also called twice (lines 12 and 16). The automatic local array's elements are initialized with the values 1, 2 and 3 (line 43). The function prints the array, adds 5 to each element and prints the array again. The second time the function is called, the array elements are initialized to 1, 2 and 3 again because the array has automatic storage duration

# Self Check

1 (Multiple Choice) Which of the following statements a), b) or c) is false?

+   - a) A static local variable exists for the duration of the program but is visible only in the function body.
+   - b) A static local array is created and initialized once, not each time the function is called. This reduces program execution time, particularly for programs with frequently called functions that contain large arrays.
+   - c) If you do not explicitly initialize a static array, that array's elements are initialized to zero by default.
+   - d) All of the above statements are true.

Answer: d.

# 6.7 Passing Arrays to Functions

To pass an array argument to a function, specify the array's name without any brackets. For example, if array hourlyTemperatures has been defined as

```
int hourlyTemperatures[HOURS_IN_A_DAY];
```

the function call

```
modifyArray(hourlyTemperatures, HOURS_IN_A_DAY)
```

passes array hourlyTemperatures and its size to function modifyArray.

Recall that all arguments in C are passed by value. However, C automatically passes arrays to functions by reference—the called functions can modify the callers' original array element values. We'll see in Chapter 7 that this is not a contradiction. An array's name evaluates to the address in memory of the array's first element. Because the array's starting address is passed, the called function knows precisely where the array is stored. So, any modifications the called function makes to the array elements change the values of the original array's elements in the caller.

# Showing That an Array Name Is an Address

Figure 6.10 demonstrates that "the value of an array name" is really the address of the array's first element by printing array, &array[0] and &array using the %p conversion specification for printing addresses. The %p conversion specification normally outputs addresses as hexadecimal numbers, but this is compiler-dependent. Hexadecimal (base 16) numbers consist of the digits 0 through 9 and the letters A through F—the hexadecimal equivalents of the decimal numbers 10–15. Online Appendix E provides an in-depth discussion of the relationships among binary (base 2), octal (base 8), decimal (base 10; standard integers) and hexadecimal integers. The output shows