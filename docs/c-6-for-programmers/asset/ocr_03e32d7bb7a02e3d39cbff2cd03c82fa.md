```
```csharp
// push elements onto stack
try
{
    Console.WriteLine("\nPushing elements onto doubleStack");

    // push elements onto stack
    foreach (var element in doubleElements)
    {
        Console.Write($"{element:F1} ");
        doubleStack.Push(element); // push onto doubleStack
    }
}
catch (FullStackException exception)
{
    Console.Error.WriteLine($"\nMessage: {exception.Message}");
    Console.Error.WriteLine(exception.StackTrace);
}
}

// test Pop method with doubleStack
private static void TestPopDouble()
{
    // pop elements from stack
    try
    {
        Console.WriteLine("\nPopping elements from doubleStack");

        double popValue; // store element removed from stack

        // remove all elements from stack
        while (true)
        {
            popValue = doubleStack.Pop(); // pop from doubleStack
            Console.Write($"{popValue:F1} ");
        }
    }
    catch (EmptyStackException exception)
    {
        Console.Error.WriteLine($"\nMessage: {exception.Message}");
        Console.Error.WriteLine(exception.StackTrace);
    }
}

// test Push method with intStack
private static void TestPushInt()
{
    // push elements onto stack
    try
    {
        Console.WriteLine("\nPushing elements onto intStack");
    }
```
```

Fig. 18.8 | Testing generic class Stack. (Part 2 of 4.)