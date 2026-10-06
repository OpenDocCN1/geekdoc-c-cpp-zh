
## CHAPTER 4 Making Decisions

A partial solution to this problem is to add an else clause to the statement:

```cs
if(saleAmount >= 1000)
    commissionRate = 0.08;
else if(saleAmount >= 500)
    commissionRate = 0.06;
else if(saleAmount <= 499)
    commissionRate = 0.05;
```

> Don't Do It
> The logic reaches this point, the expression must be true, so it is waste of time to test this condition.

168

The last two logical tests in this code are sometimes called else-if statements because each subsequent if are placed on the same line. When the else-if format is used to test multiple cases, programmers frequently forgo the traditional indentation and align each-if with the others.

With this code, saleAmount is $5000, the expression (saleAmount >= 1000) is true and commissionRate becomes 0.08; then the entire structure ends. When saleAmount is not greater than equal to $1000 (for example, $800), the first if is false and the else statement executes and correctly sets commissionRate to 0.06.

This version of the code works, which is somewhat inefficient because it executes as follows:

- When saleAmount is at least $1000, the first Boolean test is true, so commissionRate is assigned .08 and the reach ends.
- When saleAmount is less than $1000 but at least $500, the first Boolean test is false, but the second one is true, so commissionRate is assigned .06 and if else structure ends.
- The only saleAmount that reaches the third Boolean test is less than $500, so the only Boolean test, if(saleAmount <= 499), is always true. When an expression is true, is there no need to evaluate it. In other words, if saleAmount is not at least $1000 and is also not least $500, it must default by least to reach or $499.

The improved code is as follows:

```cs
if(saleAmount >= 1000)
    commissionRate = 0.08;
else if(saleAmount >= 500)
    commissionRate = 0.06;
else
    commissionRate = 0.05;
```

In other words, this example uses three commission rates, two boundaries should be checked. If there were three rates, there would be three boundaries to check, and so on.

With a nested if-else, processing is most efficient when the first question asked is the one that is most likely to be true. In other words, if you know that a large number of saleAmount values are greater than $1000, compare saleAmount to that value. That way, the logic bypasses the rest of the decisions. If, however, you know that most saleAmounts are small, processing is most efficient when the first decision is if(saleAmount < 500).

## Using && and || Appropriately

Beginning programmers often use the && operator when they mean to use ||, and often use || when they should use &&. Part of the problem lies in the way we use the English language. For example, your boss might request, "Display an error message when an employee's hourly pay is less than $5.65 and when an employee's hourly pay is greater than $60. Because your boss used the and in the request, you might be tempted to write a program statement like the following:

```cs
if(payRate < 5.65 && payRate > 60)
    WriteLine("Error in pay rate");
```

As a single variable, no payRate can ever be less than 5.65 and greater than 60 at the same time, so the output statement can execute, no matter what value payRate has. In this case, you must write the following statement to display the error message under the correct circumstances:

```cs
if(payRate < 5.65 || payRate > 60)
    WriteLine("Error in pay rate");
```

Similarly, your boss might request, "Output the names of employees in departments 1 and 2." Because your boss used the and in the request, you might be tempted to write the following:

```cs
if(department == 1 && department == 2)
    WriteLine("Name is: {0}", name);
```

However, the department can never contain both 1 and 2 at the same time, so no employee name will ever be output, no matter what the employee is in.

The correct statement is:

```cs
if(department == 1 || department == 2)
    WriteLine("Name is: {0}", name);
```

## Using the Operator Correctly

Whenever you use negatives, it is easy to make logical mistakes. For example, suppose your boss says, "Make sure that if the sales is not A or B, the customer gets a 10 percent discount." You might be tempted to code the following:

```cs
if(salesCode != 'A' && salesCode != 'B')
    discount = 0.10;
```

However, this logic will result in every customer receiving the 10 percent discount because every salesCode is either not A or B. For example, if salesCode is A, then it is not B. The expression salesCode != 'A' && salesCode != 'B' is always true. The correct statement is one of the following:

```cs
if(salesCode != 'A' && salesCode != 'B')
    discount = 0.10;
```

```cs
if(salesCode == 'A' || salesCode == 'B')
discount = 0.10;
```

In the first example, if salesCode is not 'A' and it is not 'B', then the discount is applied correctly. In the second example, if salesCode is 'A' or 'B', the inner Boolean expression is true, and the NOT operator (!) changes the evaluation to false, not applying the discount for A or B sales. You could also avoid the confusing negative situation by asking questions in a positive way, as in the following:

```cs
if(salesCode == 'A' || salesCode == 'B')
discount = 0;
else
discount = 0.10;
```

Watch the video Avoiding Common Decision Errors.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_196_0.png)

## TWO TRUTHS & A LIE

### Avoiding Common Decision Errors

- 1. If you want to display OK when userEntry is 12 and highestScore is 20, the following is a usable C# statement:
  if (userEntry == 12 && highestScore == 20)
  WriteLine("OK");
- 2. If you want to display OK when userEntry is 20 or highestScore is 70, the following is a usable C# statement:
  if (userEntry == 20 || highestScore >= 70)
  WriteLine("OK");
- 3. If you want to display OK when userEntry is anything than 99 or 100, the following is a usable C# statement:
  if (userEntry != 99 && userEntry != 100)
  WriteLine("OK");

The expression userEntry != 12 && userEntry != 13 is always true. The correct statement is one of the following: (Wait, the OCR text seems garbled here, based on context):

When an expression is true, there is no need to evaluate it. In other words, if saleAmount is not at least $1000 and is also not least $500, it must default by least to reach or $499.
