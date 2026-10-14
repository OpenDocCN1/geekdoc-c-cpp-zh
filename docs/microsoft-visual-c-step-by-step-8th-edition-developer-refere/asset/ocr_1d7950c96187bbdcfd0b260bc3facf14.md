# Note

The *Console.WriteLine* method automatically calls the *ToString* method of its argument to format the argument as a string.

The *doWork* method should now look like this:

Click here to view code image

```
static void doWork()
{
    ...
    Date defaultDate = new Date();
    Console.WriteLine(defaultDate);
}
```

# Note

When you type *new Date(,* IntelliSense automatically detects that two constructors are available for the *Date* type.

+   8. On the Debug menu, click Start Without Debugging to build and run the program. Verify that the date January 1 1900 is written to the console.
+   9. Press the Enter key to return to the Visual Studio 2015 programming environment.
+   10. In the Code and Text Editor window, return to the *doWork* method and add two more statements. In the first statement, declare a local variable named *weddingAnniversary* and initialize it to July 4 2015. (I actually did get married on Independence Day, although it was many years ago.) In the second statement, write the value of *weddingAnniversary* to the console.

The *doWork* method should now look like this:

Click here to view code image

```
static void doWork()
{
    ...
    Date weddingAnniversary = new Date(2015, Month.July, 4);
    Console.WriteLine(weddingAnniversary);
}
```

+   11. On the Debug menu, click Start Without Debugging, and then confirm that the date July 4 2015 is written to the console below the previous information.
+   12. Press Enter to close the program and return to Visual Studio 2015.