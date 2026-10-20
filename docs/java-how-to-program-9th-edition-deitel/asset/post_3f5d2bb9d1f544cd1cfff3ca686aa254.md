
## 4.27 (Dangling-else Problem)

Determine the output for each of the given sets of code when x is 9 and y is 11 and when x is 11 and y is 9. The compiler ignores the indentation in a Java program. Also, the Java compiler always associates an else with the immediately preceding if unless told to do otherwise by the placement of braces ({}). On first glance, you may not be sure which if a particular else matches—this situation is referred to as the “dangling-else problem.” We’ve eliminated the indentation from the following code to make the problem more challenging. [Hint: Apply the indentation conventions you’ve learned.]

- a)
```
if ( x < 10 )
if ( y > 10 )
System.out.println( "******" );
else
System.out.println( "####" );
System.out.println( "$$$$" );
```

- b)
```
if ( x < 10 )
{
if ( y > 10 )
System.out.println( "******" );
}
else
{
System.out.println( "####" );
System.out.println( "$$$$" );
}
```

## 4.28 (Another Dangling-else Problem)

Modify the given code to produce the output shown in each part of the problem. Use proper indentation techniques. Make no changes other than inserting braces and changing the indentation of the code. The compiler ignores indentation in a Java program. We’ve eliminated the indentation from the given code to make the problem more challenging. [Note: It’s possible that no modification is necessary for some of the parts.]

```
if ( y == 8 )
if ( x == 5 )
System.out.println( "@@@@" );
else
System.out.println( "####" );
System.out.println( "$$$$" );
System.out.println( "&&&&" );
```

- a) Assuming that x = 5 and y = 8, the following output is produced:

```
@@@@
$$$$
&&&&
```

- b) Assuming that x = 5 and y = 8, the following output is produced:

```
@@@@
```

- c) Assuming that x = 5 and y = 8, the following output is produced:

```
@@@@
```

- d) Assuming that x = 5 and y = 7, the following output is produced. [Note: The last three output statements after the else are all part of a block.]

```
####
$$$$
&&&&
```

## 4.29 (Square of Asterisks)

Write an application that prompts the user to enter the size of the side of a square, then displays a hollow square of that size made of asterisks. Your program should work for squares of all side lengths between 1 and 20.

## 4.30 (Palindromes)

A palindrome is a sequence of characters that reads the same backward as forward. For example, each of the following five-digit integers is a palindrome: 12321, 55555, 45554 and 11611. Write an application that reads in a five-digit integer and determines whether it’s a palindrome. If the number is not five digits long, display an error message and allow the user to enter a new value.

## 4.31 (Printing the Decimal Equivalent of a Binary Number)

Write an application that inputs an integer containing only 0s and 1s (i.e., a binary integer) and prints its decimal equivalent. [Hint: Use the remainder and division operators to pick off the binary number’s digits one at a time, from right to left. In the decimal number system, the rightmost digit has a positional value of 1 and the next digit to the left a positional value of 10, then 100, then 1000, and so on. The decimal number 234 can be interpreted as 4 * 1 + 3 * 10 + 2 * 100. In the binary number system, the rightmost digit has a positional value of 1, the next digit to the left a positional value of 2, then 4, then 8, and so on. The decimal equivalent of binary 1101 is 1 * 1 + 0 * 2 + 1 * 4 + 1 * 8, or 1 + 0 + 4 + 8 or, 13.]

## 4.32 (Checkerboard Pattern of Asterisks)

Write an application that uses only the output statements

```
System.out.print( "* " );
System.out.print( " " );
System.out.println();
```

to display the checkerboard pattern that follows. A System.out.println method call with no arguments causes the program to output a single newline character. [Hint: Repetition statements are required.]

![](img/009e962758dcc71dbc43a493362e6dc0_186_0.png)

## 4.33 (Multiples of 2 with an Infinite Loop)

Write an application that keeps displaying in the command window the multiples of the integer 2—namely, 2, 4, 8, 16, 32, 64, and so on. Your loop should not terminate (i.e., it should create an infinite loop). What happens when you run this program?

## 4.34 (What’s Wrong with This Code?)

What is wrong with the following statement? Provide the correct statement to add one to the sum of x and y.

```
System.out.println( ++(x + y) );
```

## 4.35 (Sides of a Triangle)

Write an application that reads three nonzero values entered by the user and determines and prints whether they could represent the sides of a triangle.

## 4.36 (Sides of a Right Triangle)

Write an application that reads three nonzero integers and determines and prints whether they could represent the sides of a right triangle.

## 4.37 (Factorial)

The factorial of a nonnegative integer n is written as n! (pronounced “n factorial”) and is defined as follows:

n! = n · (n − 1) · (n − 2) · … · 1  (for values of n greater than or equal to 1)

and

n! = 1  (for n = 0)

For example, 5! = 5 · 4 · 3 · 2 · 1, which is 120.

- a) Write an application that reads a nonnegative integer and computes and prints its factorial.

- b) Write an application that estimates the value of the mathematical constant e by using the following formula. Allow the user to enter the number of terms to calculate.

  e = 1 + 1/1! + 1/2! + 1/3! + …

- c) Write an application that computes the value of e^x by using the following formula. Allow the user to enter the number of terms to calculate.

  e^x = 1 + x/1! + x²/2! + x³/3! + …

## Making a Difference

### 4.38 (Enforcing Privacy with Cryptography)

The explosive growth of Internet communications and data storage on Internet-connected computers has greatly increased privacy concerns. The field of cryptography is concerned with coding data to make it difficult (and hopefully—with the most advanced schemes—impossible) for unauthorized users to read. In this exercise you’ll investigate a simple scheme for encrypting and decrypting data. A company that wants to send data over the Internet has asked you to write a program that will encrypt it so that it may be transmitted more securely. All the data is transmitted as four-digit integers. Your application should read a four-digit integer entered by the user and encrypt it as follows: Replace each digit with the result of adding 7 to the digit and getting the remainder after dividing the new value by 10. Then swap the first digit with the third, and swap the second digit with the fourth. Then print the encrypted integer. Write a separate application that inputs an encrypted four-digit integer and decrypts it (by reversing the encryption scheme) to form the original number. [Optional reading project: Research “public key cryptography” in general and the PGP (Pretty Good Privacy) specific public key scheme. You may also want to investigate the RSA scheme, which is widely used in industrial-strength applications.]

### 4.39 (World Population Growth)

World population has grown considerably over the centuries. Continued growth could eventually challenge the limits of breathable air, drinkable water, arable cropland and other limited resources. There’s evidence that growth has been slowing in recent years and that world population could peak some time this century, then start to decline.

For this exercise, research world population growth issues online. Be sure to investigate various viewpoints. Get estimates for the current world population and its growth rate (the percentage by which it’s likely to increase this year). Write a program that calculates world population growth each year for the next 75 years, using the simplifying assumption that the current growth rate will stay constant. Print the results in a table. The first column should display the year from year 1 to year 75. The second column should display the anticipated world population at the end of that year. The third column should display the numerical increase in the world population that would occur that year. Using your results, determine the year in which the population would be double what it is today, if this year’s growth rate were to persist.
