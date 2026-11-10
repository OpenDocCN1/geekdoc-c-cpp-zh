
- 5. What is the purpose of the comma operator? Which control statement does the comma operator usually appear in?
- 6. Why is the use of the `goto` statement generally discouraged? Under what conditions might the `goto` statement be helpful? What types of usage should be avoided and why?
- 7. Differentiate between a `for` loop and a `while` loop. Discuss the usage of each.
- 8. Distinguish between the following:
  - (a) do-while and while loop
  - (b) break and continue
- 9. Write a program using conditional operators to determine whether a year entered through the keyboard is a leap year or not.
- 10. The factorial of an integer n is the product of consecutive integers from 1 to n. That is, factorial n = n! = n × (n - 1) × (n - 2) × (n - 3) × ... × 3 × 2 × 1. Write a C program to find the factorial value of n.
- 11. Write a C program to print the quotient of an integer number without using `/`.
- 12. Write a program to print all the even and odd numbers of a certain range as indicated by the user.
- 13. Write a C program to convert an integer number into its binary equivalent without using an array.
- 14. Write a C program to find the prime factors of a number given by the user.
- 15. Write a C program to check whether a number is a power of 2 or not.
- 16. Write a program to find the GCD of two numbers.
- 17. Write a program to find the sum of digits of a number given by the user.
- 18. Write a C program to calculate the sum of prime numbers in a range.
- 19. Write a C program to print the sum of the following series up to n terms where n is given by the user.

  1 + x + x²/2! + x³/3! + ... (The value of x is also given by the user.)

- 20. Write a C program to print the sum of the following series up to n terms where n is given by the user.

  x - x³/3! + x⁵/5! - ... (The value of x is given by the user.)

- 21. Write a C program to print the following series: 0 1 1 2 3 5 8 13 ... The number of terms to be printed should be given by the user.
- 22. Write a C program to print the numbers that do not appear in the Fibonacci series. The number of such terms to be printed should be given by the user.
- 23. Write a program to convert a decimal number into any base.
- 24. Write a program to check whether a number is a Krishnamurthy number or not. A Krishnamurthy number is one whose sum of factorial of digits equals the number.
- 25. Write a program to print the second largest number among a list of numbers without using an array.
- 26. Write programs to print the sum of the following series (with and without `pow()` library function).
  - (a) S = 1 + x + x² + x³ + x⁴ + ... n terms
  - (b) S = -x + x² + x³ + ... n terms
  - (c) S = 1 + x + x²/2! + x³/3! + ... n terms
  - (d) S = 1 + (1+2) + (1+2+3) + ... n terms
  - (e) S = 1 - x + x²/2! - x³/3! + ... n terms
  - (f) S = x - x³/3! + x⁵/5! + ... n terms
  - (g) S = 2 + 22 + 222 + 2222 + ... n terms
  - (h) S = 1 + x/4 + x²/8 + ... n terms
  - (i) S = x - x²/2! + x³/3! - x⁴/4! ... n terms
- 27. Write a program to print the prime numbers in a range.
- 28. Given a number, write a program using a while loop to reverse the digits of the number. For example, the number 12345 should be written as 54321.
- 29. Write a program to print the following triangle.
  - (a)

    ```text
    *
    * *     * * *
    * * * * ... up to nth line
    ```
  - (b)

    ```text
    *
    * *
    * * *
    * * * * * ... up to nth line
    ```
  - (c)

    ```text
    1
    1 2
    1 2 3
    1 2 3 4 ... up to nth line
    ```
  - (d)

    ```text
    1
    2 1 2
    3 2 1 2 3 ... up to nth line
    ```
  - (e)

    ```text
    1
    2 2
    3 3 3
    4 4 4 4
    5 5 5 5 5 ... up to nth line
    ```
- 30. Write a program to check whether a number is a prime number or not.
- 31. Write a program to print all the prime numbers of a certain range given by the user.
- 32. Write a program to print the Floyd’s triangle.
- 33. Write a program to add the prime numbers of a certain range given by the user.

## PROJECT QUESTIONS

- 1. Write a C program that prompts the user to enter the date as three integer values for the month, the day in the month, and the year. The program should then output the date in the form 31st December 2003 when the user enters, say, 12 31 2003. The program has to work out when superscripts “th”, “nd”, “st”, and “rd” need to be appended to the day value. The programmer should not forget 1st, 2nd, 3rd, 4th; and then 11th, 12th, 13th, 14th; and 21st, 22nd, 23rd, and 24th.
- 2. This is a well-known game with a number of variants. The following variant has an interesting winning strategy. Two players alternately take marbles from a pile. In each move, a player chooses how many marbles to take. The player must take at least one but at most half of the marbles. Then the other player takes a turn. The player who takes the last marble loses. Write a C program in which the computer plays against a human opponent. Generate a random integer between 10 and 100 to denote the initial size of the pile. Generate a random integer between 0 and 1 to decide whether the computer or the human takes the first turn. Generate a random integer between 0 and 1 to decide whether the computer plays smart or stupid. In stupid mode the computer simply takes a random legal value (between 1 and n/2, where n is the total number of marbles) from the pile whenever it has a turn. In smart mode the computer takes off enough marbles to make the size of the pile a power of two minus 1—that is, 3, 7, 15, 31, or 63. That is always a legal move, except when the size of the pile is currently one less than a power of two. In that case, the computer makes a random legal move. It should be noted that the computer cannot be beaten in smart mode when it has the first move, unless the pile size happens to be 15, 31, or 63. Of course a human player who has the first turn and knows the winning strategy can win against the computer.

