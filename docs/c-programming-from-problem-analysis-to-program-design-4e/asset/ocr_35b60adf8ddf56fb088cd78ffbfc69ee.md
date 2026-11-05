The current value of count, 1, is used in the multiplication because the ++ comes after the identifier name. After using count in the arithmetic, it is incremented by 1, becoming 2. Because the decrement operator comes before the variable firstNum, 1 is subtracted from firstNum before the multiplication is performed. Thus, 1 is multiplied by 9, and the result is added to 100.

# Compound Operations

You commonly write arithmetic operations that modify a variable by using its original value as part of the calculation. Consider the following:

```
answer = 100;
answer = answer + 5;
```

The variable answer holds the end result, but it is also used in the computation. Compound operators provide a shortcut way to write assignment statements using the result as part of the computation. The last line in the preceding code segment (answer = answer + 5;) could be replaced with the following:

```
answer += 5;
```

Both statements take the original value of answer, add 5 to it, and store the result back in answer.

> NOTE
> In expressions involving multiple operations, the compound operation is always performed last. For example: answer += 45 * 28 + 37 / 16; is equivalent to answer = answer + (45 * 28 + 37 / 16); The original value of answer is not added until the expression on the right of the equal sign is complete.

Accumulation is another type of operation commonly found in applications. You will often find it necessary to keep a running total or accumulate values that a single variable holds. For example, to determine the average of a set of values, the values are normally added to an accumulator and divided by the number of entries. Consider the following:

```
int total = 0;
int newValue;
// : Note statements that enable the user
// to enter values for newValue are inserted here

total = total + newValue;
```

If multiple values are input by the user, each newValue could be added to total. This is an example of accumulating values. Accumulators are often used with monetary amounts. For example, to accumulate the total amount of money received or the total for an order that includes a number of items, a variable such as