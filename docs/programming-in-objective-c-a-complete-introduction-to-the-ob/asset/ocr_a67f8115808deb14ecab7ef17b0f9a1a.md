# Chapter 6 Making Decisions

```
rem_4 = year % 4;
rem_100 = year % 100;
rem_400 = year % 400;
```

```
if ( rem_4 == 0 && rem_100 != 0 ) || rem_400 == 0 )
    NSLog ("@*It's a leap year.")
else
    NSLog ("@*Nope, it's not a leap year.");

[pool drain];
return 0;
```

# Program 6.5 Output

Enter the year to be tested:
1955
Nope, it's not a leap year.

# Program 6.5 Output (Rerun)

Enter the year to be tested:
2000
It's a leap year.

# Program 6.5 Output (Rerun)

Enter the year to be tested:
1800
Nope, it's not a leap year.

The previous examples use a year that is not a leap year because it isn't divisible by 4 (1955), a year that is a leap year because it is evenly divisible by 400 (2000), and a year that isn't a leap year because it is evenly divisible by 100 but not by 400 (1800). To complete the run of test, you should also try a year that is evenly divisible by 4 and not by 100. This is left as an exercise for you.

We mentioned that Objective-C gives the programmer a tremendous amount of flexibility in forming expressions. For instance, in the previous program, you did not have to calculate the intermediate results rem_4, rem_100, and rem_400—you could have performed the calculation directly inside the if statement, as follows:

```
if ( year %4 == 0 && year %100 != 0 ) || year %400 == 0 )
```

Using blank spaces to set off these operators still makes the previous expression readable. If you decided to ignore this and removed the unnecessary set of parentheses, you could end up with an expression that looked like this:

```
if(year%4==0&&year%100!=0||year%400==0)
```