in C# 11.0, when the "static abstract method in interfaces" feature is officially introduced. It is very likely that the next version of .NET will also include a number of helper interfaces to make it easier to represent certain type constraints, such as INumber for instance.

![](bbox=[0.13, 0.21, 0.2, 0.3])

You can try this feature in .NET 6/C# 10.0 by enabling the "preview" option. Refer to other resources if you want to try it out before the C# 11.0 release.

In this lesson, we also introduced the switch expression of C# 8.0. Although it can be viewed as a simple generalization of the ternary expression and the switch statement, its pattern matching capability makes it more flexible and more expressive. We will likely see more and more uses of the switch expressions in Modern C#.

# ## 13.3. Exercises

+   1.  Although the bubble sort algorithm is one of the easiest sorting algorithms, it is rarely used in practice because it is not very efficient. Another sorting algorithm that is easy to implement and that is widely used is the so-called quick sort algorithm. Try implementing the `void Sort<T>(IList<T> arr, T pivot)` where `T : IEquatable<T>, IComparable<T>` method using quick sort.