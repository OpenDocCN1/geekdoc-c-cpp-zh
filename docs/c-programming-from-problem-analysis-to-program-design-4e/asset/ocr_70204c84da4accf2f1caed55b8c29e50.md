```
public void Push(T anItem)
{
    items[stackPointer] = anItem;
    stackPointer++;
}
}
```

Example 11-30 illustrates the changes needed to implement the class. Notice three separate objects are instantiated. The only values that can be placed in the int Stack are integers. Thus, a type-safe data structure has been created.

# EXAMPLE 11.30

```
public class TestOfGenericStack
{
    static void Main(string[] args)
    {
        Stack<int> intStack = new Stack<int>(5);
        Stack<double> doubleStack = new Stack<double>(5);
        Stack<string> stringStack = new Stack<string>(5);
        stringStack.Push("test");

        intStack.Push(100);
        intStack.Push(200);

        doubleStack.Push(3.6);

        Console.WriteLine("Values in the 3 Stacks are: " +
            doubleStack.Pop() + ", " +
            intStack.Pop() + ", " +
            intStack.Pop() + ", " +
            stringStack.Pop());
        Console.ReadKey();
    }
}
```

Notice no casting was necessary in Example 11-30. The output produced from Examples 11-29 and 11-30 is the same as what was shown in Figure 11-17.

# Generic Methods

You can define generic methods that are not part of a generic class. This way, the method defers the specification of one or more types until the method is declared and instantiated by client code. Defining a generic method is similar to defining a generic class. You insert an identifier between the left and right brackets on the method definition line to indicate it is a generic method. Then place that identifier either in the parameter list or as a return type or in both places. This is illustrated in Example 11-31.