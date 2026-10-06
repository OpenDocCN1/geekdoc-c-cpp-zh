```
}
return 0;
}
```

# Program 4.4. Output

```
a % b = 0
a % c = 5
a % d = 4
a / d * d + a % d = 25
```

The statement inside main that defines and initializes the variables a, b, c, and d in a single statement.

As you know, NSLog uses the character that immediately follows the percent sign to determine how to print its next argument. However, if it is another percent sign that follows, the NSLog routine takes this as an indication that you really intend to display a percent sign and inserts it at the appropriate place in the program's output.

You are correct if you concluded that the function of the modulus operator % is to give the remainder of the first value divided by the second value. In the first example, the remainder of 25 divided by 5 is 0. If you divide 25 by 10, you would have a remainder of 5, as verified by the second line of output. Dividing 25 by 7 gives a remainder of 4, as shown in the third output line.

Let's now turn our attention to the last arithmetic expression evaluated in the last statement. You will recall that any operations between two integer values in Objective-C are performed with integer arithmetic. Therefore, any remainder resulting from the division of two integer values is simply discarded. Dividing 25 by 7, as indicated by the expression a / d, gives an intermediate result of 3. Multiplying this value by the value of d, which is 7, produces the