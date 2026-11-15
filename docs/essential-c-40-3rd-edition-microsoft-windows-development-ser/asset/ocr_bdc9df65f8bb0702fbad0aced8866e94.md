```
throw new ArgumentNullException("comparisonMethod");
}
for (i = items.Length - 1; i >= 0; i--)
{
    for (j = 1; j <= i; j++)
    {
        if (comparisonMethod(items[j - 1], items[j]))
        {
            temp = items[j - 1];
            items[j - 1] = items[j];
            items[j] = temp;
        }
    }
}
// ...
```

ComparisonHandler is a data type that represents a method for comparing two integers. Within the BubbleSort() method you then use the instance of the ComparisonHandler, called comparisonMethod, inside the conditional expression. Since comparisonMethod represents a method, the syntax to invoke the method is identical to calling the method directly. In this case, comparisonMethod takes two integer parameters and returns a Boolean value that indicates whether the first integer is greater than the second one.

Perhaps more noteworthy than the particular algorithm, the ComparisonHandler delegate is strongly typed to return a bool and to accept only two integer parameters. Just as with any other method, the call to a delegate is strongly typed, and if the data types do not match up, then the C# compiler reports an error. Let us consider how the delegate works internally.

# Delegate Internals

C# defines all delegates, including ComparisonHandler, as derived indirectly from System.Delegate, as shown in Figure 12.1.1

The first property is of type System.Reflection.MethodInfo, which I cover in Chapter 17. MethodInfo describes the signature of a particular method, including its name, parameters, and return type. In addition to

1. The C# standard doesn't specify the delegate implementation's class hierarchy. .NET's implementation, however, does derive indirectly from System.Delegate.