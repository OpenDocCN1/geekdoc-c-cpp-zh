```
```csharp
Console.WriteLine("Final Result: " + result);
}
catch (Exception ex)
{
    Console.WriteLine("Error: " + ex.Message);
}
}

public static async Task<int> Task1()
{
    await Task.Delay(1000); // Simulate asynchronous delay
    return 10;
}

public static async Task<int> Task2(int input)
{
    await Task.Delay(1500); // Simulate asynchronous delay
    return input * 2;
}

public static async Task<int> Task3(int input)
{
    await Task.Delay(2000); // Simulate asynchronous delay
    return input + 5;
}
}
```
```

In this example, `Task1`, `Task2`, and `Task3` are chained sequentially using `await`. Each method performs an asynchronous operation and passes its result to the next method in the chain.

# 2. Parallel Execution and Combining Results: