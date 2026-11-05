```
DisplayGreeting:
{
    Console.WriteLine("Hello! What is your name?");

    input = Console.ReadLine();

    if (input.Length >= 1)
    {
        Console.WriteLine(
            "Hello, " +
            input +
            ", enter 'Exit' at any time to exit this app.");

        goto AwaitFurtherInstruction;
    }
    else
    {
        goto DisplayGreeting;
    }
}

AwaitFurtherInstruction:
{
    input = Console.ReadLine();

    if(input.ToLower() == "exit")
    {
        input = String.Empty;

        Environment.Exit(0);
    }
    else
    {
        goto AwaitFurtherInstruction;
    }
}
}
}
```