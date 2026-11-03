
```c
i) printf( "The product is %d\n", x * y );
j) scanf( "%d, %d, %d", &x, &y, &z );
```

### 2.8 Fill in the blanks in each of the following:

- a) All ______ must be declared before being used in a program.
- b) C is ______. Uppercase and lowercase letters are different in C.
- c) Single-line comments begin with _______.
- d) __________ are words reserved by C and cannot be used.
- e) __________ and __________ are ignored by the compiler.

### 2.9 Write a single C statement or line that accomplishes each of the following:

- a) Print the message "Have a nice day."
- b) Assign the sum of variables b and c to variable a.
- c) Check if the value of variable a is greater than variable b. If it is, store the difference of the two in variable c.
- d) Input three integer values from the keyboard and place them in int variables p, q, and r.

### 2.10 State which of the following are true and which are false. If false, explain your answer.

- a) C regards the functions main and Main as identical.
- b) The associativity of the operators specifies whether they evaluate from left to right or from right to left.
- c) The statement if(a = b) checks whether the variables a and b are equal.
- d) Conditions in if statements are formed by using assignment operators.
- e) The following are all valid variable names: _3g, my_val, h22, 123greetings, July98.

### 2.11 Fill in the blanks in each of the following:

- a) The __________ statement allows a program to perform different actions based on a condition.
- b) If the result of an integer division, where both the numerator and the denominator are integers, is a fraction, the fractional part is __________.
- c) The directive __________ tells the preprocessor to include the contents of the input/output stream header files.

### 2.12 What, if anything, prints when each of the following statements is performed? If nothing prints, then answer "Nothing." Assume a = 15, b = 4 and c = 7.

- a) printf("%d", a % b);
- b) printf("%d", a * c + b);
- c) printf("b= ");
- d) printf("a = 15");
- e) printf("%d ", a = a + b, a + b);
- f) c = a + b;
- g) scanf("%d%d", &a, &b);
- h) // printf("Now a and b changes to %d and %d", a, b);
- i) printf("\n");

### 2.13 Which, if any, of the following C statements contain variables whose values are replaced?

- a) printf("Enter two Numbers: ");
- b) scanf("%d%d", &a, &b);
- c) sum = a + b;
- d) printf("\nThe result is: %d", sum);

### 2.14 Given the equation y = ax³ − bx² − 6, which of the following, if any, are correct C statements for this equation?

- a) y = a * x * x * x - b * x * x - 6;
- b) y = a * x * x * x - b * x * x - 6;
- c) a * (x * x * x) - b * x * x * ( - 6 );
- d) a * (x * x * x ) - b * (x * x) - 6;
- e) a * x * x * x - (b * x * x - 6 );
- f) (a * x * 3 - b * x * 2 ) - 6;

### 2.15 State the order of evaluation of the operators in each of the following C statements and show the value of x after each statement is performed.

```c
a) x = 8 + 15 * ( 6 - 2 ) - 1;
b) x = 5 % 5 + 5 * 5 - 5;
c) x = ( 5 * 7 * ( 5 + ( 7 * 5 / ( 7 ) ) ) );
```

### 2.16 (Arithmetic) Write a program that asks the user to enter two numbers, obtains them from the user and prints their sum, product, difference, quotient and remainder.

### 2.17 (Final Velocity) Write a program that asks the user to enter the initial velocity and acceleration of an object, and the time that has elapsed, places them in the variables u, a, and t, and prints the final velocity, v, and distance traversed, s, using the following equations.

```c
a) v = u + at
b) s = ut + 1/2 at^2
```

### 2.18 (Comparing Values) Write a program that asks the user to enter the highest rainfall ever in one season for a country, and the rainfall in the current year for that country, obtains the values from the user, checks if the current rainfall exceed the highest rainfall and prints an appropriate message on the screen. If the current rainfall is higher, it assigns that value as the highest rainfall ever. Use only the single-selection form of the if statement you learned in this chapter.

### 2.19 (Arithmetic, Largest Value and Smallest Value) Write a program that inputs three different integers from the keyboard, then prints the sum, the average, the product, the smallest and the largest of these numbers. Use only the single-selection form of the if statement you learned in this chapter. The screen dialogue should appear as follows:

