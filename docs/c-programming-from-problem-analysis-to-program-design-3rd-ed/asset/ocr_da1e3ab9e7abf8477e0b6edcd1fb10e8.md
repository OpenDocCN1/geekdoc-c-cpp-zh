```
finally
{
    Console.WriteLine("...\n...\n" +
    "Terminated Normally!!!");
}
}
}
```

The application in Example 12-5 is poised to avoid terminating abnormally. Because System.Exception is the base exception class, the catch could have been written without the parenthesized arguments. It is acceptable in C# to write:

```
try
{
    // Statement(s)
}
catch
{
    // Statement(s)
}
```

In Example 12-5, you cannot just remove the (System.Exception e) from the last catch. If you do, a syntax error is generated. The error is not generated because of removal of the type; it is because the catch block uses the identifier e to display the exception type. If you remove "(System.Exception e)", be sure to modify the catch clause code so that it does not refer to the e object.

![](bbox=[0.15, 0.77, 0.22, 0.86])

> You cannot write a catch unless you include it within a try block.

Now, when the user enters nonnumeric characters, such as the 9U entered during the running of the application shown in Figure 12-14, the output shown in Figure 12-17 is produced.