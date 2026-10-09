And, its test driver:

ring-buffer/src/MRU/Program.cs (lines 3-21)

```
```csharp
3 var cap = 3u;
4 var list = new ShortList<int>(cap);

6 list.Add(1);
7 list.Add(2);
8 Console.WriteLine($"len = {list.Count}");
9 lock (list) {
10     foreach (var item in list) {
            Console.WriteLine($"item = {item}");
    }
11 }
12 
13 list.Add(3);
14 Console.WriteLine($"len = {list.Count}");
15 lock (list) {
16     foreach (var item in list) {
            Console.WriteLine($"item = {item}");
17 }
18 }
```
```

We will leave it to the readers to understand this code sample, and how it differs from the use case of the fixed size FIFO queue.

We could have created additional test projects for testing each of these apps (e.g. using NUnit or XUnit or other C#/.NET testing frameworks). But, for illustration purposes, the "main programs" should suffice. All sample programs in this book are written like they are "real programs", which we can potentially "publish", if desired.

![](bbox=[0.13, 0.7, 0.18, 0.75])