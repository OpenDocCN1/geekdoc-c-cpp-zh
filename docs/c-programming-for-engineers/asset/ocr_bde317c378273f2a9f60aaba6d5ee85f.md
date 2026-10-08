# 10.8 Library Functions

10.6 The following function is supposed to return the sum of two integers, but it does not compile. Identify and fix the issue.

```
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {
    printf("%d\n", add(3, 5));
    return 0;
}
```

10.7 The function below is meant to return the factorial of a number but produces incorrect results for some inputs. Identify the issue and correct it.

```
#include <stdio.h>

int factorial(int n) {
    if (n == 0)
        return 0;
    else
        return n * factorial(n - 1);
}

int main() {
    printf("%d\n", factorial(5)); // Expected: 120
    return 0;
}
```

10.8 Write a function celf2ah() to convert Celsius to Fahrenheit. Test the function with -40, 0, 40, and 100 degrees Celsius to check the accuracy of conversion.

10.9 Write a program to generate an array of integers, grade[60]. Fill with random numbers 0-100 then find mean, median and standard deviation of the generated numbers.

10.10 Modify the program so that each element is defined by adding two random numbers, i.e. (rand() % 51) + (rand() % 51) and compare the standard deviation against the previous method.

10.11 Write a C function that takes an integer array and its size as arguments, and returns a new array with the elements in reverse order.

10.12 Write a program that defines and calls a C function that takes an array of integers and its length as arguments and returns the average of its elements.

10.13 Write a program that defines and calls a C function that takes a character as an argument and checks if it is a vowel or a consonant.

10.14 Write a program that defines and calls a C function that takes an array of integers and its length as arguments and finds the maximum and minimum values in the array.