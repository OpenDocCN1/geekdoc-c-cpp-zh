```
May, June, July, August,
September, October, November, December
}
}
```

5. Display the Program.cs file in the Code and Text Editor window.

As in the exercises in previous chapters, the Main method calls the doWork method and traps any exceptions that occur.

6. In the Code and Text Editor window, add a statement to the doWork method to declare a variable named first of type Month and initialize it to Month.January. Add another statement to write the value of the first variable to the console.

The doWork method should look like this:

Click here to view code image

```
static void doWork()
{
    Month first = Month.January;
    Console.WriteLine(first);
}
```

# Note

When you type the period following Month, Microsoft IntelliSense automatically displays all the values in the Month enumeration.

7. On the Debug menu, click Start Without Debugging.

Visual Studio 2015 builds and runs the program. Confirm that the word January is written to the console.

8. Press Enter to close the program and return to the Visual Studio 2015 programming environment.

9. Add two more statements to the doWork method to increment the first variable and display its new value to the console, as shown in bold here:

Click here to view code image

```
static void doWork()
{
    Month first = Month.January;
    Console.WriteLine(first);
    first++;
    Console.WriteLine(first);
}
```

10. On the Debug menu, click Start Without Debugging.

Visual Studio 2015 builds and runs the program. Confirm that the words