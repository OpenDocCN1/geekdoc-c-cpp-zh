```
Console.WriteLine("Life lost.");
}
```

Of course, this means if the shields are less than or equal to zero and the armor is less than or equal to zero. Both of these conditions must be true for the life to be lost.

The || operator works much the same with the exception that only one condition has to be true:

The || operator works in a similar way, except that only one of the two sides needs to be true:

```
int shields = 60;
int armor = 30;
```

```
if(shields > 0 || armor > 0)
{
Console.WriteLine("You're alive! Keep going!");
}
```

When you use either operator, a computer will do what’s known as “lazy evaluation” and this means that, unless it has to, it will not check the second part. So, in the previous example, the computer always checks the shields to see if they are greater than 0 but the only time it will check armor greater than 0 is when shields is equal to 0.

You can also put several of these together and, using parentheses, come up with some unique conditions. Whatever you want to do is possible; you just have to keep an eye on readability and that leads us to an alternative way of writing code to make it more readable.

# Nesting if Statements

The last thing I want to discuss is the nested if statement. What this means is that if statements and if-else statements can be placed inside other if statements in a process called nesting.