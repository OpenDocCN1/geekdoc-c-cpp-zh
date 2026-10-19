```
if ( i <= count - 1 ) {
    a[ count - 1 ] = count - 1;
}
if ( i == count - 2 ) {
    a[ count -2 ] = count - 2;
}
```

Here are the results of unrolling the loop the second time:

| Language | Straight Time | Double Unrolled Time | Time Savings |
|---|---|---|---|
| C++ | 1.75 | 1.01 | 42% |
| Java | 1.01 | 0.581 | 43% |
| PHP | 5.33 | 3.70 | 31% |
| Python | 2.51 | 2.79 | -12% |
| Note: Benchmarked for the case in which count equals 100. |

The results indicate that further loop unrolling can result in further time savings, but not necessarily so, as the Java measurement shows. The main concern is how Byzantine your code becomes. When you look at the previous code, you might not think it looks incredibly complicated, but when you realize that it started life a couple of pages ago as a five-line loop, you can appreciate the tradeoff between performance and readability.

# Minimizing the Work Inside Loops

One key to writing effective loops is to minimize the work done inside a loop. If you can evaluate a statement or part of a statement outside a loop so that only the result is used inside the loop, do so. It’s good programming practice, and in some cases it improves readability.

Suppose you have a complicated pointer expression inside a hot loop that looks like this:

```
C++ Example of a Complicated Pointer Expression Inside a Loop
for ( i = 0; i < rateCount; i++ ) {
    netRate[ i ] = baseRate[ i ] * rates->discounts->factors->net;
}
```

In this case, assigning the complicated pointer expression to a well-named variable improves readability and often improves performance.

```
C++ Example of Simplifying a Complicated Pointer Expression
quantityDiscount = rates->discounts->factors->net;
for ( i = 0; i < rateCount; i++ ) {
    netRate[ i ] = baseRate[ i ] * quantityDiscount;
}
```