## Chapter 11: Arrays and Strings

### Learning Objectives

After studying this chapter, the readers will be able to

- define an array
- explain one-dimensional arrays, their declaration, initialization, ways to access individual array elements, representation of array elements in memory, and other possible operations
- discuss one-dimensional strings and the way they are declared, initialized, manipulated, inputted, and displayed
- explain two-dimensional arrays, initialization of sized and unsized two-dimensional arrays, accessing elements in such arrays, and their uses
- explain array of strings, their declaration, initialization, other operations, manipulations, and uses
- get a brief idea of three-dimensional arrays or even larger ones

### 11.1 Introduction

The variables used so far have all had a common characteristic: each variable can only be used to store a single value at a time. For example, each of the variables ch, n, and price declared in the statements

```c
char ch;
int n;
float price;
```

are of different data types and each variable can only store one value of the declared data type. These types of variables are called *scalar variables*. A scalar variable is a single variable whose stored value is an *atomic type*. This means that the value cannot be further subdivided or separated into a legitimate data type.

In contrast to atomic types, such as integer, floating point, and double precision data, there are aggregate types. An aggregate type, which is referred to as both a *structured type* and a *data structure*, is any type whose values can be decomposed and are related by some defined structure. Additionally, operations must be available for retrieving and updating individual values in the data structure. Such a *derived data type* is an array.

### Why array?

Consider a brand-new problem: a program that can print its input in reverse order. If there are two values, this is easy and the program is

```c
#include <stdio.h>
int main()
{
    int v1, v2;
    printf("Enter two values:");
    scanf("%d %d", &v1, &v2);
    printf("%d\n%d\n", v2, v1);
    return 0;
}
```

If there are three values, this is still relatively easy and the program is

```c
#include <stdio.h>
int main()
{
    int v1, v2, v3;
    printf("Enter three values: ");
    scanf("%d %d %d", &v1, &v2, &v3);
    printf("%d\n %d\n %d \n", v3, v2, v1);
    return 0;
}
```

But what if there are ten or twenty or one hundred values? Then it is not so easy.

Besides that, the solutions work only if the number of inputs exactly matches with those expected by the user.
Consider another problem: the average of *n* integer numbers given by the user can easily be computed as follows.

```c
#include <stdio.h>
int main()
{
    int count,s=0, n, num;
    float avg;
    printf("\n How many numbers?");
    scanf("%d", &n);
    for(count=1;count<=n;++count)
    {
        printf("\n Enter the Number:");
        scanf("%d", &num);
        s+=num;
    }
    avg=(float)s/n;
    printf("Average is %f", avg);
    return 0;
}
```

Now if the problem is given as 'Print the numbers that are greater than the average', then one solution is to read the numbers twice, that is,

- read in all the numbers and calculate the average.
- read in all the numbers again, this time checking each as it is read against a previously calculated average.

If input is from the keyboard, then the user has to enter each number twice and accurately, with no mistakes. This is not a viable solution. Because, for 25 numbers entered, the user has to remember all the numbers. But what if there are 50 or 100 numbers? Then, it is not so easy. To solve this problem, an array is required. It is a collection of numbered elements.

An array is a fundamental data structure that enables the storing and manipulation of potentially huge quantities of data. An array stores an *ordered sequence* of *homogeneous values*. Homogeneous means that all the values are of the same data type. The order of the values is also preserved, i.e., the integer array { 1, 2, 3, 4 } is different from { 1, 4, 3, 2 }.

An array can be defined as a data structure consisting of an ordered set of data values of the homogeneous (same) type. An array is a collection of individual data elements that are:

- Ordered — one can count off the elements 0, 1, 2, 3...
- Fixed in size
- Homogeneous — all elements have to be of the same type, e.g., int, float, char, etc.

In C, each array has two fundamental properties: the data type and the size. Individual array elements are identified by an integer index. In C, the index begins at zero and is always written inside square brackets.

> **Note**
> - A scalar variable is a single variable whose stored value is an atomic data type.
> - An array is a collection of individual data elements that are ordered, fixed in size, and homogeneous.
> - An array is considered to be a derived data type.
> - Array enables the storing and manipulation of potentially huge quantities of data.

### 11.2 One-Dimensional Array

There are several forms of an array used in C: one-dimensional or single-dimensional and multidimensional array. In this section, one-dimensional arrays will be discussed.

Since the array is one dimensional, there will be a single subscript or index whose value refers to the individual array element which ranges from 0 to (*n*-1), where *n* is the total number of elements in the array.

### 11.2.1 Declaration of a One-dimensional Array

To use an array variable in a program, it must be declared. When defining an array in a program, three things need to be specified.

- The type of data it can hold, i.e., int, char, double, float, etc.
- The number of values it can hold, i.e., the maximum number of elements it can hold
- A name
