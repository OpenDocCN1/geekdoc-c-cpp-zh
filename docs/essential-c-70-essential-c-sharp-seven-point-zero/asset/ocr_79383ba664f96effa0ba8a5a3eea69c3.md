```
return result;
}
}
```

```
public class Program
{
public static void Main(string[] args)
{
int[] numbers = new int[args.Length];
for (int count = 0; count < args.Length; count++)
{
numbers[count] = args[count].Length;
}

Console.WriteLine($"Longest argument length = { SimpleMath.Max(numbers) }");
Console.WriteLine($"Shortest argument length = { SimpleMath.Min(numbers) }");
}
```

This class does not have any instance fields (or methods), so creation of such a class would be pointless. Consequently, the class is decorated with the `static` keyword. The `static` keyword on a class provides two facilities. First, it prevents a programmer from writing code that instantiates the `SimpleMath` class. Second, it prevents the declaration of any instance fields or methods within the class. Because the class cannot be instantiated, instance members would be pointless. The `Program` class in prior listings is another good candidate for a `static` class because it too contains only `static` members.

+   End 2.0

One more distinguishing characteristic of the `static` class is that the C# compiler automatically marks it as abstract and sealed within the `CIL`. This designates the class as **inextensible**; in other words, no class can be derived from this class or even instantiate it.

+   Begin 3.0

+   Begin 6.0

In the previous chapter, we saw that the `using static` directive can be used with `static` classes such as `SimpleMath`. For example, adding a `using static SimpleMath;` declarative at the top of Listing 6.41 would allow you to invoke `Max` without the `SimpleMath` prefix:

+   End 6.0

```
Console.WriteLine($"Longest argument length = { Max(numbers) }");
```