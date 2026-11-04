In this example, we assume the Person type has an overridden implementation for both `GetHashCode` and `Equals`, as shown earlier in this chapter. The default `System.Object` implementation for those methods will result in reference equality semantics, so the two separate instances of a Person called Lisa with age 8 will be treated as different, resulting in five elements in the set rather than four.

Additional element-based methods are illustrated in the following example. Notice the use of the C# 3.0 collection initializer syntax once more:

```
var numbers = new HashSet<int> { 1, 2, 2, 3, 4, 5, 5 }; // { 1, 2, 3, 4, 5 }
numbers.Add(6);                                      // { 1, 2, 3, 4, 5, 6 }
numbers.Remove(3);                                   // { 1, 2,    4, 5, 6 }
numbers.RemoveWhere(n => n % 2 == 0);                // { 1,         5 }
numbers.Clear();                                     // { }

foreach (int number in numbers)
    Console.WriteLine(number);
```

Beside methods that operate at the level of individual elements, `HashSet<T>` exposes set-level operations, too. Let’s define the following sets and illustrate each of those operations using them:

```
var first = new HashSet<int> { 1, 2, 3, 5, 8, 13 };
var second = new HashSet<int> { 2, 3, 5, 7, 11 };
```

Figure 16.11 illustrates four common set-level operations graphically.

![](bbox=[0.064, 0.605, 0.788, 0.94])

**FIGURE 16.11** Set-level operations on `HashSet<T>`.