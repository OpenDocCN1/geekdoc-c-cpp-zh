
6. Suppose that a gas company bases its charges on consumption according to the following table:

| Gas Used | Rate |
|---|---|
| First 70 cubic meters | $5.00 minimum cost |
| Next 100 cubic meters | 5¢ per cubic meter |
| Next 230 cubic meters | 2.5¢ per cubic meter |
| Over 400 cubic meters | 1.5¢ per cubic meter |

Meter readings are four-digit numbers that represent cubic meters. Write a program in which the meter reading for the previous month and the current meter reading are entered and then the amount of the bill is calculated. Note: The current reading may be less than the previous one; for example, one month’s reading might be 9897 and the next month’s reading 0103.

## Section 5.5

- 1. Write a driver program to test your summation code from Exercise 7.
- 2. Write a driver program to test your summation code from Exercise 8.
- 3. The sequence of Fibonacci numbers begins with the integers 1, 1, 2, 3, 5, 8, 13, 21, . . . where each number after the first two is the sum of the two preceding numbers. Write a program that reads a positive integer n and uses a for loop to generate and display the first n Fibonacci numbers.
- 4. Ratios of consecutive Fibonacci numbers 1/1, 1/2, 2/3, 3/5, . . . approach the golden ratio. Modify the program in Problem 3 so that it also displays the decimal values of the ratios of consecutive Fibonacci numbers.
- 5. A certain product is to sell for unitPrice dollars. Write a program that reads values for unitPrice and totalNumber and then produces a table showing the total price of from 1 through totalNumber units. The table should have a format like the following:

Number of Units    Total Price
================    ==========
1                   $1.50
2                   $3.00
3                   $4.50
4                   $6.00
5                   $7.50

- 6. Write a program to read a set of numbers and calculate and display the mean, variance, and standard deviation of the set of numbers. The mean and variance of numbers x₁, x₂, . . . , xₙ can be calculated using the formulas

mean = (1/n) Σᵢ₌₁ⁿ xᵢ    variance = (1/n) Σᵢ₌₁ⁿ xᵢ² − (1/n²) ( Σᵢ₌₁ⁿ xᵢ )²

The standard deviation is the square root of the variance.

```
geometric mean = \sqrt[n]{x_1 \cdot x_2 \cdots x_n}
= the nth root of the product of the numbers
```

```
harmonic mean = \frac{n}{\frac{1}{x_1} + \frac{1}{x_2} + \cdots + \frac{1}{x_n}}
```

Write a program that reads a list of numbers and calculates their arithmetic mean, geometric mean, and harmonic mean. These values should be displayed with appropriate labels.

```
p = \frac{1}{2} \left( \frac{y}{y + z} \right)
```

because y/(y + z) is the probability that the parent is of type AB and 1/2 is the probability that such a parent will donate gene A. Then the proportions x', y', and z' of AA, AB, and BB, respectively, in each succeeding generation are given by

```
x' = p^2 , y' = 2p(1-p) , z' = (1-p)^2
```

```
p' = \frac{1}{2} \left( \frac{y'}{y' + z'} \right)
```

Write a program to calculate and display the generation number and the proportions of AA, AB, and BB under appropriate headings for 30 generations. (Note that the proportions of AA and AB should approach 0, because gene A will gradually disappear.)

9. Write a program that uses an input loop to read data values as shown in the following table, calculates the miles per gallon in each case, and displays the values with appropriate labels:

| Miles Traveled | Gallons of Gasoline Used |
|---|---|
| 231 | 14.8 |
| 248 | 15.1 |
| 302 | 12.8 |
| 147 | 9.25 |
| 88 | 7 |
| 265 | 13.3 |

10. Write a program that uses an input loop to read several values representing miles, converts miles to kilometers (1 mile = 1.60935 kilometers), and displays all values with appropriate labels.

11. Suppose that two hallways, one 8 feet wide and the other 10 feet wide, meet at a right angle and that a ladder is to be carried around the corner from one hallway into the other. Using the similar triangles in the following diagram, we see that

L = x + (10x) / sqrt(x^2 - 64)

Write a program that initializes x to 8.1 and then increments it by 0.1 to find to the nearest 0.1 foot the length of the longest ladder that can be carried around the corner. (Note: This length is the same as the minimum value of the distance L.)

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_163_0.png)

## Functions and Libraries

| 6.1 Introductory Example: Temperature Conversion with Expressions | 150 |
| 6.2 Introductory Example: Temperature Conversion with a Function | 153 |
| 6.3 Programmer-Defined Functions | 155 |
| 6.4 An Introduction to Libraries | 168 |
| 6.5 Introduction to Numerical Methods | 177 |
| Chapter Summary | 186 |
| Test Yourself | 190 |
| Exercises | 192 |
| Programming Problems | 194 |

> Home computers are being called upon to perform many new functions, including the consumption of homework formerly eaten by the dog.
> 
> DOUG LARSON

> The function of education is to teach one to think intensively and to think critically .... Intelligence plus character—that is the goal of true education.
> 
> MARTIN LUTHER KING, JR.

> Doing research on the Web is like using a library assembled piecemeal by pack rats and vandalized nightly.
> 
> ROGER EBERT

## 150 ■ Programming in C++ for Engineering and Science

> I never met a library I didn’t like.

A MAJOR THEME OF THIS CHAPTER is writing code that is reusable. As we show first, reusability may be on a “local” level in which code segments are encapsulated in a function that is a separate part of a program but can be used anywhere else in the program. Also, because it is a separate piece of code, it can be used in other programs by copying and pasting this code into them. For reusability on a larger scale, functions (and other program components such as constant declarations) can be stored in a library from which any program can retrieve and use them, just as the programs in Examples 5.4 and 5.5 used the function sqrt() from the cmath library.

A second theme of this chapter is information hiding, also known as abstraction, which refers to separating unnecessary details about a computation from what others need to know in order to use it. Here again we will see that this separation can be done on a local scale for functions that are part of a program, and that libraries make true information hiding possible.

Also, functions make it possible to modularize programs, which facilitates solving complex problems. We divide a problem into a number of simpler problems, develop functions to solve these simpler problems, and then combine them with a main “driver” program to produce a complete program that solves the original problem. In this chapter, however, we will look only at fairly simple functions in detail and give several examples, because understanding how to construct and use functions is fundamental to writing reusable code. We will also see how libraries are constructed. It must be realized, however, that this first look at functions and libraries is only an introduction. Many more features and uses will be given in later chapters.

Many problems involve the use of formulas in their solutions. For example, in Section 4.1, we used Einstein’s formula e = m × c² to compute the energy released by a quantity of matter and found that converting this formula into a C++ expression was quite straightforward. In this chapter we begin with a temperature-conversion problem that is also easy to solve in C++, but our first version of a program to perform these conversions will undergo a series of modifications with a view to increasing reusability.

Fahrenheit and Celsius are two scales used to measure temperature. We will develop a program to convert temperatures in Celsius to the equivalent Fahrenheit temperatures.

Our program will repeatedly display on the screen a prompt for a Celsius temperature. Each time, the user will enter a numeric value (the Celsius temperature) from the keyboard that the program will read. It will then compute the Fahrenheit temperature equivalent of
