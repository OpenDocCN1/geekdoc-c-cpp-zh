```
// (1, bar)
// (2, foo)
// (3, qux)
```

Or to reverse the sort use:

```
list.Sort((a, b) => b.Item2.CompareTo(a.Item2));
```

# Section 23.4: Return multiple values from a method

Tuples can be used to return multiple values from a method without using out parameters. In the following example AddMultiply is used to return two values (sum, product).

```
void Write()
{
    var result = AddMultiply(25, 28);
    Console.WriteLine(result.Item1);
    Console.WriteLine(result.Item2);
}

Tuple<int, int> AddMultiply(int a, int b)
{
    return new Tuple<int, int>(a + b, a * b);
}
```

Output:

53
700

Now C# 7.0 offers an alternative way to return multiple values from methods using value tuples More info about ValueTuple struct.