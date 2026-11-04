The logical comparisons are defined for all numeric types, including float, double, decimal, and char. All the following statements are legal:

```
bool b;
b = 3 > 2;    // true
b = 3.0 > 2.0;  // true
b = 'a' > 'b';  // false -- Alphabetically, later = greater.
b = 'A' < 'a';  // true -- Upper A is less than lower a.
b = 'A' < 'B';  // true -- All upper are less than all lower.
b = 10M > 12M;  // false
```

The comparison operators always produce results of type bool. The comparison operators other than == are not valid for variables of type string. (Not to worry: C# offers other ways to compare strings.)

# Comparing floating-point numbers:
Is your float bigger than mine?

Comparing two floating-point values can get dicey, and you need to be careful with these comparisons. Consider the following comparison:

```
float f1;
float f2;
f1 = 10;
f2 = f1 / 3;
bool b1 = (3 * f2) == f1;  // b1 is true if (3 * f2) equals f1.
f1 = 9;
f2 = f1 / 3;
bool b2 = (3 * f2) == f1;
```

Notice that both the fifth and eighth lines in the preceding example contain first an assignment operator (=) and then a logical comparison (==). These are different animals, so don't type = when you mean ==. C# does the logical comparison and then assigns the result to the variable on the left.

The only difference between the calculations of b1 and b2 is the original value of f1. So, what are the values of b1 and b2? The value of b2 is clearly true: 9 / 3 is 3; 3 * 3 is 9; and 9 equals 9. Voilà!

The value of b1 isn't obvious: 10 / 3 is 3.333... and 3.333... * 3 is 9.999.... Is 9.999... equal to 10? That depends on how clever your processor and compiler are. On a Pentium or later processor, C# isn't smart enough to realize that b1 should be true if the calculations are moved away from the comparison.

You can use the system absolute value method to compare f1 and f2:

```
Math.Abs(f1 - 3.0 * f2) < .00001;  // Use whatever level of accuracy.
```

This calculation returns true for both cases. You can use the constant Double.Epsilon instead of .00001 to produce the maximum level of accuracy.

![](bbox=[0.1, 0.85, 0.22, 0.95])