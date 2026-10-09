
creation called *anonymous methods*. Every version of C# after C# 2.0 supports anonymous methods for backward compatibility, but in new code they should be deprecated in favor of using lambda expressions. This chapter includes Advanced Topic blocks that describe how to use anonymous methods should you need to work with legacy C# 2.0 code; you can largely ignore these sections if you are working only with newer code.

We conclude the chapter with a discussion of *expression trees*, which enable you to use the compiler's analysis of a lambda expression at execution time.

![](img/ef6a8a417630b222bfb3f3b949facff0_574_0.png)

## Introducing Delegates

Veteran C and C++ programmers have long used function pointers as a mechanism for passing a reference to one method as an argument to another method. C# achieves similar functionality by using **delegates**. Delegates allow you to capture a reference to a method and pass it around like any other object, and to call the captured method like any other method. Let's consider an example illustrating how this technique might be useful.

## Defining the Scenario

Although it is not very efficient, one of the simplest sort routines is the bubble sort. Listing 13.1 shows the BubbleSort() method.

```csharp
// LISTING 13.1: BubbleSort() Method
static class SimpleSort1
{
    public static void BubbleSort(int[] items)
    {
        int i;
        int j;
        int tmp;
        if (items == null)
        {
            return;
        }

        for (i = items.Length - 1; i >= 0; i--)
        {
            for (j = 1; j <= i; j++)
            {
                if (items[j - 1] > items[j])
                {
                    tmp = items[j - 1];
                    items[j - 1] = items[j];
                    items[j] = tmp;
                }
            }
        }
        // ...
    }
}
```

This method will sort an array of integers in ascending order.

Suppose you need to sort the integers in Listing 13.1 in either ascending or descending order. You could duplicate the code and replace the greater-than operator with a less-than operator, but it seems like a bad idea to replicate several dozen lines of code merely to change a single operator. As a less verbose alternative, you could pass in an additional parameter indicating how to perform the sort, as shown in Listing 13.2.

### LISTING 13.2: BubbleSort() Method, Ascending or Descending

```csharp
class SimpleSort2
{
    public enum SortType
    {
        Ascending,
        Descending
    }

    public static void BubbleSort(int[] items, SortType sortOrder)
    {
        int i;
        int j;
        int tmp;
        if (items == null)
        {
            return;
        }

        for (i = items.Length - 1; i >= 0; i--)
        {
            for (j = 1; j <= i; j++)
            {
                bool swap = false;
                switch (sortOrder)
                {
                    case SortType.Ascending:
                        swap = items[j - 1] > items[j];
                        break;
                    case SortType.Descending:
                        swap = items[j - 1] < items[j];
                        break;
                }
                if (swap)
                {
                    tmp = items[j - 1];
                    items[j - 1] = items[j];
                    items[j] = tmp;
                }
            }
        }
        // ...
    }
}
```

However, this code handles only two of the possible sort orders. If you wanted to sort them lexicographically (that is, 1, 10, 11, 12, 2, 20, ...), or order them via some other criterion, it would not take long before the number of SortType values and the corresponding switch cases would become cumbersome.

### Delegate Data Types

To increase flexibility and reduce code duplication in the previous code listings, you can make the comparison method a parameter to the BubbleSort() method. To pass a method as an argument, a data type is required to represent that method; this data type is generally called a *delegate* because it “delegates” the call to the method referred to by the object. You can use the name of a method as a delegate instance. And, since C# 3.0, you can also use a lambda expression as a delegate, to express a short piece of code “in place” rather than creating a method for it. (In C# 7.0, you can create local function and then use the function name for the delegate as well.) Listing 13.3 includes a modification to the BubbleSort() method that takes a lambda expression parameter. In this case, the delegate data type is Func<int, int, bool>.

### LISTING 13.3: BubbleSort() with Delegate Parameter

```csharp
class DelegateSample
{
    // ...
    public static void BubbleSort(
        int[] items, Func<int, int, bool> compare)
    {
        int i;
        int j;
        int temp;

        if (compare == null)
        {
            throw new ArgumentNullException(nameof(compare));
        }

        if (items == null)
        {
            return;
        }

        for (i = items.Length - 1; i >= 0; i--)
        {
            for (j = 1; j <= i; j++)
            {
                if (compare(items[j - 1], items[j]))
                {
                    temp = items[j - 1];
                    items[j - 1] = items[j];
                    items[j] = temp;
                }
            }
        }
        // ...
    }
}
```

