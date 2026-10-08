+   **11. Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 11.1.**

![](bbox=[0.33, 0.185, 0.75, 0.29])

**FIGURE 11.1**
Runtime exception generated from the lack of type-safety

Not only have you lost type safety, you are also performing *n*+1 conversion operations, where *n* is the number of elements in the array. As you might guess, the larger the array, the more expensive this method becomes.

Using generics, this problem becomes simple. You gain the ability to write the code only once without losing type safety or incurring multiple conversion operations. Listing 11.3 shows the same **Min** method defined using generics. If you compare this to the method defined in Listing 11.1, you can see that they are almost identical.

# **LISTING 11.3 Finding the Minimum Value Using Generics**

```
public T Min<T>(T[] values) where T: IComparable<T>
{
T min = values[0];
foreach (T value in values)
{
if (value.CompareTo(min) < 0)
{
min = value;
}
}
return min;
}
```

> **By the Way**
**where T : IComparable<T>**
This constraint might be a bit confusing because it looks like there is a circular dependency here. In fact, it's actually straightforward and means that T must be a type that can be compared to other T's.

The biggest difference is that the generic version uses a generic type parameter *T*, specified by the **<T>** syntax, after the method name. The type parameter acts as a placeholder for a real type supplied at compile time. In this example, we know that