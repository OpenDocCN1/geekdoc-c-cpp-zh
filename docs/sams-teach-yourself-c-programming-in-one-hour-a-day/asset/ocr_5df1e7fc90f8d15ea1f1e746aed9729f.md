# LESSON 7: Fundamentals of Reading and Writing Information

conversion specifier for each variable. The conversion specifiers are paired with variables in left-to-right order. If you write

```
printf("Rate = %f, amount = %d", rate, amount);
```

the variable rate is paired with the %f specifier, and the variable amount is paired with the %d specifier. The positions of the conversion specifiers in the format string determine the position of the output. If there are more variables to printf() than there are conversion specifiers, the unmatched variables aren't printed. If there are more specifiers than variables, the unmatched specifiers print "garbage"

You aren't limited to printing the value of variables with printf(). The arguments can be any valid C expression. For example, to print the sum of x and y, you could write

```
total = x + y;
printf("%d", total);
```

You could also write

```
printf("%d", x + y);
```

Listing 7.2 demonstrates the use of printf(). Lesson 14 gives more details on printf().

# Input

# LISTING 7.2 nums.c: Using printf() to Display Numerical Values

```
1: /* Demonstration using printf() to display numerical values. */
2:
3: #include <stdio.h, c
4:
5: int a = 2, b = 10, c = 50;
6: float f = 1.05, g = 25.5, h = -0.1;
7:
8: int main(void )
9 {
10: printf("\nDecimal values without tags: %d %d %d", a, b, c);
11: printf("\nNumerical values with tags: %t\d %t\d %t\d", a, b, c);
12:
13: printf("\nFloats on 1 line: \%f\%f\%f", f, g, h);
14: printf("\nFloats on 3 lines: \n\%f\n\%f\n\%f", f, g, h);
15:
16: printf("\nThe rate is %f%%", f);
17: printf("\nnThe rate to 2 decimal places is %.2f%%", f);
18: printf("\nnThe rate to 1 decimal place is %.1f%%", f);
19:
20: printf("\nnThe result of %f/%f = %f\n", f, g / f);
21:
22: return 0;
23: }
```