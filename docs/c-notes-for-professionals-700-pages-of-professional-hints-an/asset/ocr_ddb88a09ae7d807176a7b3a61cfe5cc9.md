```
if (conditionA == true && conditionB == false && conditionC == true) // ...
```

This can be rewritten as

```
if (conditionA && !conditionB && conditionC)
```

# Section 4.3: If-Else If-Else Statement

Following on from the If-Else Statement example, it is now time to introduce the Else If statement. The Else If statement follows directly after the If statement in the If-Else If-Else structure, but intrinsically has has a similar syntax as the If statement. It is used to add more branches to the code than what a simple If-Else statement can.

In the example from If-Else Statement, the example specified that the score goes up to 100; however there were never any checks against this. To fix this, lets modify the method from If-Else Statement to look like this:

```
static void PrintPassOrFail(int score)
{
    if (score > 100) // If score is greater than 100
    {
        Console.WriteLine("Error: score is greater than 100!");
    }
    else if (score < 0) // Else If score is less than 0
    {
        Console.WriteLine("Error: score is less than 0!");
    }
    else if (score >= 50) // Else if score is greater or equal to 50
    {
        Console.WriteLine("Pass!");
    }
    else // If none above, then score must be between 0 and 49
    {
        Console.WriteLine("Fail!");
    }
}
```

All these statements will run in order from the top all the way to the bottom until a condition has been met. In this new update of the method, we've added two new branches to now accommodate for the score going out of bounds.

For example, if we now called the method in our code as PrintPassOrFail(118);, the output would be a Console Print saying Error: score is greater than 100!; and if we called the method in our code like PrintPassOrFail(-28);, the output would say Error: score is less than 0!.