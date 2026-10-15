
```
```csharp
{
    int i;
    int[] items = new int[5];

    for (i=0; i < items.Length; i++)
    {
        Console.Write("Enter an integer: ");
        items[i] = int.Parse(Console.ReadLine());
    }

    BubbleSort(items, GreaterThan);

    for (int i = 0; i < items.Length; i++)
    {
        Console.WriteLine(items[i]);
    }
}
```
```

Note that the ComparisonHandler delegate is a reference type, but you do not necessarily use new to instantiate it. The conversion from the **method group**—the expression that names the method—to the delegate type automatically creates a new delegate object in C# 2.0 and later.

## ADVANCED TOPIC

## Delegate Instantiation in C# 1.0

In Listing 12.7, the delegate was instantiated by simply passing the name of the desired method, GreaterThan, as an argument to the call to the BubbleSort() method. The first version of C# required instantiation of the delegate, using the more verbose syntax shown in Listing 12.8.

## LISTING 12.8: Passing a Delegate As a Parameter in C# 1.0

```
```csharp
BubbleSort(items,
    new ComparisonHandler(GreaterThan));
```
```

Later versions support both syntaxes; throughout the remainder of the book we will show only the modern, concise syntax.

Although all delegate data types derive indirectly from System.Delegate, the C# compiler does not allow you to declare a class that derives directly or indirectly from System.Delegate or System.MulticastDelegate. As a consequence, the code shown in Listing 12.9 is not valid.

## LISTING 12.9: System.Delegate Cannot Explicitly Be a Base Class

```
// ERROR: 'ComparisonHandler' cannot
// inherit from special class 'System.Delegate'
public class ComparisonHandler: System.Delegate
{
    // ...
}
```

Passing the delegate to specify the sort order is a significantly more flexible strategy than using the approach described at the beginning of this chapter. By passing a delegate you can change the sort order to be alphabetical simply by adding an alternative delegate to convert integers to strings as part of the comparison. Listing 12.10 shows a full listing that demonstrates alphabetical sorting, and Output 12.1 shows the results.

## LISTING 12.10: Using a Different ComparisonHandler-Compatible Method

```
using System;
class DelegateSample
{
    public delegate bool ComparisonHandler(int first, int second);
    public static void BubbleSort(
        int[] items, ComparisonHandler comparisonMethod)
    {
        int i;
        int j;
        int temp;
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
    }
```

```
}
}

public static bool GreaterThan(int first, int second)
{
    return first > second;
}

public static bool AlphabeticalGreaterThan(
    int first, int second)
{
    int comparison;
    comparison = (first.ToString().CompareTo(
        second.ToString()));

    return comparison > 0;
}

static void Main(string[] args)
{
    int i;
    int[] items = new int[5];

    for (i=0; i<items.Length; i++)
    {
        Console.Write("Enter an integer: ");
        items[i] = int.Parse(Console.ReadLine());
    }

    BubbleSort(items, AlphabeticalGreaterThan);

    for (i = 0; i < items.Length; i++)
    {
        Console.WriteLine(items[i]);
    }
}
}
```

## OUTPUT 12.1

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

Lambda expressions are themselves divided into two types: **statement lambdas** and **expression lambdas.** Figure 12.2 shows the hierarchical relationship between these terms.

## Statement Lambdas

The purpose of a lambda expression is to eliminate the hassle of declaring an entirely new member when you need to make a delegate from a very simple method. Several different forms of lambda expressions exist. A statement lambda, for example, consists of a formal parameter list, followed by the lambda operator =>, followed by a code block.

Listing 12.11 shows equivalent functionality to the call to BubbleSort from Listing 12.7, except that Listing 12.11 uses a statement lambda to represent the comparison method, rather than creating a GreaterThan method. As you can see, much of the information that appeared in the GreaterThan method declaration is included in the statement lambda; the formal parameter declarations and the block are the same, but the method name and its modifiers are missing.

## LISTING 12.11: Creating a Delegate with a Statement Lambda

```
// ...
    BubbleSort(items,
        (int first, int second) =>
        {
            return first < second;
        }
    );
// ...
```

When reading code that includes a lambda operator, you would replace the lambda operator with the words go/goes to. For example, in Listing 12.11, you would read the second BubbleSort() parameter as “integers first and second go to returning the result of first less than second.”

As readers will observe, the syntax in Listing 12.11 is almost identical to that in Listing 12.7, apart from the fact that the comparison method is now found lexically where it is converted to the delegate type, rather than being found elsewhere and looked up by name. The name of the method is missing, which explains why such methods are called “anonymous functions.”

The return type is missing, but the compiler can see that the lambda expression is being converted to a delegate whose signature requires the return type bool. The compiler verifies that the expressions of every return statement in the statement lambda’s block would be legal in a bool-returning method. The public modifier is missing; given that the method is no longer an accessible member of the containing class, there is no need to describe its accessibility. Similarly, the static modifier is no longer necessary. The amount of “ceremony” around the method is already greatly reduced.

The syntax is still needlessly verbose, however. We have deduced from the delegate type that the lambda expression must be bool-returning; we can similarly deduce that both parameters must be of type int, as shown in Listing 12.12.

## LISTING 12.12: Omitting Parameter Types from Statement Lambdas

```
// ...

BubbleSort(items,
    (first, second) =>
    {
        return first < second;
    }
);

// ...
```

In general, explicitly declared parameter types are optional in all lambda expressions if the compiler can infer the types from the delegate that the lambda expression is being converted to. For situations when specifying the type makes code more readable, however, C# enables you to do so. In cases where inference is not possible, the C# language requires that the lambda parameter types be stated explicitly. If one lambda parameter type is specified explicitly, then all of them must be specified explicitly, and they must all match the delegate parameter types exactly.

## Guidelines

- CONSIDER omitting the types from lambda formal parameter lists when the types are obvious to the reader, or when they are an insignificant detail.

One other means of reducing the syntax is possible, as shown in Listing 12.13: A lambda expression that has exactly one parameter whose type is inferred may omit the parentheses around the parameter list. If there are zero parameters or more than one parameter, or if the single parameter is explicitly typed, the lambda must have parentheses around the parameter list.

## LISTING 12.13: Statement Lambdas with a Single Input Parameter

```
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
// ...
IEnumerable<Process> processes = Process.GetProcesses().Where(
    process => { return process.WorkingSet64 > 1000000000; });
// ...
```

In Listing 12.13, the where() method returns a query for processes that have a physical memory utilization greater than 1 billion bytes. Contrast this with Listing 12.14, which has a parameterless statement lambda. The empty parameter list requires parentheses. Note also that in Listing 12.14, the body of the statement lambda includes multiple statements inside the statement block (via curly braces). Although a statement lambda can contain any number of statements, typically a statement lambda uses only two or three statements in its statement block. (The use of the generic Func delegate type is described in the section “General-Purpose Delegates: System.Func and System.Action” later in this chapter.)

## LISTING 12.14: Parameterless Statement Lambdas

```
using System;
// ...
Func<string> getUserInput =
    () =>
    {
        string input;
        do
        {
            input = Console.ReadLine();
        }
        while(input.Trim().Length == 0);
        return input;
    };
// ...
```
