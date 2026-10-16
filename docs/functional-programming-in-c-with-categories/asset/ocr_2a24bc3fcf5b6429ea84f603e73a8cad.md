```
Action<int, Action<int>> c2) =>
(int x, Action<int> callback) =>
    c1(x, r => c2(r, callback));
```

```
var f = Compose(square, cube);
```

```
f(4, r => Console.WriteLine(r));
```

having this idea of composition, we can fold a list of callbacks.

# Folding Tasks

Having two Tasks, we can compose:

```
Task<int> A = Task<int>.FromResult(5);
Task<int> B = Task<int>.FromResult(7);
```

```
Task<int> Compose(Task<int> t1, Task<int> t2) =>
    t1.ContinueWith(a => a.Result + t2.Result);
```

Having a List of Tasks we can Fold them:

```
var list = new List<Task<int>>() { A, B };
```

```
Task<int> total = Task<int>.FromResult(0);
foreach (var current in list)
{
    total = A.ContinueWith(a => a.Result + B.Result);
}
```

Or using the Aggregate

```
Task<int> t = list.Aggregate(
    Task.FromResult(0),
    (accumulation, current) => A.ContinueWith(a => a.Result + B.Result)
);
```

We will go in more detail in the Monads Chapter.