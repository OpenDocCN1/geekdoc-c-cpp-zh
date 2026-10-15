```
public static void FirstFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("First Thread Displays: " + number);
        Thread.Sleep(200);
    }
    StateOfThreads("FirstFunction()");
}
public static void SecondFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("Second Thread Displays: " + number);
        Thread.Sleep(500);
    }
    StateOfThreads("SecondFunction()");
}
public static void ThirdFunction()
{
    for (int number = 1; number <= 5; number++)
    {
        Console.WriteLine("Third Thread Displays: " + number);
        Thread.Sleep(700);
    }
    StateOfThreads("ThirdFunction()");
    Console.Write("\nPress ENTER to quit...");
    Console.ReadLine();
}
```

In Listing 31.8, you can see that after setting the names of the threads, the current states of the three threads are displayed by calling the static method named as StateOfThreads() at various levels in the application.
Figure 31.8 shows the output of Listing 31.8:

![](bbox=[0.25, 0.55, 0.8, 0.92])

Figure 31.8: Determining a Thread State