```
}

Console.WriteLine("This will only be printed if the 'return' statement isn't executed.");
}
```

Note that whenever we hit a return statement, the flow goes straight back to the point the method was called and nothing more will be executed from within the method.

# Handing Something Off to a Method

On occasion, we will want a method to do something with specific information. We can place what information we want the method to work with inside parentheses in a process called handing off.

```
static void Count(int numberToCountTo)
{
    for(int current = 1; current <= numberToCountTo; current++)
    {
        Console.WriteLine(current);
    }
}
```

Where the method is defined, you add the variable type and provide it with a name that it will use in the method. In our example, numberToCountTo is a parameter. When a method is called and it has a parameter in it, a value can be passed to the method or by placing the value inside parentheses, you can hand off the value so the method can work with it:

```
Count(5);
Count(15);
```

In conjunction with the code before, these two lines will print the numbers 1, 2, 3, 4, 5 and then it will print 1, 2, 3, 4, 5, 6, 7, 8, 9, 10,