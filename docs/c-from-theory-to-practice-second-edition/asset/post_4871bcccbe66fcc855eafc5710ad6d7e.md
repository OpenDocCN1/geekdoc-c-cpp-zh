
## U.6.5
What is the output of the following program? You are reminded that printf() returns the number of the displayed characters.

```
#include <stdio.h>
int main(void)
{
    int i, sum;
    float j = 1.2345;
    sum = 0;
    for(i = 0; i < 3; i++)
        sum = sum + printf("%.2f\n", j);
    printf("Val = %d\n", sum);
    return 0;
}
```

## U.6.6
Write a program that reads continuously daily temperatures and displays the percentage of those with a temperature equal, less, or more than 40°F. If the user enters 1000, the insertion of temperatures should terminate.

## U.6.7
Write a program that reads up to 100 integers. If an input number is greater than the last entered, the insertion of numbers should terminate and the program should display how many numbers were entered.

## U.6.8
Write a program that reads three integers (e.g., a, b, and c) one after the other, not all together. The program should force the user to enter the numbers in descending order (i.e., a > b > c).

## U.6.9
Write a program that reads the initial height from which a ball is thrown and displays after how many bounces the ball reaches a height less than ¼ of the initial height. The program should prompt the user to enter the decrease height ratio (%). For example, the input value 0.1 means that each time the ball hits the ground, it bounces up to a height 10% less than the previous one.

## U.6.10
Write a program that reads integers continuously until the user enters 0. Then, the program should display the largest positive and the smallest negative input numbers. If the user enters only positive or negative numbers, the program should display an informative message. Zero is counted as neither a positive nor a negative number.

## U.6.11
Write a program that is mandatory to read 10 positive numbers. If an input number is negative, the program should prompt the user to enter another one. The program should display how many negative numbers were entered, before it terminates. Use a for loop. Zero is counted as neither a positive or negative number.

## U.6.12
Write a program that reads 10 integers and displays how many times the user entered successive values. For example, if the user enters: -5, 10, 17, -31, -30, -29, 75, 76, 9, -4, the program should display 3 due to the pairs: {-31, -30}, {-30, -29}, and {75, 76}.

## U.6.13
How many terms should be added by the series:
S₁ = 4 + 10 + 16 + 22 + ...
S₂ = 1 + 8 + 15 + 22 + ...

so that S₂ becomes at least 100 greater than S₁. Use a do-while loop.

## U.6.14
Write a program that reads an integer and displays the number of its bits set. For example, if the user enters 30 (in binary: 000000000000000000000000011110), the program should display 4.

## U.6.15
Write a program that uses rand() to generate the integers 0 and 1 in a random manner. The program should read an integer that corresponds to rand() calls and displays the maximum number of successive 0 and 1 pairs in the generated sequence. For example, if the user enters 15, rand() should be called 15 times, and if, let's say, the generated sequence is 010011010100, the program should display 2 because that is the maximum number of pairs with successive 01.

## U.6.16
What is the output of the following program? Explain why.

```
#include <stdio.h>
int main(void)
{
    int i, j, k = 100;
    for(i = 0; i < 2; i++)
    {
        printf("One ");
        for(j = 0; k; j++)
        {
            printf("Two ");
            k -= 50;
        }
    }
    return 0;
}
```

## U.6.17
Write a program that reads an integer that corresponds to a number of lines. The program should display in the first line a number of '*' equal to the input number, and one less in each next line. For example, if the user enters 5 the program should display:
*****
****
***
**
*

## U.6.18
Write a program that reads an integer that corresponds to a number of lines. Suppose that the user enters 4. The program should add spaces and '*' according to the line number, as shown in the following (three spaces at the left of one '*' in the first line, two spaces at the left of two '*' in the second line, and so on). When the last line is reached, the program should display in each line one '*' less, and the spaces at the right of '*', until one '*' is displayed.

