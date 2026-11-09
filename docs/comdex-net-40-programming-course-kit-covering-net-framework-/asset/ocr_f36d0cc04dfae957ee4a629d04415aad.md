```
```csharp
for (i = 1; i <= 10; ++i)
{
    Console.WriteLine("Iteration " + i);
}
Console.WriteLine("For loop terminated");
Console.ReadLine();
}
```
```

In the highlighted code of Listing 19, we first declare an int type variable, i. The i variable acts as the loop control variable for the for loop. It is declared before the for loop but initialized to 1 in the for loop. After initializing the i variable, the for loop checks the expression, i <= 10, which is the condition of the for loop. If this condition is true, then the number of current iteration is displayed. After this, the i variable is incremented by 1. This completes one iteration of the for loop. The control now goes to the condition where the updated value of the i variable is checked again. In this way, the for loop iterates 10 times. At the end of the tenth iteration, the i variable is equal to 11. Therefore, in the eleventh iteration, the condition becomes false. As a result, the control terminates the for loop, and the for loop terminated, is displayed.

+   8. Press the F5 key on the keyboard to run the application. The output of the application appears, as shown in Fig.C#-1.25:

![](bbox=[0.424, 0.445, 0.562, 0.505])

Fig.C#-1.25

Note that you can omit any or all of the initializer, condition, or update expressions. However, you cannot omit the semicolon that separates the three expressions. You can omit the initializer expression only when you declare and initialize the loop control variable before the for loop. If you omit the condition expression in a for loop, then by default, the condition is assumed to be true and the for loop keeps executing infinitely. The loops that keeps executing forever are called infinite loops. You can also create an infinite loop by omitting the update expression of the for loop. However, you should avoid creating infinite loops while developing programs.

Let's look at the example of an infinite for loop given in the following code snippet:

```
```csharp
for (int i=0;i<3;)
{
    console.WriteLine("Infinite Loop");
}
```
```

In the preceding code snippet, the loop control variable, i, is declared and initialized to zero. In the for loop, the expression, i<3, is the condition. Note that there is no update expression in the for loop. Therefore, in this case, the i<3 condition is always true because the value of the i variable does not change and is always less than 3. This implies that this for loop executes infinite number of times, displaying the message Infinite Loop.

# ### Using the foreach Loop

The foreach loop is similar to the for loop with a slight difference. The foreach loop allows you to iterate through arrays and collections (collections are similar to arrays but unlike arrays, they can store different types of objects together). Unlike the for loop, the foreach loop does not check any condition. The foreach loop simply goes through the items or elements of an array or collection and executes a set of statements for every element. The foreach loop automatically terminates after the execution of statements for the last element of the array or collection.