Casting at least one of the two integers to float type would yield the correct result:

```
float average = 25f/10;
```

The result of 25f/10 would be float type, which is the larger of the two types, yielding the correct result. 2.5.

So, when you divide an integer by another integer, at least one of the two must be cast to a real type to get the result with the fractional part, if any.

Step 1-9: Add the following statement to the click event handler of Compute Total button, run the program and observe the value of average:

```
float average = 25 / 10;    //yields 2
```

Change the expression to 25f/10f, and see the difference in value (2.5).

Change the expression to 25f/10, which yields 2.5.

Delete the statement.

# Multiplication with large integers

Multiplication with large integers can result in unexpected consequences:

```
int price = 3000;
int quantity = 1000000;
long cost = price * quantity;
```

The product 3000 * 1000000 yields 3 billion. However, because the product of the two int types (price * quantity) is represented as int, whose limit is approximately 2.15 billion, the result is outside the limit and yields incorrect results.

Step 1-10: Add the following statements, run the program and note the value of cost.

```
int price = 3000;
int quantity = 1000000;
long cost = price * quantity;
```

Delete the statements.

The value of cost is incorrect because the result is int type, whose limit is about 2.15 billion, which is too small for the result of 3000,000,000 (3 billion).

# An oddity in C#

When an operation involves short or sbyte types, these types are automatically converted to int type before performing the operation. So, the result will be int type.

```
short exam1 = 80;
sbyte exam2 = 90;
short total = exam1 + exam2; // Error! The result is int type (odd!), whereas total is short type
```

You may cast the result to short, as in

```
short total = (short) (exam1 + exam2);
```