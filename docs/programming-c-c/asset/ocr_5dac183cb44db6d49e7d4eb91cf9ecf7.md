In case of nested loop, continue will continue next iteration of nearest loop.

Do not confuse that continue transfer program control to loop condition. It transfers program control to next part of the loop.

Use of continue statement without condition is worthless. Hence, it is often used with if statements.

# How continue statement Works?

```
while (testExpression) {
    // codes
    if (testExpression) {
        continue;
    }
}
```

```
do {
    // codes
    if (testExpression) {
        continue;
    }
} while (testExpression);
```

```
for (init; testExpression; update) {
    // codes
    if (testExpression) {
        continue;
    }
}
```

We will see example programs of continue statement along with the loops and switches.

# Difference between break and continue

| break | continue |
| --- | --- |
| A break can appear in both switch and loop (for, while, do) statements. | A continue can appear only in loop (for, while, do) statements. |
| A break causes the switch or loop statements to terminate the moment it is executed. Loop or switch ends abruptly when break is encountered. | A continue doesn't terminate the loop, it causes the loop to go to the next iteration. All iterations of the loop are encountered. The continue statement is used to skip statements in the loop that appear after the continue. |