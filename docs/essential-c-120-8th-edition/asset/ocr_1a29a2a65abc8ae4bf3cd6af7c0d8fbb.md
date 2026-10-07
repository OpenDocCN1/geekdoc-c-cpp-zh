# Guidelines

CONSIDER whether the readability benefit of defining your own delegate type outweighs the convenience of using a predefined generic delegate type.

# ADVANCED Topic

# Declaring a Delegate Type

In many cases, the inclusion of Func and Action delegates in Microsoft .NET Framework 3.5, and later in the .NET Standard, virtually eliminates the need to define your own delegate types. However, you should consider declaring your delegate types when doing so significantly increases the readability of the code. A delegate named Comparer, for example, provides an explicit indication of what the delegate is used for, whereas Func<int, int, bool> only identifies the delegate's parameters and return type. Listing 13.5 shows how to declare the Comparer delegate to require two integers and return a Boolean value.

Listing 13.5: Declaring a Delegate Type

```
public delegate bool Compar(
    int first, int second);
```

Given the new delegate type, you can update Listing 13.3 with a signature that replaces Func<int, int, bool> with Comparer:

```
public static void BubbleSort(int[]) items, Comparer compare
```

Just as classes can be nested in other classes, so delegates can also be nested in classes. If the delegate declaration appeared within another class, the delegate type would be a nested type, as shown in Listing 13.6.

Listing 13.6: Declaring a Nested Delegate Type

```
public class DelegateSample
{
    public delegate bool ComparisonHandler(
```