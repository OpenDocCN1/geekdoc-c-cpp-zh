![](bbox=[0.32, 0.18, 0.78, 0.28])

# Figure 3.3 sum = sum + 10; causes a new value to be stored in sum

Assignment expressions such as sum = sum + 10, which use the same variable on both sides of the assignment operator, can be written by using the following shortcut assignment operators:

+= -= *= /= %=

For example, the expression sum = sum + 10 can be written as sum += 10. Similarly, the expression price *= rate is equivalent to the expression price = price * rate. In using shortcut assignment operators, note that the variable to the left of the assignment operator is applied to the complete expression on the right. For example, the expression price *= rate + 1 is equivalent to the expression price = price * (rate + 1), not price = price * rate + 1.

# Accumulating

Assignment expressions, such as sum += 10 or its equivalent, sum = sum + 10, are common in programming. These expressions are required in accumulating subtotals when data is entered one number at a time. For example, if you want to add the numbers 96, 70, 85, and 60 in calculator fashion, the following statements could be used:

| Statement | Value in sum |
|---|---|
| sum = 0; | 0 |
| sum = sum + 96; | 96 |
| sum = sum + 70; | 166 |
| sum = sum + 85; | 251 |
| sum = sum + 60; | 311 |

The first statement initializes sum to 0, which removes any number stored in sum that would invalidate the final total (a "garbage value"). As each number is added, the value stored in sum is increased accordingly. After completion of the last statement, sum contains the total of all the added numbers. Program 3.3 shows the effect of these statements by displaying sum's contents after each addition.