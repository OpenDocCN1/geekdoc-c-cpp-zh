Without the parentheses, however, b would be divided by 4 and the result added to a. Table 2-3 shows more expressions and their values.

# Table 2-3 More expressions and their values

| Expression | Value |
| --- | --- |
| (5 + 2) * 4 | 28 |
| 10 / (5 - 3) | 5 |
| 8 + 12 * (6 - 2) | 56 |
| (6 - 3) * (2 + 7) / 3 | 9 |

> NOTE: Parentheses can be used to enhance the clarity of a math expression, when they are unnecessary to get the correct result. For example, look at the following-statement:
Set fahrenheit = celsius * 1.8 + 32
Even when it is unnecessary to get the correct result, you can insert parentheses to clearly show that celsius * 1.8 happens in the math expression:
Set fahrenheit = (celsius * 1.8) + 32

![](bbox=[0.158, 0.298, 0.203, 0.345])

![](bbox=[0.773, 0.473, 0.843, 0.523])

# In the Spotlight:

# Calculating Average

Determining the average of a group of values is a simple calculation: You add all of the values and divide the sum by the number of values. Although this is a straightforward-calculation, it is easy to make a mistake when writing a program that calculates an average. For example, let's assume the variables a, b, and c hold a value and we want to calculate the average of those values. If we are careless, we might write a statement such as the following to perform the calculation:

Set average = a + b + c / 3

Can you see the error in this statement? When it executes, the division will take place. The first value c is divided by 3, and the result will be added to a + b. That is not the correct way to calculate an average. To correct this error we need to put parentheses around a + b + c, as shown here:

Set average = (a + b) / 3

Let's try the process of writing a program that calculates an average. Suppose you have taken three tests in your computer science class, and you want to write a program that will display the average of the test scores. Here is the algorithm:

+   1. Get the first test score.
2. Get the second test score.
3. Get the third test score.
4. Calculate the average by adding the three test scores and dividing the sum by 3.
5. Display the average.