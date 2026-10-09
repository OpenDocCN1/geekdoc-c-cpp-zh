```
BubbleSort(items, AlphabeticalGreaterThan);
```
for (i = 0; i < items.Length; i++)
{
    Console.WriteLine(items[i]);
}
```
}
```

# **OUTPUT 13.1**

```
Enter an integer: 1
Enter an integer: 12
Enter an integer: 13
Enter an integer: 5
Enter an integer: 4
1
12
13
4
5
```

The alphabetical order is different from the numeric order. Even so, notice how simple it was to add this additional sort mechanism compared to the process used at the beginning of the chapter. The only changes to create the alphabetical sort order were the addition of the `AlphabeticalGreaterThan` method and then passing that method into the call to `BubbleSort()`.

# # Lambda Expressions

In Listings 13.7 and 13.10, we saw that you can convert the expressions `GreaterThan` and `AlphabeticalGreaterThan` to a delegate type that is compatible with the parameter types and the return type of the named method. You might have noticed that the declaration of the `GreaterThan` method—the code that says it is a public, static, bool-returning method with two parameters of type int named `first` and `second`—was considerably larger than the body of the method, which simply compared its two parameters and returned the result. It is unfortunate that so much ceremony must surround such a simple method merely so that it can be converted to a delegate type.

To address this concern, C# 2.0 introduced a far more compact syntax for creating a delegate, and C# 3.0 introduced several even more compact

![](bbox=[0.01, 0.69, 0.12, 0.75])