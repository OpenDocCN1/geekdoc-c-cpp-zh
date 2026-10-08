```
while (row >= 1)
{
    column = 1;
    while (column <= 10)
    {
        Console.Write(row % 2 == 1 ? "" : ">");
        column++;
    }
    --row;
    Console.WriteLine();
}
```

# 5.27 (Dangling-else Problem) The C# compiler associates an else with the immediately preceding if unless to do otherwise by the placement of braces { and }. This behavior can lead to what is referred to as the dangling-else problem. The indentation of the nested statement

```
if (x > 5)
if (y > 5)
    Console.WriteLine("x and are > 5");
else
    Console.WriteLine("x <= 5");
```

appears that if x is greater than 5, the nested if determines whether y is also greater than 5. If so, the statement continues by printing the string "x and are > 5". Otherwise, it appears if x is not greater than 5, the else part of if...else outputs the string "x <= 5". Beware! This nested...else statement does not execute it. The compiler actually interprets the statement as

```
if (x > 5)
if (y > 5)
    Console.WriteLine("x and are > 5");
else
    Console.WriteLine("x <= 5");
```

in which the body of the first if is a nested...else. The outer statement tests whether x is greater than 5. If the second condition is true, the proper string—”x and are > 5” is displayed. However, if the second condition is false, the string "x <= 5” is displayed. Equally bad, if the inner...else's condition is false, the inner if is skipped and nothing is displayed. For this exercise, add braces to the preceding code snippet to force the nested if...else to execute as it was originally intended.

# 5.28 (Another Dangling-else Problem) Based on the dangling-else discussion in Exercise 5.27, state the output for each of the following code snippets when m is 8 and n is 4 and when m is 4 and n is 8. We eliminated the indentation from the code to make it more challenging. [Hint: Apply the indentation conventions you've learned.]

```
if (m > 5)
    if (n < 20)
        Console.WriteLine("RGB Mode");
    else
        Console.WriteLine("CMYK Mode");
else Console.WriteLine("Greyscale Mode");
```