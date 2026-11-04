example, the following code gives you the same result as the previous code but without the pre-increment operator:

```
int x, y = 10;
y = y + 1;
x = 10 + y;
```

# Logical Operators

The logical operators perform calculations on boolean (true or false) values. They let you combine logical statements to form new ones.

Lesson 18 explains how to use these values to perform tests that let a program take action only under certain circumstances. For example, a program might pay an employee overtime if the employee is hourly and worked more than 40 hours in the last week.

Table 11-5 summarizes the boolean operators.

TABLE 11-5

| OPERATOR | MEANING |
|---|---|
| & | AND |
| | | OR |
| ^ | XOR |
| ! | NOT |
| && | Conditional AND |
| || | Conditional OR |

The & operator returns true if and only if both of its operands are true. For example, you must buy lunch if it's lunchtime and you forgot to bring a lunch today:

```
mustBuyLunch = isLunchTime & forgotToBringLunch;
```

The | operator returns true if either of its operands is true. For example, you can afford lunch if either you brought enough money or you have a credit card (or both):

```
canAffordLunch = haveEnoughMoney | haveCreditCard;
```