The delegate of type Func<int, int, bool> represents a method that compares two integers. Within the BubbleSort() method, you then use the instance of the Func<int, int, bool>, referred to by the compare parameter, to determine which integer is greater. Since compare represents a method, the syntax to invoke the method is identical to calling any other method. In this case, the Func<int, int, bool> delegate takes two integer parameters and returns a Boolean value that indicates whether the first integer is greater than the second one:

```csharp
if (compare(items[j - 1], items[j])) { ... }
```

Note that the Func<int, int, bool> delegate is strongly typed to represent a method that returns a bool and accepts exactly two integer parameters. Just as with any other method call, the call to a delegate is strongly typed, and if the data types for the arguments are not compatible with the parameters, the C# compiler reports an error.

### Declaring Delegate Types

You just saw how to define a method that uses a delegate, and you learned how to invoke a call to the delegate simply by treating the delegate variable as a method. However, you have yet to learn how to declare a delegate type. To declare a delegate type, you use the delegate keyword and follow it with what looks like a method declaration. The signature of that method is the signature of the method that the delegate can refer to, and the name of the delegate type appears where the name of the method would appear in a method declaration. The Func<...> delegate in Listing 13.3, for example, is declared as

```csharp
public delegate TResult Func<in T1, in T2, out TResult>(
    in T1 arg1, in T2 arg2)
```

(The in/out type modifiers were not added until C# 4.0, and we will discuss them later in the chapter.)

### General Purpose Delegate Types: System.Func and System.Action

Fortunately, starting with C# 3.0, it turns out you rarely, if ever, need to declare your own delegates. The need to define your own custom delegate types was effectively eliminated with the .NET 3.5 runtime library (which corresponds to C# 3.0) because it included a set of general-purpose delegates, most of them generic. The System.Func family of delegates is for referring to methods that return a value; the System.Action family of delegates is for referring to void-returning methods. The signatures for these delegates are shown in Listing 13.4.

### LISTING 13.4: Func and Action Delegate Declarations

```csharp
public delegate void Action();
public delegate void Action<in T>(T arg)
public delegate void Action<in T1, in T2>(
    in T1 arg1, in T2 arg2)
public delegate void Action<in T1, in T2, in T3>(
    T1 arg1, T2 arg2, T3 arg3)
public delegate void Action<in T1, in T2, in T3, in T4>(
    T1 arg1, T2 arg2, T3 arg3, T4 arg4)
// ...
public delegate void Action<
    in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8,
    in T9, in T10, in T11, in T12, in T13, in T14, in T15, in T16>(
    T1 arg1, T2 arg2, T3 arg3, T4 arg4,
    T5 arg5, T6 arg6, T7 arg7, T8 arg8,
    T9 arg9, T10 arg10, T11 arg11, T12 arg12,
    T13 arg13, T14 arg14, T15 arg15, T16 arg16)

public delegate TResult Func<out TResult>();
public delegate TResult Func<in T, out TResult>(T arg)
public delegate TResult Func<in T1, in T2, out TResult>(
    in T1 arg1, in T2 arg2)
public delegate TResult Func<in T1, in T2, in T3, out TResult>(
    T1 arg1, T2 arg2, T3 arg3)
public delegate TResult Func<in T1, in T2, in T3, in T4,
    out TResult>(T1 arg1, T2 arg2, T3 arg3, T4 arg4)
// ...
public delegate TResult Func<
    in T1, in T2, in T3, in T4, in T5, in T6, in T7, in T8,
    in T9, in T10, in T11, in T12, in T13, in T14, in T15, in T16,
    out TResult>(
    T1 arg1, T2 arg2, T3 arg3, T4 arg4,
    T5 arg5, T6 arg6, T7 arg7, T8 arg8,
    T9 arg9, T10 arg10, T11 arg11, T12 arg12,
    T13 arg13, T14 arg14, T15 arg15, T16 arg16)

public delegate bool Predicate<in T>(T obj)
```

Since the delegate definitions are generic, it is possible to use them instead of defining your own custom delegate (which we discuss shortly).

The first delegate type in Listing 13.4 is an *Action<...>*. It is used to represent a method for which there is no return and supports methods of up to 16 parameters. For delegates that need to return a result, there is the *Func<...>* delegate. The last type parameter of *Func<...>* is *TResult*—the type of the return. The other type parameters on *Func<...>* correspond in sequence to the types of the delegate parameters.