```
    *
   **
  ***
 ****
  ***
   **
    *
```

## U.6.19
Write a program that reads two integers (e.g., M, N) and produces a M×N grid. Each grid cell should be 3×2 characters wide. As an example, a 3×5 grid follows:

```
+--+--+--+--+--+
|  |  |  |  |  |
+--+--+--+--+--+
|  |  |  |  |  |
+--+--+--+--+--+
|  |  |  |  |  |
+--+--+--+--+--+
```

The three horizontal characters of each cell are: +-- and the two verticals are: +|

## U.6.20
Write a program that reads a positive integer (e.g., N) and calculates the sum of:

\(\frac{5}{3}+\frac{25}{9}+\frac{125}{27}+\cdots\)

until it becomes greater than N. The program should display the last valid sum and the number of its terms, before it terminates.

## U.6.21
Write a program that reads an integer (e.g., N) and displays the sum of:

\(\frac{1}{1\times3}+\frac{1}{3\times5}+\frac{1}{5\times7}+\cdots+\frac{1}{(N-2)\times N}\).

The program should force the user to enter an odd number greater than or equal to 3.

## U.6.22
Write a program that reads an integer (e.g., N) and displays the sum of: \(2^2+4^2+6^2+\cdots+(2\times N)^2\). The program should force the user to enter a positive integer less than 20.

Use one loop.

## U.6.23
Write a program that reads 100 integers and displays the integer that was given the most successive times. If more than one number was given the same most successive times, your program should display the last one.

## U.6.24
Write a program that reads 100 integers and displays the two different higher values.

## U.6.25
Write a program that reads an integer and displays the prime numbers that are less than or equal to it. You are reminded that a prime number is any integer greater than 1 with no divisor other than 1 and itself.

## U.6.26
Write a program that reads an integer and displays its digits in words. If the number is negative, it should begin with the word minus. The program should accept integers up to five digits. For example, if the user enters -12, the program should display minus one two.

## U.6.27
Write a program that reads a positive integer and checks if it is an Armstrong number. An Armstrong number is a number that it is equal to the sum of its digits raised to the power of the number of digits. For example, the three-digit number 153 is an Armstrong number, because 1³ + 5³ + 3³ = 1 + 125 + 27 = 153.

## 7 Arrays
The variables we’ve used so far can store a single value. In this chapter, we’ll talk about a new type of variable capable of storing a number of values. This type is called array. An array may be multidimensional. We’ll focus on the simplest and most usual kinds: the one-dimensional and two-dimensional arrays. To introduce you to arrays, we’ll show you how to use arrays of integers and floating-point numbers. We’ll discuss other types of arrays, as well as their close relationship to pointers in later chapters. In Chapter 12, we’ll describe some popular algorithms for searching a value in an array and sorting its elements.

## One-Dimensional Arrays
An array is a data structure that contains a number of values, or else elements, of the same type. Each element can be accessed by its position within the array.

### Declaring Arrays
To declare a one-dimensional array, we must specify its name, the number of its elements, and its data type, like this:

```
data_type array_name[number_of_elements];
```

The number_of_elements, or else the length of the array, is specified by an integer constant expression greater than 0 enclosed in brackets. A popular error is to use a variable whose value is set during the program execution. No, it is not allowed. All the elements are of the same type; it may be of any type (e.g., int, float, char, ...). For example, the statement:

`int arr[1000];` declares the array `arr` with 1000 elements of type `int`. To realize the importance of arrays, imagine that if C didn’t support this type of aggregate variable, we’d have to declare 1000 different integer variables.

> > **Tip**
> >
> > The length of an array cannot change during the program execution. It remains fixed.

If the length of the array is used several times in the program, a good practice is to use a macro instead. If you ever need to change it, you just change the macro. For example:

```
#define SIZE 150
float arr[SIZE]; /* The compiler replaces SIZE with 150 and creates an array of 150 floats. */
```
