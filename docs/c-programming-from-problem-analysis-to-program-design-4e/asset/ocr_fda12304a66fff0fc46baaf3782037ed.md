```
```csharp
for (int i = 0; i < countOfScores; i++)
{
    Console.Write("Enter score {0}: ", i+1);
    inValue = Console.ReadLine();
    examScore[i] = int.Parse(inValue);
    totalScores += examScore[i];
}

averageTestScore = totalScores /
                   countOfScores;
Console.WriteLine("Average is {0}",
                  averageTestScore);
}
catch
{
    Console.WriteLine("Problem with scores - " +
                      "Cannot compute average");
}
Console.ReadKey();
}
}
}
```
```

If the application is run and the user types a nonnumeric character, such as the value 9U (shown entered for score 3 in Figure 12-14), the program does not crash. Instead, the exception-handler code found in the catch block is executed and alerts the user of the error.

![](bbox=[0.186, 0.587, 0.912, 0.747])

**FIGURE 12-14** Generic catch block handles the exception

# GENERIC CATCHES

The problem with using a generic `catch` to avoid abnormal termination is that because any type of exception is handled by the catch code, you are never quite sure what caused the exception to be thrown. Take, for example, the two output listings shown in Figure 12-15.