# 2.3 Folding monoids showcase

In this section we are going to display some examples of monoid folding using the Aggregate function. In all the examples we are going to:

+   1. Identify some type S and find some way to combine two S into a single S.
+   2. Then having that given a List of S we can use Aggregate to fold them.

# Folding delegates Func<,>

We will study this case extensively later in this chapter because it is the base of many classical object-oriented patterns. Here we will start with two Func<int, int> delegates:

```
Func<int, int> A = (x) => x + 1;
Func<int, int> B = (x) => x + 2;
```

Having those two we can find a function that combines them into a single Func<int, int>

```
Func<int, int> compose = (x) => A(x) + B(x);
```

Having this function, we can now fold a whole list of Func<int, int> into one.

```
List<Func<int, int>> list = new List<Func<int, int>>() { A, B };
```

```
Func<int, int> accumulation = (x) => x;
foreach (var current in list)
{
    accumulation = (x) => accumulation(x) + current(x);
}
```

This for loop can be abbreviated using the Aggregate method:

```
var folding = list.Aggregate(
    (int x) => x,
    (Func<int, int> accumulation, Func<int, int> current) =>
        (x) => accumulation(x) + current(x)
);
```

```
Console.WriteLine(folding(2));
```

# Folding callbacks

Having two callbacks, we can find a way to compose them into a single callback:

```
Action<int, Action<int>> square = (x, callback) => callback(x * x);
Action<int, Action<int>> cube = (x, callback) => callback(x * x * x);
```

```
Action<int, Action<int>> Compose(Action<int, Action<int>> c1,
```