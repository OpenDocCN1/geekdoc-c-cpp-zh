```
}
_elements.Insert(i, value);
}}
```

This algorithm is naively simple, and much better ways exist to keep a sorted collection using tree structures and whatnot, but what matters to us here is how the constraint now allows us to rely on the CompareTo method on objects of type T. In this particular case, the compiler knows that List<T>’s indexer will return an object of type T. Because the value argument passed to Add is also of type T, it’s possible to resolve the CompareTo method call correctly as proven in Figure 15.16.

![](bbox=[0.08, 0.38, 0.88, 0.73])

FIGURE 15.16 IntelliSense knows about the generic constraints.

To convince yourself this algorithm works (and to get an idea about how suboptimal this choice of algorithm is), you can use the following code:

```
var ordered = new OrderedList<int>();
var rand = new Random();
for (int i = 0; i < 10000; i++)
    ordered.Add(rand.Next(100));

bool faulty = false;
int prev = -1;

// Note: don't forget to implement GetEnumerator methods as shown in Figure 15.16.
foreach (var n in ordered) {
    if (prev > n) {
        faulty = true;
```