```c
Enter three different integers: 13 27 14
Sum is 54
Average is 18
Product is 4914
Smallest is 13
Largest is 27
```

### 2.20 (Converting from seconds to hours, minutes and seconds) Write a program that asks the user to enter the total time elapsed, in seconds, since an event and converts the time to hours, minutes and seconds. The time should be displayed as hours:minutes:seconds. [Hint: Use the remainder operator]

### 2.21 (Shapes with Asterisks) Write a program that prints the following shapes with asterisks.

### 2.22 What does the following code print?

```c
printf( "\n\n%s\n\n%s\n%s\n%s\n" );
```

### 2.23 (Largest and Smallest Integers) Write a program that reads in three integers and then determines and prints the largest and the smallest integers in the group. Use only the programming techniques you have learned in this chapter.

### 2.24 (Odd or Even) Write a program that reads an integer and determines and prints whether it's odd or even. [Hint: Use the remainder operator. An even number is a multiple of two. Any multiple of two leaves a remainder of zero when divided by 2.]

### 2.25 Print your initials in block letters down the page. Construct each block letter out of the letter it represents, as shown on the top of the next page:

```c
PPPPPPPP
  P   P
  P   P
  P   P
  P   P

JJ
J
J
JJJJJJ

DDDDDDDD
D      D
D      D
D      D
DDDDD
```

### 2.26 (Multiples) Write a program that reads in two integers and determines and prints whether the first is a multiple of the second. [Hint: Use the remainder operator.]

### 2.27 (Checkerboard Pattern of Asterisks) Display the following checkerboard pattern with eight printf statements and then display the same pattern with as few printf statements as possible.

```c
* * * * * * * *
* * * * * * * *
* * * * * * * *
* * * * * * * *
* * * * * * * *
* * * * * * * *
* * * * * * * *
* * * * * * * *
```

### 2.28 Distinguish between the terms fatal error and nonfatal error. Why might you prefer to experience a fatal error rather than a nonfatal error?

### 2.29 (Integer Value of a Character) Here's a peek ahead. In this chapter you learned about integers and the type int. C can also represent uppercase letters, lowercase letters, and a considerable variety of special symbols. C uses small integers internally to represent each different character. The set of characters a computer uses together with the corresponding integer representations for those characters is called that computer's character set. You can print the integer equivalent of uppercase A, for example, by executing the statement

```c
printf( "%d", 'A' );
```

Write a program that prints the integer equivalents of some uppercase letters, lowercase letters, digits and special symbols. As a minimum, determine the integer equivalents of the following: A B C a b c 0 1 2 5 ^ + / and the blank character.

### 2.30 (Separating Digits in an Integer) Write a program that inputs one five-digit number, separates the number into its individual digits and prints the digits separated from one another by three spaces each. [Hint: Use combinations of integer division and the remainder operation.] For example, if the user types in 42139, the program should print

```c
4  2  1  3  9
```

### 2.31 (Table of Squares and Cubes) Using only the techniques you learned in this chapter, write a program that calculates the squares and cubes of the numbers from 0 to 10 and uses tabs to print the following table of values:

| number | square | cube |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |
| 10 | 100 | 1000 |

## Making a Difference

### 2.32 (Body Mass Index Calculator) We introduced the body mass index (BMI) calculator in Exercise 1.12. The formulas for calculating BMI are

$BMI = \frac{weightInPounds \times 703}{heightInInches \times heightInInches}$

or

$BMI = \frac{weightInKilograms}{heightInMeters \times heightInMeters}$

Create a BMI calculator application that reads the user's weight in pounds and height in inches (or, if you prefer, the user's weight in kilograms and height in meters), then calculates and displays the user's body mass index. Also, the application should display the following information from the Department of Health and Human Services/National Institutes of Health so the user can evaluate his/her BMI:

| BMI VALUES |
|---|
| Underweight: less than 18.5 |
| Normal: between 18.5 and 24.9 |
| Overweight: between 25 and 29.9 |
| Obese: 30 or greater |

> [Note: In this chapter, you learned to use the int type to represent whole numbers. The BMI calculations when done with int values will both produce whole-number results. In Chapter 4 you'll learn to use the double type to represent numbers with decimal points. When the BMI calculations are performed with doubles, they'll both produce numbers with decimal points—these are called "floating-point" numbers.]
