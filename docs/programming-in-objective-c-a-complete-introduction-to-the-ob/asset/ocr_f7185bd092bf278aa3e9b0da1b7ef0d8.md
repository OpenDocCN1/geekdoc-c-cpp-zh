```
triangularNumber = 0;
for ( n = 1; n <= number; ++n)
triangularNumber += n;

NSLog("Triangular number %i is %i", number, triangularNumber);
}
```

[pool drain];
return 0;

# Program 5.5 Output

What triangular number do you want?
12
Triangular number 12 is 78

What triangular number do you want?
25
Triangular number 25 is 325

What triangular number do you want?
50
Triangular number 50 is 1275

What triangular number do you want?
75
Triangular number 75 is 2850

What triangular number do you want?
83
Triangular number 83 is 3486

The program consists of two levels of for statements. The outermost for statement is as follows:

```
for ( counter = 1; counter <= 5; ++counter )
```

This specifies that the program loop is be executed precisely five times. The value of counter is initially set to 1 and is incremented by 1 until it is no longer than or equal to 5 (in other words, until it reaches 6).

Unlike the previous program example, the variable counter is not used anywhere else within the program. However, because it is a variable, you must declare it in the program.

The program loop actually consists of all the more remaining program statements, as indicated by the braces. You might be able to easily comprehend the way this program operates if you conceptualize it as follows:

For 5 times

```
{
  Get the number from the user.
```