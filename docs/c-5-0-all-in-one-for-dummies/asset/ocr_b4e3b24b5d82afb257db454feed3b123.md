![](bbox=[0.14, 0.17, 0.24, 0.29])

Most of the values show two decimal places for the cents in the amount. Because trailing zeros aren't displayed in all versions of C#, some values may show only a single digit — or even no digit — after the decimal point. Thus, $12.70 may be displayed as 12.7. If so, you can fix the problem by using the special formatting characters described in Chapter 3 of this mini-book. (C# 2.0 and later appear to show trailing zeros by default.)

The CalculateInterestTable program begins by reading the principal and interest values from the user and checking to make sure that they're valid. CalculateInterestTable then reads the number of years over which to iterate and stores this value in the variable duration.

Before entering the while loop, the program declares a variable year, which it initializes to 1. This will be the "current year" — that is, the number changes "each year" as the program loops. If the year number contained in year is less than the total duration contained in duration, the principal for "this year" is recalculated by calculating the interest based on the "previous year." The calculated principal is output along with the current-year offset.

![](bbox=[0.14, 0.5, 0.24, 0.62])

The statement decimal.Round() rounds the calculated value to the nearest fraction of a cent.

The key to the program lies in the last line within the block. The statement year = year + 1; increments year by 1. If year begins with the value 3, its value will be 4 after this expression. This incrementing moves the calculations along from one year to the next.

After the year has been incremented, control returns to the top of the loop, where the value year is compared to the requested duration. In the sample run, if the current year is less than 10, the calculation continues. After being incremented ten times, the value of year becomes 11, which is greater than 10, and program control passes to the first statement after the while loop — the program stops looping.

![](bbox=[0.14, 0.78, 0.24, 0.9])

Most looping commands follow this basic principle of incrementing a counter until it exceeds a previously defined value.

The counting variable year in CalculateInterestTable must be declared and initialized before the while loop in which it is used. In addition, the year variable must be incremented, usually as the last statement within the loop. As this example demonstrates, you have to look ahead to see which variables you need. This pattern is easier to use after you've written a few thousand while loops, like I have.

![](bbox=[0.14, 0.9, 0.24, 1.0])

When writing while loops, don't forget to increment the counting variable, as I did in this example:

```
int nYear = 1;
while (nYear < 10)
{
    // ... whatever ...
}
```