# 20.6 Generic Classes 871

```
// push elements onto stack
foreach (var element in intElements)
{
    Console.Write($"{element}");\n    intStack.Push(element); // push onto intStack
}
catch (FullStackException exception)
{
    Console.Error.WriteLine($"\nmessage: {exception.Message}");
    Console.Error.WriteLine(exception.StackTrace);
}
```

```
// test Pop method with intStack
private static void TestPopInt()
{
    // pop elements from stack
    Console.Error.WriteLine("\npopping elements from intStack");
    int popValue; // store element removed from stack
    // remove all elements from stack
    while (true)
    {
        popValue = intStack.Pop(); // pop from intStack
        Console.Write($"popValue:{popValue}");\
    }
}
catch (EmptyStackException exception)
{
    Console.Error.WriteLine("\nmessage: {exception.Message}");
    Console.Error.WriteLine(exception.StackTrace);
}
```

Push elements onto doubleStack
1.1 2.2 3.3 4.4 5.5 6.6
Message: Stack is full,cannot push 6.6
At Stack!1.Push(T pushValue) in C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 35
At Test.TestPopDouble(C) in C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 39

Popping elements from doubleStack
5.5 4.4 3.3 2.2 1.1
Message: Stack is empty, cannot pop
At Stack!1.Pop() in C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 49
At Test.TestPopDouble(C) in C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 62

Fig20.8 | Testing generic class. (Part 3 of 4)