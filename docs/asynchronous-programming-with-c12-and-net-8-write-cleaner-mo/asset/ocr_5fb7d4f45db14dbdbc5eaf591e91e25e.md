```
}
public static async Task<int> Task1()
{
    await Task.Delay(1000); // Simulate asynchronous
delay
    return 10;
}
public static async Task<int> Task2(int input)
{
    await Task.Delay(1500); // Simulate asynchronous
delay
    if (input < 0) throw new
InvalidOperationException("Invalid input");
    return input * 2;
}
public static async Task<int> Task3(int input)
{
    await Task.Delay(2000); // Simulate asynchronous
delay
    return input + 5;
}
}
```